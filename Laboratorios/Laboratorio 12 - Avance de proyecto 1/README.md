# Avance de Proyecto 1: Analisis Exploratorio de Data y Pre Procesamiento

## 1. Introducción

## 2. Metodología y Resultados

### 2.1 Dataset

####**Dataset General:** bigP3BCI: An Open, Diverse and Machine Learning Ready P300-based Brain-Computer Interface Dataset

**Fuente:** PhysioNet

**Objetivo:** Este dataset fue desarrollado para estudiar sistemas híbridos de interfaz cerebro-computadora (BCI), combinando señales EEG con datos de seguimiento ocular durante el uso de un speller BCI basado en P300.

**Adquisición de datos:**
- Sistema utilizado: Plataforma BCI2000 
- Dispositivo EEG: Amplificadores de bioseñales de g.tec medical engineering GmbH.
- Electrodos: Pasivos con gel y activos secos.
- Frecuencia de muestreo: 256 Hz.
- Filtros: Paso de banda y notch 
- Frecuencia de muestreo del eye tracker: 30 Hz.
- Dispositivo para seguimiento ocular: Tobii Pro X2-30
- Sincronización: Señales EEG y datos de seguimiento ocular sincronizados a través de BCI2000.

**Datos extraídos: **
- Señales crudas de EEG.
- Eventos del codificador BCI ( P300).
- Caracteres objetivo y retroalimentación visual del speller.
- Datos de seguimiento ocular (coordenadas, diámetro de pupila).
- Información demográfica del sujeto (edad, sexo, raza/etnia).
- Diagnóstico médico (presencia o no de esclerosis lateral amiotrófica(ELA)) y puntuaciones funcionales (ALSFRS-R).

####**Dataset:** Online Evaluation of Dynamic Stopping Algorithms for the P300 Speller in People with ALS

**Fuente:**  PMC PubMed

**Objetivo:** Evaluar algoritmos adaptativos de recolección de datos (dynamic stopping (DS) y dynamic stopping with language model (DSLM)) para mejorar la velocidad y precisión de un deletreador P300 en participantes con esclerosis lateral amiotrófica (ELA). 

**Adquisición de datos:**
- Fases:
    Entrenamiento: 3 palabras de 6 letras.
    Prueba: 2 palabras por algoritmo (static, DS y DSLM).
- Total de caracteres evaluados por algoritmo: 36 por participante.
- Software de adquisición de señales EEG: BCI2000 
- Dispositivo: Gorros de 32 y 16 canales
- Frecuencia de muestreo: 256 Hz.
- Canales usados para procesamiento: Fz, Cz, P3, Pz, P4, PO7, PO8, Oz.


### 2.2 Analisis Exploratorio de Datos
En la etapa de análisis exploratorio de datos buscamos, entre otras cosas, visualizar patrones generales en la señal EEG, como la presencia y latencia del componente P300; identificar los canales más representativos y distinguir la forma de onda entre condiciones (por ejemplo, estímulos target vs non-target); así como detectar posibles anomalías, ruido excesivo o sujetos que no presenten una respuesta clara. Este análisis inicial también funciona como un paso diagnóstico previo a la aplicación de modelos más complejos. Por ello, consideramos que la mejor forma de representar visualmente esta información es mediante la gráfica de la media de los potenciales evocados por sujeto, ya que resalta de forma clara y robusta la respuesta neuronal típica, facilitando su interpretación y comparación.

```python
def plot_erps_by_channel(channel):
    sujetos_ordenados = ['F_05', 'F_06', 'F_07', 'F_08', 'F_03', 
                        'F_20', 'F_21', 'F_23', 'F_24', 'F_25']
    datos = {}
    for sujeto in sujetos_ordenados:
        var_t = f'epochs_{sujeto.lower()}_{channel.lower()}_method1_t'
        var_nt = f'epochs_{sujeto.lower()}_{channel.lower()}_method1_nt'
        epochs_t, epochs_nt = obtener_epochs_target(sujeto, channel)
        datos[sujeto] = (epochs_t, epochs_nt)
    times = np.linspace(0, 0.8, 204)
    plt.figure(figsize=(11, 10))
    for i, (sujeto, (epochs_t, epochs_nt)) in enumerate(datos.items(), start=1):
        plt.subplot(5, 2, i)
        plt.plot(times, epochs_t.mean(axis=0), label='Target', color='green')
        plt.plot(times, epochs_nt.mean(axis=0), label='Non-Target', color='blue')
        plt.ylabel(sujeto.replace('_', ''))  # Mostrar F03 en vez de F_03
        plt.grid(True)
        plt.xlim([0, 0.8])
        if i == 1:
            plt.legend(loc='upper right')
    plt.suptitle(f'ERPs en canal {channel}', y=1.02)
    plt.tight_layout()
    plt.show()
```

    
| Mean P300 of all subjects filtered | Mean P300 of all subjects Non filtered |
|:----------------------------------:|:--------------------------------------:|
| ![Filtered](https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%2012%20-%20Avance%20de%20proyecto%201/Imagenes/P300%20Mean%20F.png?raw=true) | ![NonFiltered](https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%2012%20-%20Avance%20de%20proyecto%201/Imagenes/P300%20Mean%20NF.png?raw=true) |

### 2.3 Filtrado de la señal EEG
El filtro Butterworth pasabanda es ideal para señales EEG porque permite conservar las frecuencias relevantes, mientras atenúa el ruido de baja frecuencia (artefactos de movimiento, drift) y de alta frecuencia (ruido muscular, interferencia eléctrica). Además, su respuesta en frecuencia es suave y sin distorsiones dentro de la banda, y al aplicarse con filtfilt, se logra un filtrado sin desplazamiento de fase, lo cual es crucial para mantener la forma y latencia original de los potenciales evocados.

```python
def butter_bandpass_filter(data, lowcut, highcut, fs, order=4):
    nyq = 0.5 * fs
    low = lowcut / nyq
    high = highcut / nyq
    b, a = butter(order, [low, high], btype='band')
    y = filtfilt(b, a, data)
    return y
```

Se aplica a las señales EEG del dataset, con la siguiente función:
```python
def cargar_edf_sujeto(sujeto_id, archivos_train):
    archivos_sujeto = [f for f in archivos_train if os.path.basename(f).startswith(sujeto_id)]
    if not archivos_sujeto:
        raise ValueError(f"No se encontraron archivos EDF para el sujeto {sujeto_id}")
    dfs = []
    raw_info = None
    for i, archivo in enumerate(sorted(archivos_sujeto)):
        raw = mne.io.read_raw_edf(archivo, preload=True, verbose=False)
        fs = raw.info['sfreq']  # frecuencia de muestreo
        df = raw.to_data_frame()
        # Definir bandas según sujeto
        if sujeto_id in ["F_05", "F_06", "F_07", "F_08"]:
            lowcut, highcut = 0.1, 30
        else:
            lowcut, highcut = 0.5, 30
        # Aplicar filtro solo a columnas EEG
        eeg_cols = [col for col in df.columns if col.startswith('EEG_')]
        for col in eeg_cols:
            df[col] = butter_bandpass_filter(df[col].values, lowcut, highcut, fs)
        dfs.append(df)
        if raw_info is None:
            raw_info = raw.info  # Guardamos solo una vez la info del sampling
    
    df_concatenado = pd.concat(dfs, ignore_index=True)
    return df_concatenado, raw_info
```


### 2.4 Pre Procesamiento

```python
def obtener_epochs_target(sujeto_id, canal_eeg, fs=256, base_path="./StudyF"):
    # Paso 1: Obtener archivos del sujeto
    archivos = listar_archivos_train(base_path)
    df, raw_info = cargar_edf_sujeto(sujeto_id, archivos)

    # Paso 2: Detectar eventos relevantes
    stim_type = (df['StimulusType'].to_numpy() == 1000000.0)
    stim_begin = (df['StimulusBegin'].to_numpy() == 1000000.0)
    joint_signal = stim_begin  # Consideramos todos los flashes como candidatos (v2)
    #joint_signal = stim_type & stim_begin (v1)
    edges = np.diff(joint_signal.astype(int), prepend=0)
    event_indices = np.where(edges == 1)[0]

    # Paso 3: Epocamiento
    eeg_data = df[canal_eeg].values
    pre = 0
    post = int(0.8 * fs)
    epoch_len = pre + post

    epochs_target = []
    epochs_nontarget = []
    
    for t in event_indices:
        if t - pre >= 0 and t + post < len(eeg_data):
            epoch = eeg_data[t - pre : t + post]
            if stim_type[t]:  # target
                epochs_target.append(epoch)
            else:             # non-target
                epochs_nontarget.append(epoch)

    return np.array(epochs_target), np.array(epochs_nontarget)
```
La función obtener_epochs_target carga los archivos EEG de entrenamiento de un sujeto específico y extrae segmentos de señal (épocas) alrededor de eventos visuales relevantes (flashes), definidos por el inicio de un estímulo (StimulusBegin == 1000000.0). Utiliza un canal EEG específico y una frecuencia de muestreo dada (por defecto 256 Hz) para identificar los momentos donde comienzan estos estímulos y extrae una ventana de 0.8 segundos desde cada evento. Luego clasifica las épocas en dos grupos: target (si el evento también corresponde a un StimulusType == 1000000.0) y non-target (si no), retornando ambos conjuntos como matrices NumPy. Esta función es útil para preparar los datos de entrada en aplicaciones de BCI como el P300 speller.
|                                                                                           |
|-------------------------------------------------------------------------------------------|
| Segmento de la señal EEG filtrada, con los segmentos del potencial relacionado a eventos P300 resaltados en azul |
| ![Epoch F](https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%2012%20-%20Avance%20de%20proyecto%201/Imagenes/Epoch%20F.png) |
| Segmento de la señal EEG no filtrada, con los segmentos del potencial relacionado a eventos P300 resaltados en azul |
| ![Epoch NF](https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%2012%20-%20Avance%20de%20proyecto%201/Imagenes/Epoching%20NF.png) |



