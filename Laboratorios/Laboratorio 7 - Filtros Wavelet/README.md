# LABORATORIO 7: Filtros Wavelet

## **Tabla de contenidos:**
<div style="border: 2px solid gray; padding: 20px;border-radius: 15px; width: 40%; height: 180px;">

1. [**Transformada Wavelet aplicada a señales ECG**](#1-introducción)  
2. [**Transformada Wavelet aplicada a señales EEG**](#2-proposito-de-la-práctica)
3. [**Transformada Wavelet aplicada a señales EMG**](#3-materiales-y-metodos)
4. [**Bibliografía**](#4-bibliografia)

</div>
<br>

## **1) Transformada Wavelet aplicada a señales ECG**

### 1.1) ECG Feature Extraction Using Optimal Mother Wavelet [1]

Transformada usada: Transformada Wavelet Discreta (DWT)

- En el estudio se porpone un método automatizado para seleccionar la "wavelet madre óptima", con el objetivo de mejorar la extracción de características en señales ECG.
- Este algoritmo se basó en la correlación entre la wavelet y la señal ECG. Se trato de maximizar la similitud morfológica ya existente para mejorar la representación de los ciclos "PQRST".
- Se resalta que la DWT permitió identificar con precisión complejos QRS, ondas P y T, a pesar de que se tuvieron condiciones en las que la señal presentaba ruido.
- Se aplicó una estrategia que se enfocaba en la descomposición de multiresolución para separar los diferentes componentes de la señal y así poder analizarlas en distintas frecuencia.
- Las características extraídas fueron usadas posteriormente para detección de arritmias o clasificación de latidos cardíacos, demostrando un rendimiento superior frente a otras funciones wavelet no optimizadas.
  
**Conclusión:** El uso de una wavelet madre seleccionada óptimamente mejora considerablemente la precisión en la detección de eventos cardíacos y la calidad de las características extraídas, haciendo de la DWT una herramienta eficaz en el análisis clínico de ECG. [1]

## **2) Transformada Wavelet aplicada a señales EEG [2]**

Transformadas utilizadas: Daubechies, Symlets y Coiflets

**Impacto principal:**
- En el estudio, se realiza una comparación de 45 funciones MWT y se evalúa las principales características (entre las más resaltantes Daubechies, Symlets y Coiflets), además también se comparan familias de wavelets ortogonales que son reconocidas en el área de procesamiento de señales biomédicas, utilizando métodos como correlación cruzada y ANOVA para determinar la compatibilidad con señales EEG adquiridas durante la realización de tareas que requieren trabajo de la memoria.
- El objetivo de este estudio es identificar la MWT óptima con un enfoque en la eliminación de ruido, descomposición, reconstrucción de componentes y extracción de características de una señal.
- Así mismo, la eficacia de cada MWT se evaluó mediante el coeficiente de correlación cruzada (XCorr) entre la señal EEG filtrada por bandas de interés (X) y la señal denoised reconstruida (Y), con el objetivo de medir el grado de similitud entre ambas.
- El análisis de compatibilidad mostró como resultados que la wavelet “sym9”, de la familia Symlets, mostró una mayor similitud y compatibilidad con las señales EEG registradas en cinco regiones del cuero cabelludo y también se obtuvieron resultados notables con “coif3” (Coiflets) y “db7” (Daubechies).

**Conclusión:** La selección óptima de la MWT debe basarse en los valores más altos de XCorr, y este enfoque resulta útil no solo para mejorar el procesamiento de señales EEG, sino también como herramienta complementaria para el diagnóstico clínico basado en señales EEG.


## **3)Transformada Wavelet aplicada a señales EMG**

### 3.1) Wavelet Analysis of the EMG Signal to Assess Muscle Fatigue [3]

Transformada usada: Transformada Wavelet Discreta (DWT)

- La DWT permitió detectar cambios en la fatiga muscular en ejercicios dinámicos como el uso de un ergómetro de remo.
- Se utilizó para calcular frecuencias medias (MNF) y medianas (MDF), donde se encontró que la mayoría de los músculos mostraban coeficientes de regresión negativos (indicadores de fatiga), con mayor consistencia que el STFT.
- Ofrece mejor resolución temporal y frecuencial que FFT y STFT en señales EMG no estacionarias.
- Fue efectiva para reconstruir señales EMG y extraer componentes de fatiga, validando su uso como herramienta de análisis en actividades cíclicas dinámicas.

**Conclusión:** La DWT es precisa para evaluar fatiga muscular y superior a métodos tradicionales en análisis dinámicos de EMG.[3]

### 3.2) Wavelet-Based Assessment of the Muscle-Activation Frequency Range by EMG Analysis [4]

Transformada usada: Transformada Wavelet Continua (CWT)

- Desarrollaron un algoritmo adaptativo basado en CWT para detectar activaciones musculares en el dominio tiempo-frecuencia.
- Permite identificar con precisión el inicio, fin y el rango de frecuencia de cada activación muscular, incluso con señales EMG ruidosas (bajo SNR).
- Demostró alta exactitud (MAE ≈ 10–30 ms), y la capacidad de detectar la variabilidad intra e intermuscular en frecuencias de activación (100–500 Hz).
- Mejora la fiabilidad del análisis EMG en condiciones reales como caminatas o tareas prolongadas, útil para interfaces humano-máquina y rehabilitación.

**Conclusión**: La CWT mejora significativamente la robustez y profundidad del análisis de señales EMG en tiempo y frecuencia, sobre todo en entornos clínicos y robóticos.[4]

### 3.3) Application of Wavelet Analysis in EMG Feature Extraction for Pattern Classification [5]

Transformada usada: Transformada Wavelet Discreta (DWT)

- La trasformada aplicada fue la DWT, con el objetivo de extraer las características principales de señales EMG, para esto se eliminó ruido y las partes no deseadas usando descomposición multiresolución.
- Las características extraídas de los niveles principales (primer y segundo nivel) mostraron como resultado una mejora de la separabilidad entre clases en tareas de clasificación de movimientos.
- Las señales reconstruidas a partir de componentes wavelet seleccionados mostraron mejor rendimiento en la clasificación de patrones, esto se comporbó por una evaluación por métricas estadísticas.
- Esta trasformada ermite una extracción eficiente de características (MAV y RMS) con diversos beneficios como reducción de dimensionalidad y mejora en la precisión de clasificación.

**Conclusión**: DWT facilita una extracción de características más efectiva para sistemas de reconocimiento de patrones EMG, aumentando la precisión y eficiencia del análisis.[5]

## **4) Bibliografía**
[1] S. K. Chaudhary, R. Pachori, and R. Kumar, “ECG feature extraction using optimal mother wavelet,” International Journal of Medical Informatics, 2005. [Online]. Available: https://www.researchgate.net/publication/3897917_ECG_feature_extraction_using_optimal_mother_wavelet

[2] N. K. Al-Qazzaz, S. H. Bin Mohd Ali, S. A. Ahmad, M. S. Islam, y J. Escudero, “Selection of mother wavelet functions for multi-channel EEG signal analysis during a working memory task”, Sensors (Basel), vol. 15, núm. 11, pp. 29015–29035, 2015.

[3] N. Daniel and J. Małachowski, "Wavelet analysis of the EMG signal to assess muscle fatigue in the lower extremities during symmetric movement on a rowing ergometer," Acta of Bioengineering and Biomechanics, vol. 25, no. 2, 2023. DOI: 10.37190/ABB-02282-2023-01.

[4] F. Di Nardo, T. Basili, S. Meletani, and D. Scaradozzi, "Wavelet-Based Assessment of the Muscle-Activation Frequency Range by EMG Analysis," IEEE Access, vol. 10, pp. 9793–9806, Jan. 2022. DOI: 10.1109/ACCESS.2022.3141162.

[5] A. Phinyomark, C. Limsakul, and P. Phukpattaranont, "Application of Wavelet Analysis in EMG Feature Extraction for Pattern Classification," Measurement Science Review, vol. 11, no. 2, pp. 45–52, 2011. DOI: 10.2478/v10048-011-0009-y
