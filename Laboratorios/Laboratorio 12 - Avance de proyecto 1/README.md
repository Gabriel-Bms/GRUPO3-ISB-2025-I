# LABORATORIO 10 - PROCESAMIENTO EEG
## **Actividades** 

## Fuente de datos 
*EEGBCI – EEG Motor Movement/Imagery Dataset*

Fuente: PhysioNet

URL: https://physionet.org/content/eegmmidb/1.0.0/

Electrodos: 64 canales (10-10 International System)

Frecuencia de muestreo: 160 Hz

Formato: .edf

Descripción: Este databaset registra movimientos reales e imaginarios de las manos y pies derecho e izquiero. Este es ideal para BCI y análisis de foco atencional durante tareas motoras.

## Preprocesamiento de señales EEG
```python
raw = mne.io.read_raw_edf("S001R03.edf", preload=True)
raw.set_eeg_reference('average')
raw.filter(0.5, 40)
raw.notch_filter(freqs=60)
raw.plot(scalings='auto', n_channels=10)
```

<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%2010%20-%20Procesamiento%20de%20EEG/imagenes/1eeg1.png><p>
  </p>
</div>
<br>
<br>
</p>



Segmentación y extracción de eventos
```python
events, event_id_all = mne.events_from_annotations(raw)
print(event_id_all)

# Definir solo las tareas motoras (T1 y T2 en S001R03)
event_id = {
    'tarea_mano_derecha': event_id_all['T1'],  # usualmente 2
    'tarea_mano_izquierda': event_id_all['T2']  # usualmente 3
}

epochs = mne.Epochs(raw, events, event_id=event_id,
                    tmin=0, tmax=4, baseline=None, preload=True)
```
Potencia por bandas EEG
```python
import numpy as np
from mne.time_frequency import psd_array_welch

def extract_bandpower(epoch_data, sfreq, band, n_fft=256):
    psd, freqs = psd_array_welch(epoch_data, sfreq=sfreq, fmin=band[0], fmax=band[1], n_fft=n_fft)
    return np.mean(psd, axis=-1)

bands = {
    'delta': [0.5, 4],
    'theta': [4, 8],
    'alpha': [8, 13],
    'beta': [13, 30],
    'gamma': [30, 40]
}

sfreq = epochs.info['sfreq']
features = []

for epoch in epochs.get_data():
    epoch_feats = []
    for band_name, band_range in bands.items():
        bp = extract_bandpower(epoch, sfreq, band_range)
        epoch_feats.extend(bp)
    features.append(epoch_feats)

X = np.array(features)
y = epochs.events[:, -1]
```


```python
import pandas as pd

feature_names = []
for band in bands:
    for ch in range(raw.info['nchan']):
        feature_names.append(f'{band}_ch{ch}')

df = pd.DataFrame(X, columns=feature_names)
df['label'] = y
df.head()
```
## Preprocesamiento completo de EEG
Eliminación de artefactos, análisis MNE integrado, extracción de características, ingeniería de características y visualización de PCA

```python
import numpy as np
import mne
from mne.preprocessing import ICA
import pywt
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.preprocessing import StandardScaler
from sklearn.decomposition import PCA
from scipy.stats import kurtosis, skew
```

## 1. Load and preprocess raw EEG

```python
file_path = '/content/S001R03.edf'
raw = mne.io.read_raw_edf(file_path, preload=True)
raw.set_eeg_reference('average')      # average reference
raw.filter(0.5, 40)                   # band-pass 0.5–40 Hz
raw.notch_filter(freqs=60)            # notch at 60 Hz
```
## 2. . Remove artifacts via ICA

```python
ica = ICA(n_components=20, random_state=97, max_iter=800)
ica.fit(raw)
```
### 2a. Remove EOG (blink) if any EOG channel exists
```python
eog_chs = [ch for ch in raw.ch_names if 'EOG' in ch.upper()]
if eog_chs:
    eog_inds, _ = ica.find_bads_eog(raw, ch_name=eog_chs[0])
    ica.exclude = eog_inds
    raw_clean = ica.apply(raw.copy())
else:
    raw_clean = raw.copy()
```
### 2b. Remove muscle artifacts via high-frequency PSD ratio on ICA components
```python
sources = ica.get_sources(raw_clean).get_data()
sf = raw_clean.info['sfreq']
muscle_inds = []
for idx, comp in enumerate(sources):
    psd_high, _  = mne.time_frequency.psd_array_welch(comp, sfreq=sf, fmin=30, fmax=45)
    psd_total, _ = mne.time_frequency.psd_array_welch(comp, sfreq=sf, fmin=1,  fmax=45)
    if psd_high.mean() / psd_total.mean() > 0.5:
        muscle_inds.append(idx)
ica.exclude += muscle_inds
raw_clean = ica.apply(raw_clean.copy())
```
## 3. Integrated MNE-Python analysis
### 3a. Detect bad channels via peak-to-peak criterion

```python
ptp_threshold = 200e-6  # 200 µV, adjust as needed
data_eeg = raw_clean.get_data(picks='eeg')
ptp = np.ptp(data_eeg, axis=1)
bads = [raw_clean.ch_names[i] for i, val in enumerate(ptp) if val > ptp_threshold]
raw_clean.info['bads'] = bads
```
### 3b. Set montage and interpolate bads
```python
montage = mne.channels.make_standard_montage('standard_1020')
raw_clean.set_montage(montage, on_missing='ignore')
try:
    raw_clean.interpolate_bads()
except ValueError:
    print("Warning: skipping bad-channel interpolation (no digitization points)")
```
### 3c. Temporal inspection
```python
raw_clean.plot(n_channels=10, duration=5, title='Cleaned Raw EEG')
```
### 3d. Frequency inspection (PSD)
```python
raw_clean.plot_psd(fmin=1, fmax=50, average=True, picks='eeg')
```
### 3e. Epochs & Evoked
```python
events, event_id_all = mne.events_from_annotations(raw_clean)
event_id = {
    'tarea_mano_derecha': event_id_all.get('T1'),
    'tarea_mano_izquierda': event_id_all.get('T2')
}
epochs = mne.Epochs(raw_clean, events, event_id=event_id,
                    tmin=0, tmax=4, baseline=None, preload=True)
evoked = epochs.average()
evoked.plot(spatial_colors=True, titles='Evoked Response')
```
Safe topomap plotting without digitization

```python
times = np.linspace(0.1, 0.4, 5)
try:
    evoked.plot_topomap(times=times, ch_type='eeg', cmap='RdBu_r', sensors=False)
except Exception as e:
    print(f"Warning: could not plot topomap ({e})")
```
## 4. Prepare for feature extraction
```python
sfreq = epochs.info['sfreq']
```
## 5. Feature extraction: bandpower + DWT
```python
bands = {
    'delta': (0.5, 4),
    'theta': (4,   8),
    'alpha': (8,  13),
    'beta':  (13, 30),
    'gamma': (30, 40)
}

def extract_bandpower(epoch, band):
    psd, _ = mne.time_frequency.psd_array_welch(
        epoch, sfreq=sfreq, fmin=band[0], fmax=band[1], n_fft=256)
    return psd.mean(axis=-1)

def apply_dwt(ch_data):
    cA, cD = pywt.dwt(ch_data, 'db4')
    return cA.mean(), cD.mean()

features_bp = []
features_wt = []
for epoch in epochs.get_data():
    bp_feats = []
    for band in bands.values():
        bp_feats.extend(extract_bandpower(epoch, band))
    features_bp.append(bp_feats)
    wt_feats = []
    for ch in epoch:
        wt_feats.extend(apply_dwt(ch))
    features_wt.append(wt_feats)

X_bp = np.array(features_bp)
X_wt = np.array(features_wt)
X = np.hstack((X_bp, X_wt))
y = epochs.events[:, -1]
```
## 6. Feature engineering: statistics per epoch
```python
def calc_stats(X):
    return {
        'mean':     np.mean(X, axis=1),
        'std':      np.std(X, axis=1),
        'max':      np.max(X, axis=1),
        'min':      np.min(X, axis=1),
        'kurtosis': kurtosis(X, axis=1),
        'skewness': skew(X, axis=1)
    }

stats = calc_stats(X)
df = pd.DataFrame(X, columns=[f'F{i+1}' for i in range(X.shape[1])])
for name, vals in stats.items():
    df[name] = vals
```
## 7. Normalize engineered features
```python
scaler_feat = StandardScaler()
X_norm = scaler_feat.fit_transform(df)
```
## 8. PCA and visualization
```python
pca = PCA(n_components=2)
pc = pca.fit_transform(X_norm)
pca_df = pd.DataFrame(pc, columns=['PC1', 'PC2'])
pca_df['Label'] = y

plt.figure(figsize=(8, 6))
sns.scatterplot(data=pca_df, x='PC1', y='PC2', hue='Label', palette='Set2', s=100)
plt.title('PCA of EEG Features (2 Components)')
plt.xlabel('PC1')
plt.ylabel('PC2')
plt.grid(alpha=0.3)
plt.legend(title='Tarea')
plt.tight_layout()
plt.show()
```
<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%2010%20-%20Procesamiento%20de%20EEG/imagenes/1eeg3.png><p>
  </p>
</div>
<br>
<br>
</p>


<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%2010%20-%20Procesamiento%20de%20EEG/imagenes/1eeg4.png><p>
  </p>
</div>
<br>
<br>
</p>


<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%2010%20-%20Procesamiento%20de%20EEG/imagenes/1eeg5.png><p>
  </p>
</div>
<br>
<br>
</p>


```python
import matplotlib.pyplot as plt
import seaborn as sns

# DataFrame con las estadísticas calculadas para cada epoch
# Asumimos que se llama 'df' y contiene las columnas: mean, std, max, min, kurtosis, skewness
stats_cols = ['mean', 'std', 'max', 'min', 'kurtosis', 'skewness']

# 1. Histogramas con KDE para cada estadístico
plt.figure(figsize=(14, 10))
for i, col in enumerate(stats_cols):
    ax = plt.subplot(2, 3, i + 1)
    sns.histplot(df[col], kde=True, ax=ax)
    ax.set_title(f'Distribución de {col}')
    ax.set_xlabel(col)
plt.tight_layout()
plt.show()

# 2. Boxplot resumen de todos los estadísticos
plt.figure(figsize=(10, 6))
sns.boxplot(data=df[stats_cols])
plt.title('Boxplot de Estadísticas a través de los Epochs')
plt.xlabel('Estadístico')
plt.ylabel('Valor')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```


<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%2010%20-%20Procesamiento%20de%20EEG/imagenes/1eeg6.png><p>
  </p>
</div>
<br>
<br>
</p>


<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%2010%20-%20Procesamiento%20de%20EEG/imagenes/1eeg7.png><p>
  </p>
</div>
<br>
<br>
</p>


<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%2010%20-%20Procesamiento%20de%20EEG/imagenes/1eeg8.png><p>
  </p>
</div>
<br>
<br>
</p>



```python
import matplotlib.pyplot as plt
import seaborn as sns

# Assumes you have:
# - `feature_stats`: a dict with keys 'mean', 'std', 'max', 'min', 'kurtosis', 'skewness'
# - `feature_df`: a DataFrame with your feature columns

# 1. Bar plots for each statistic
plt.figure(figsize=(10, 6))
plt.bar(range(len(feature_stats['mean'])), feature_stats['mean'], color='blue', alpha=0.7)
plt.title('Mean of the Features')
plt.xlabel('Feature Index')
plt.ylabel('Mean')
plt.tight_layout()
plt.show()

plt.figure(figsize=(10, 6))
plt.bar(range(len(feature_stats['std'])), feature_stats['std'], color='green', alpha=0.7)
plt.title('Standard Deviation of the Features')
plt.xlabel('Feature Index')
plt.ylabel('Standard Deviation')
plt.tight_layout()
plt.show()

plt.figure(figsize=(10, 6))
plt.bar(range(len(feature_stats['max'])), feature_stats['max'], color='orange', alpha=0.7)
plt.title('Maximum of the Features')
plt.xlabel('Feature Index')
plt.ylabel('Maximum')
plt.tight_layout()
plt.show()

plt.figure(figsize=(10, 6))
plt.bar(range(len(feature_stats['min'])), feature_stats['min'], color='red', alpha=0.7)
plt.title('Minimum of the Features')
plt.xlabel('Feature Index')
plt.ylabel('Minimum')
plt.tight_layout()
plt.show()

plt.figure(figsize=(10, 6))
plt.bar(range(len(feature_stats['kurtosis'])), feature_stats['kurtosis'], color='purple', alpha=0.7)
plt.title('Kurtosis of the Features')
plt.xlabel('Feature Index')
plt.ylabel('Kurtosis')
plt.tight_layout()
plt.show()

plt.figure(figsize=(10, 6))
plt.bar(range(len(feature_stats['skewness'])), feature_stats['skewness'], color='brown', alpha=0.7)
plt.title('Skewness of the Features')
plt.xlabel('Feature Index')
plt.ylabel('Skewness')
plt.tight_layout()
plt.show()

# 2. Correlation heatmap for the first 10 original features
plt.figure(figsize=(12, 6))
sns.heatmap(feature_df.iloc[:, :10].corr(), annot=True, cmap='coolwarm', linewidths=0.5)
plt.title('Correlation between First 10 Features')
plt.tight_layout()
plt.show()
```

<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%2010%20-%20Procesamiento%20de%20EEG/imagenes/1eeg9.png><p>
  </p>
</div>
<br>
<br>
</p>
<div align="center">

<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%2010%20-%20Procesamiento%20de%20EEG/imagenes/1eeg10.png><p>
  </p>
</div>
<br>
<br>
</p>
<div align="center">

<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%2010%20-%20Procesamiento%20de%20EEG/imagenes/1eeg11.png><p>
  </p>
</div>
<br>
<br>
</p>
<div align="center">

<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%2010%20-%20Procesamiento%20de%20EEG/imagenes/1eeg12.png><p>
  </p>
</div>
<br>
<br>
</p>
<div align="center">

<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%2010%20-%20Procesamiento%20de%20EEG/imagenes/1eeg13.png><p>
  </p>
</div>
<br>
<br>
</p>
<div align="center">

<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%2010%20-%20Procesamiento%20de%20EEG/imagenes/1eeg14.png><p>
  </p>
</div>
<br>
<br>
</p>
<div align="center">

<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%2010%20-%20Procesamiento%20de%20EEG/imagenes/1eeg15.png><p>
  </p>
</div>
<br>
<br>
</p>
<div align="center">

