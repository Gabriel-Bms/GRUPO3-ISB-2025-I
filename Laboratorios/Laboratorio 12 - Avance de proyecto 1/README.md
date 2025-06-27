# Avance de Proyecto 1: Analisis Exploratorio de Data y Pre Procesamiento

## 1. Introducción

## 2. Metodología y Resultados

### 2.1 Analisis Exploratorio de Datos
| Mean P300 of all subjects filtered | Mean P300 of all subjects Non filtered |
|:----------------------------------:|:--------------------------------------:|
| ![Filtered](https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%2012%20-%20Avance%20de%20proyecto%201/Imagenes/P300%20Mean%20F.png?raw=true) | ![NonFiltered](https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%2012%20-%20Avance%20de%20proyecto%201/Imagenes/P300%20Mean%20NF.png?raw=true) |

### 2.2 Pre Procesamiento
'''python
def obtener_epochs_target(sujeto_id, canal_eeg, fs=256, base_path="./StudyF"):
    """
    Carga todos los archivos de entrenamiento de un sujeto, encuentra los eventos 
    StimulusType == 1 y StimulusBegin == 1, y extrae las ventanas EEG alrededor 
    de esos eventos.

    Args:
        sujeto_id (str): ID del sujeto (e.g., 'F_03')
        canal_eeg (str): Nombre del canal EEG a usar (e.g., 'EEG_Pz')
        fs (int): Frecuencia de muestreo (Hz). Por defecto 256.
        base_path (str): Ruta base donde están los datos EDF

    Returns:
        epochs_target (np.ndarray): Matriz de epocas shape (n_eventos, muestras)
    """
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
'''
La función obtener_epochs_target carga los archivos EEG de entrenamiento de un sujeto específico y extrae segmentos de señal (épocas) alrededor de eventos visuales relevantes (flashes), definidos por el inicio de un estímulo (StimulusBegin == 1000000.0). Utiliza un canal EEG específico y una frecuencia de muestreo dada (por defecto 256 Hz) para identificar los momentos donde comienzan estos estímulos y extrae una ventana de 0.8 segundos desde cada evento. Luego clasifica las épocas en dos grupos: target (si el evento también corresponde a un StimulusType == 1000000.0) y non-target (si no), retornando ambos conjuntos como matrices NumPy. Esta función es útil para preparar los datos de entrada en aplicaciones de BCI como el P300 speller.
|                                                                                           |
|-------------------------------------------------------------------------------------------|
| Segmento de la señal EEG filtrada, con los segmentos del potencial relacionado a eventos P300 resaltados en azul |
| ![Epoch F](https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%2012%20-%20Avance%20de%20proyecto%201/Imagenes/Epoch%20F.png) |
| Segmento de la señal EEG no filtrada, con los segmentos del potencial relacionado a eventos P300 resaltados en azul |
| ![Epoch NF](https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%2012%20-%20Avance%20de%20proyecto%201/Imagenes/Epoching%20NF.png) |


## 3. Conclusiones

