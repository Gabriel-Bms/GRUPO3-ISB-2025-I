# Laboratorio 2 - Setup para proyectos
## Instalar un gestor de paquetes (conda, PIP)
### 1. En este caso, se utilizara Anaconda, que incluye el gestor de paquetes conda y un entorno predeterminado "base", con multiples librerias preinstaladas
### 2. Crear un entorno virtual especifico para los proyectos a desarrollar en el curso, definir la version de Python a usar
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio 02 - Setup para proyectos/Imagenes/Lab2-CrearVenv.png">


### 3. Para modigicar el entorno creado, activamos el entorno
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio 02 - Setup para proyectos/Imagenes/Lab2-ActivarVenv.png">
  
### 4. Verificar que el entorno se creo correctamente
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio 02 - Setup para proyectos/Imagenes/Lab2-VerificarVenv.png">
  
### 5. Instalar las librerias básicas para análisis, procesado y visualización de datos en el entorno creado
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio 02 - Setup para proyectos/Imagenes/Lab2-InstalarLibrerias.png">



### 6. Escoger el IDE, Anaconda incluye Jupyer Notebook, Jupyter Lab y Spyder, tambien es compatible con VSCode, en este caso usaremos Jupyter Notebook
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio 02 - Setup para proyectos/Imagenes/Lab2-InstalarJupyter.png">

### 7. Abrimos Jupyter desde el Conda Prompt
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio 02 - Setup para proyectos/Imagenes/Lab2-AbrirJupyter.png">

### 8. Creamos el primer cuaderno ipynb
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio 02 - Setup para proyectos/Imagenes/Lab2-CrearIpynb.png">

## Código para plotear 2 señales EMG y 2 señales ECG simuladas

### 1. Importamos las librerías necesarias para el análisis como numpy, pandas, scipy, sklearn y el neurokit2 para la simulación de señales. Además, verificamos las versiones de las librerías y que nos encontremos en el entorno virtual correcto.
```python
import numpy as np                                 # Verificar versiones de las librerias
import neurokit2 as nk
import pandas as pd
import scipy
import sklearn
import matplotlib
import seaborn as sns
# Verificar versiones
print("NumPy version:", np.__version__)
print("Pandas version:", pd.__version__)
print("SciPy version:", scipy.__version__)
print("Scikit-learn version:", sklearn.__version__)
print("Matplotlib version:", matplotlib.__version__)
print("Seaborn version:", sns.__version__)
print("NeuroKit2 version:", nk.__version__)
```
```text
NumPy version: 2.2.4
Pandas version: 2.2.3
SciPy version: 1.15.2
Scikit-learn version: 1.6.1
Matplotlib version: 3.10.0
Seaborn version: 0.13.2
NeuroKit2 version: 0.2.10
```

### 2. Importamos la librería matplotlib.pyplot para graficar las señales y la función welch para el cálculo del PSD
```python
import matplotlib.pyplot as plt
from scipy.signal import welch
```
  
### 3. Definimos los parámetros de frecuencia de muestreo y duración
```python
sampling_rate = 1000  # Hz
duration = 10  # segundos
length = duration * sampling_rate
```
  
### 3. Simulación de la primera señal EMG: Generamos 7 explosiones de actividad muscular con duraciones aleatorias entre 0.1 y 0.5 segundos.
```python
burst_durations1 = np.random.uniform(0.1, 0.5, size=7)                  
emg1 = nk.emg_simulate(duration=duration, sampling_rate=sampling_rate, 
                       burst_number=7, burst_duration=burst_durations1,
                       noise=0.4)
```

### 4. Simulación de la segunda señal EMG: Generamos 3 explosiones de actividad muscular con duraciones aleatorias entre 0.2 y 0.6 segundos.
```python
burst_durations2 = np.random.uniform(0.2, 0.6, size=3)                   
emg2 = nk.emg_simulate(duration=duration, sampling_rate=sampling_rate,   
                       burst_number=3, burst_duration=burst_durations2,
                       noise=0.1)
```

### 5. Simulación de las dos señales ECG: La pimera con frecuencia cardíaca de 60 bpm y la segunda con 90 bpm y se les añadió un ruido de 0.01 y 0.05 respectivamente 
```python
ecg1 = nk.ecg_simulate(duration=duration, sampling_rate=sampling_rate, 
                       heart_rate=60, method="ecgsyn", noise=0.01)
ecg2 = nk.ecg_simulate(duration=duration, sampling_rate=sampling_rate, 
                       heart_rate=90, method="ecgsyn", noise=0.05)
```

### 6. Creación de un vector tiempo para graficar las cuatro señales, dos EMG y dos ECG, como subplots separados. Se utilizó colores distintos para identificar cada señal, se añadió títulos y etiquetas a los ejes.
```python
time = np.linspace(0, duration, length)
plt.figure(figsize=(15, 10))

plt.subplot(4, 2, 1);plt.plot(time, emg1, color='purple')
plt.title("EMG 1 - Dominio del tiempo");plt.xlabel("Tiempo (s)");plt.ylabel("Amplitud")

plt.subplot(4, 2, 3);plt.plot(time, emg2, color='green')
plt.title("EMG 2 - Dominio del tiempo");plt.xlabel("Tiempo (s)");plt.ylabel("Amplitud")

plt.subplot(4, 2, 5);plt.plot(time, ecg1, color='blue')
plt.title("ECG 1 - Dominio del tiempo");plt.xlabel("Tiempo (s)");plt.ylabel("Amplitud")


plt.subplot(4, 2, 7);plt.plot(time, ecg2, color='red')
plt.title("ECG 2 - Dominio del tiempo");plt.xlabel("Tiempo (s)");plt.ylabel("Amplitud")
```
  
### 7. Definición de la función plot_psd que calcula la densidad espectral de potencia (PSD). Posteriormente, se grafica cada señal en dominio de frecuencia, separando en subplots que permiten observar la distribución de energía en distintas bandas de frecuencia. Finalmente, se usa plt.tight_layout() para ordenar las gráficas y plt.show() para mostrarlas.
```python
def plot_psd(signal, sr, title, color, subplot_index):
    freqs, psd = welch(signal, fs=sr, nperseg=2048)
    plt.subplot(4, 2, subplot_index)
    plt.semilogy(freqs, psd, color=color)
    plt.title(title)
    plt.xlabel("Frecuencia (Hz)")
    plt.ylabel("PSD (V²/Hz)")
plot_psd(emg1, sampling_rate, "EMG 1 - Dominio de frecuencia", 'purple', 2)
plot_psd(emg2, sampling_rate, "EMG 2 - Dominio de frecuencia", 'green', 4)
plot_psd(ecg1, sampling_rate, "ECG 1 - Dominio de frecuencia", 'blue', 6)
plot_psd(ecg2, sampling_rate, "ECG 2 - Dominio de frecuencia", 'red', 8)

plt.tight_layout()
plt.show()
```
### 8. Gráficas de las señales EMG en el dominio de tiempo y frecuencia
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio 2 - Setup para proyectos/Imagenes/10.png">

### 9. Gráficas de las señales ECG en el dominio de tiempo y frecuencia
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio 2 - Setup para proyectos/Imagenes/11.png">
