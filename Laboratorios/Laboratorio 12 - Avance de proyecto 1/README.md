# Avance de Proyecto 1: Analisis Exploratorio de Data y Pre Procesamiento

## 1. Introducción

La interfaz cerebro-computadora (BCI, por sus siglas en inglés) es una tecnología que permite la interacción directa entre el cerebro y un dispositivo externo sin la participación de ningún componente muscular. Esta comunicación se logra mediante el registro y análisis de señales eléctricas cerebrales, principalmente a través de electroencefalografía (EEG), con gran potencial de aplicación en personas con discapacidades motoras severas como la esclerosis lateral amiotrófica (ELA) o parálisis, así como en procesos de neurorehabilitación [1] [2]. Dentro de este campo, el P300 Speller es un tipo específico de BCI diseñado para facilitar la comunicación mediante el pensamiento. Este sistema se basa en la detección del potencial evocado P300, una señal cerebral positiva que aparece aproximadamente 300 milisegundos después de que el usuario reconoce un estímulo relevante. Para ello, se utiliza el paradigma oddball visual, en el que se presenta una matriz de caracteres cuyos elementos (filas y columnas) se iluminan de forma pseudoaleatoria, generando respuestas cerebrales diferenciales al estímulo objetivo. Estas señales EEG, que contienen información espectral útil, son procesadas y clasificadas posteriormente mediante algoritmos como redes neuronales. Sin embargo, estos sistemas enfrentan limitaciones importantes, como la velocidad de escritura lenta, la fatiga cognitiva y la necesidad de atención sostenida [3]. Ante estos desafíos, el uso de modelos de deep learning representa una alternativa prometedora para mejorar la detección de la señal P300, aumentando la precisión y la eficiencia del sistema en contextos clínicos y de asistencia personalizada. Por ello, en el presente trabajo se propone el diseño e implementación de un modelo de deep learning orientado a mejorar la detección de la señal P300 en un sistema BCI tipo Speller, con el objetivo de incrementar la precisión, reducir la latencia de respuesta y facilitar su aplicación en entornos clínicos reales.


## 2. Metodología y Resultados

### 2.1 Dataset

### **Dataset General:** bigP3BCI: An Open, Diverse and Machine Learning Ready P300-based Brain-Computer Interface Dataset [4]

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

**Datos extraídos:**
- Señales crudas de EEG.
- Eventos del codificador BCI ( P300).
- Caracteres objetivo y retroalimentación visual del speller.
- Datos de seguimiento ocular (coordenadas, diámetro de pupila).
- Información demográfica del sujeto (edad, sexo, raza/etnia).
- Diagnóstico médico (presencia o no de esclerosis lateral amiotrófica(ELA)) y puntuaciones funcionales (ALSFRS-R).

### **Dataset:** Online Evaluation of Dynamic Stopping Algorithms for the P300 Speller in People with ALS [5]

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

Las imágenes muestran la media de las señales EEG por sujeto, comparando los resultados sin filtrar y posterior al filtrado.
Se comparan las respuestas a estímulos Target (línea verde) y Non-Target (línea azul) a lo largo del tiempo.
Target: Refiere a los estímulos visuales (flash de caracteres o grupos de caracteres en la matriz del speller) en los que el usuario está concentrando su atención porque corresponde al carácter que desea escribir.
Non ‑Target: son los estímulos que se presentan pero que no coinciden con el carácter objetivo; el usuario no los está observando intencionalmente

La componente P300 se caracteriza por ser una deflexión positiva en el potencial eléctrico del EEG que ocurre aproximadamente entre los 0 y 800 milisegundos después de la presentación de un estímulo relevante o inesperado (Target). Esta deflexión positiva significa que, en esa ventana temporal se observa un aumento en la amplitud de la señal eléctrica hacia valores positivos respecto a la línea base, principalmente en electrodos centro parietales (como Pz y Cz). 

En diversos sujetos, se observa una clara diferencia entre Target y Non-Target, por ejemplo, en los 2 primeros sujetos de la parte superior. Para explicar esta diferencia cabe resaltar que el filtrado permite resaltar la componente P300 en canales relevantes como Cz y Pz, donde se evidencia una amplitud positiva entre 0 - 800 ms post estímulo.

Por otro lado, en las señales sin filtrar, la distinción entre Target y Non -Target es menos clara debido al ruido presente en las señales, lo que justifica la aplicación de preprocesamiento en etapas posteriores.

Así mismo, existe una variabilidad intersujeto: algunos presentan P300 más marcada, mientras que en otros es difícil de distinguir, esto es esperado en señales EEG reales debido a factores como diferencias anatómicas, atención del sujeto o ruido externo.


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


## Referencias
[1] A. Mostafa, Y. Ma, Y. Liu, M. Aly, and G. Chen, “Deep Learning-Based EEG Classification for P300 Detection in Brain–Computer Interface Applications,” Applied Sciences, vol. 14, no. 14, art. 6347, Jul. 2024. [Online]. Available: https://www.mdpi.com/2076-3417/14/14/6347

[2] R. Sharma and R. B. Pachori, “A review on hybrid brain–computer interface systems,” Brain Informatics, vol. 9, no. 1, p. 3, Dec. 2022. [Online]. Available: https://pmc.ncbi.nlm.nih.gov/articles/PMC9774292/

[3] A. Kübler, B. Kotchoubey, J. Kaiser, J. Wolpaw, and N. Birbaumer, “Brain–computer communication: unlocking the locked in,” Psychological Bulletin, vol. 127, no. 3, pp. 358–375, 2001. [Online]. Available: https://pmc.ncbi.nlm.nih.gov/articles/PMC3432970/

[4] B. Mainsah, C. Fleeting, T. Balmat, E. Sellers, and L. Collins, “bigP3BCI: Un conjunto de datos de interfaz cerebro-computadora basado en P300 abierto, diverso y listo para el aprendizaje automático (versión 1.0.0),” PhysioNet, 2025. [Online]. Available: https://doi.org/10.13026/0byy-ry86

[5] B. O. Mainsah, L. M. Collins, K. A. Colwell, E. W. Sellers, D. B. Ryan, K. Caves, y C. S. Throckmorton, “Increasing BCI communication rates with dynamic stopping towards more practical use: an ALS study,” Journal of Neural Engineering, vol. 12, n.º 1, p. 016013, 14 ene. 2015. doi: 10.1088/1741-2560/12/1/016013
