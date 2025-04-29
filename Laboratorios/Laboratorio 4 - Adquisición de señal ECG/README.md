# LABORATORIO 5: Uso de Bitalino para ECG

## **Tabla de contenidos:**
<div style="border: 2px solid gray; padding: 20px;border-radius: 15px; width: 40%; height: 180px;">

1. [**Introducción**](#1-introducción)  
2. [**Propósito de la práctica**](#2-propósito-de-la-práctica)
3. [**Materiales y equipos**](#3-materiales-y-equipos)
4. [**Procedimiento**](#4-procedimiento)
5. [**Resultados**](#5-resultados)
6. [**Conclusiones**](#6-conclusiones)
7. [**Referencias**](#7-referencias)
</div>
<!--  El uso del Padding es para controlar el espacio entre contenido y borde -->
<br>

## **1) Introducción** 
<p align="justify">
El uso de sistemas de adquisición de señales es ampliamente utilizado para la monitorización y el análisis de diversas señales fisiológicas. El electrocardiograma (ECG) es una herramienta utilizada para registrar la actividad eléctrica del corazón, participa en el diagnóstico de trastornos cardíacos como arritmias, infartos y enfermedades relacionadas. Estas enfermedades pueden identificarse analizando las distintas ondas que posee un ECG: la onda P, que refleja la despolarización de las aurículas; el complejo QRS, que indica la despolarización de los ventrículos, y la onda T, que representa la repolarización ventricular. Las variaciones en estas ondas pueden indicar diversas condiciones del corazón. Por ejemplo, un complejo QRS más ancho de lo esperado puede ser indicativo de un engrosamiento ventricular, lo cual es común en enfermedades como la hipertrofia ventricular [1]. 
</p>
<div align="center">
  <img src="./fig1.png" alt="EKG" width="350"><p>

  **Figura 1: Electrocardiograma con sus ondas e intervalos**
  </p>
</div>
<br>
<p align ="justify">
La monitorización de esta señal es posible mediante dispositivos portátiles como el Bitalino, un sistema flexible y accesible que permite la captura de diferentes señales biomédicas [2]. El dispositivo Bitalino, es una plataforma accesible para capturar señales biomédicas, incluyendo el ECG. A través del Bitalino, es posible obtener representaciones gráficas detalladas de las ondas cardíacas, lo que facilita la monitorización de la salud cardiovascular en tiempo real [3].

El ECG se obtiene utilizando derivadas específicas que permiten observar la señal desde diferentes ángulos. Las derivadas bipolares (como DI, DII, DIII) ofrecen vistas del corazón desde el plano frontal, mientras que las derivadas precordiales (como V1 a V6) proporcionan una visión más detallada desde el plano horizontal. Las derivadas unipolares (como aVR, aVL, aVF) permiten una mayor sensibilidad en el análisis de la actividad eléctrica del corazón [4].
</p> 

<div align="center">
   <img src="./fig2.png" alt="Derivaciones" width="350">

**Figura 2: Derivaciones del ECG**  

</div>



<br>

# 2) Propósito de la práctica

### 2.1) Objetivos 

- Realizar una correcta configuración de BiTalino y conectarlo al software OpenSignals para la adquisición de las  señales biomédicas de electrocardiografía (ECG).
- Adquirir y extraer la información de las señales  ECG del software OpenSignals (r)evolution para procesarlas posteriormente. 
- Realizar el análisis de las señales ECG mediante su visualización gráfica. 

### 2.2) Justificación de la práctica: 

El presente análisis de señales ECG tiene como finalidad evaluar las respuestas del sistema cardiovascular bajo distintos escenarios: en reposo, durante el ciclo respiratorio (inhalación y exhalación) y posterior a la realización de actividad física intensa durante 5 minutos. Para registrar las señales biomédicas se empleará el módulo BITalino, el cual digitaliza las señales analógicas a través de un conversor analógico-digital (ADC). Asimismo, el software OpenSignals permitirá la visualización y el almacenamiento de los datos capturados, gracias a su conexión inalámbrica mediante Bluetooth.

### 2.3) Aplicación biomédica

El módulo BITalino ha sido validado como una herramienta eficaz para la adquisición de señales ECG en investigaciones psicofisiológicas. En 2021, un estudio demostró que las señales obtenidas con BITalino presentan una alta concordancia con las registradas por equipos médicos estándar, lo que respalda su uso en contextos clínicos y de investigación donde se requiere una solución económica y portátil para el monitoreo cardíaco [5].

## **5) Resultados** 

| Foto  | Descripción |
|-------|------------|
|<image src="https://github.com/user-attachments/assets/89595d2a-77b8-4f45-b09f-4f5b0770f754" width="1500px" height="270px">|**Señal ECG:** <p align="justify"> Las ondas P, QRS y T son claramente visibles en todas las derivaciones (I, II, III).La frecuencia cardíaca promedio oscila entre 65.5 y 70.6 bpm, dentro del rango normal (60-90 bpm) [A].No se observan alteraciones evidentes en la conducción eléctrica o en el ritmo cardíaco.</p>**Dominio de la Frecuencia:**<p align="justify">El contenido de energía del ECG se concentra aproximadamente entre 0.5 y 50 Hz, lo cual es fisiológicamente normal para las señales de ECG en reposo.Se detecta algo de ruido, el cual es típicamente producto del ambiente de laboratorio o de artefactos menores debido al movimiento.</p> **Observaciones Importantes:**<p align="justify">El ruido eléctrico fue filtrado efectivamente.Se destaca la calidad de adquisición, aunque se pueden observar artefactos menores de movimiento en algunas de las derivaciones.</p>|
|<image src="https://github.com/user-attachments/assets/43b714cd-564b-44d9-81b4-417a36accca7" width="1500px" height="270px">|**Apnea de 10 segundos:** <p align="justify"> Inhalación profunda: Se observa una disminución en el intervalo RR, lo que indica un aumento en la frecuencia cardíaca.Durante la apnea (mantener la respiración): Los intervalos RR se estabilizan, indicando que la frecuencia cardíaca se mantiene constante.</p><p align="justify">Exhalación: Se observa un aumento en el intervalo RR, lo que refleja una disminución en la frecuencia cardíaca [B].</p><p align="justify">Este patrón refleja arritmia sinusal respiratoria, un fenómeno fisiológico normal donde la frecuencia cardíaca varía con la respiración [B]</p>**Respiración cíclica (5s inhalación / 5s exhalación):**<p align="justify"> Durante la inhalación: Se observa un acortamiento en el intervalo RR, lo que corresponde a un aumento en la frecuencia cardíaca.</p><p align="justify">Durante la exhalación: Se observa una elongación del intervalo RR, lo que indica una disminución en la frecuencia cardíaca.</p><p align="justify">Este comportamiento sugiere un funcionamiento normal del sistema nervioso autónomo.</p>|
|<image src="https://github.com/user-attachments/assets/dc61dbe9-3b72-49a1-8222-89b186306f07" width="1500px" height="270px">|**Durante el ejercicio:** <p align="justify"> Se observa un aumento significativo en la frecuencia cardíaca (>99 bpm), lo cual está dentro de los valores normales para un esfuerzo físico [C].Se produce una reducción en los intervalos RR, lo que indica una aceleración en la frecuencia cardíaca.Las ondas P y T muestran variaciones que son típicas como respuesta simpática al esfuerzo físico.</p>**Post-ejercicio (Recuperación):**<p align="justify">Inmediatamente después del ejercicio, la frecuencia cardíaca sigue elevada (>99 bpm), pero comienza a disminuir progresivamente.A pesar de la disminución de la frecuencia, se mantienen fluctuaciones ligeras en los intervalos RR debido al proceso fisiológico de recuperación.Durante la respiración post-ejercicio, se vuelve a observar el fenómeno de arritmia sinusal respiratoria, lo que es normal durante el proceso de recuperación.</p>|
|<image src="https://github.com/user-attachments/assets/8a7636d2-931f-4dc2-b0ce-8446779ba310" width="1500px" height="270px">|**Sosteniendo la respiración:** <p align="justify"> Al mantener la respiración, se observa un aumento en los intervalos RR, lo que indica una disminución de la frecuencia cardíaca. Este fenómeno es conocido como bradicardia por apnea y es típico cuando se interrumpe la respiración voluntariamente.</p><p align="justify">Durante este periodo, los intervalos RR se mantienen estables, lo que refleja una estabilización temporal de la frecuencia cardíaca debido a la falta de intercambio respiratorio.</p><p align="justify">No se observan alteraciones significativas en las ondas P, QRS y T, lo que indica que la conducción eléctrica se mantiene dentro de parámetros normales.</p><p align="justify">El proceso refleja una respuesta fisiológica controlada, donde el sistema nervioso autónomo regula la frecuencia cardíaca para adaptarse a la falta temporal de oxígeno.</p>|

## **6) Conclusiones**

**Limitaciones Identificadas**

<p align ="justify">
- Artefactos de Movimiento:Movimiento del sujeto afectó la estabilidad de la señal del BITalino.</p>
<p align ="justify">
- Colocación de Electrodos:Aunque se intentó seguir el protocolo, se reconoce que podría no haber sido perfecta.</p>
<p align ="justify">
- Condición del Sujeto:Fatiga y somnolencia durante la fase de reposo pudieron alterar los BPM.</p>

**Conclusiones Generales**

<p align ="justify">
- El ECG capturó de manera adecuada los eventos fisiológicos esperados: ritmo cardíaco normal, respuesta respiratoria, y respuesta ante el esfuerzo físico.</p>
<p align ="justify">
- Se observó un patrón normal de taquicardia durante el ejercicio y recuperación post-ejercicio progresiva.</p>
<p align ="justify">
- Importancia de las derivaciones:Las tres derivaciones permitieron una visión complementaria del estado eléctrico del corazón, reforzando el análisis multiaxial.Condiciones externas, colocación imperfecta de electrodos y artefactos de movimiento son fuentes potenciales de error, pero no invalidan los resultados principales.</p>


## **7) Referencias**

<div align="justify">

1. Johns Hopkins Medicine. Electrocardiogram. Available from: https://www.hopkinsmedicine.org/health/treatment-tests-and-therapies/electrocardiogram
2. Monroy JP, Silva H, Alves AP, Fred AL. BITalino: A low-cost, open-source bio-signal acquisition platform. Int J Biomed Eng Technol. 2017;24(4):324-336. Available from: https://www.researchgate.net/publication/236131119_BITalino_A_Biosignal_Acquisition_System_based_on_Arduino
3. PLUX – Wireless Biosignals. BITalino: A low-cost, open-source biosignal acquisition platform. Available from: https://www.pluxbiosignals.com/pages/bitalino​
4. Wasimuddin M, Elleithy K, Abuzneid S, et al. Stages-based ECG signal analysis: From traditional signal processing to machine learning approaches: A survey. 2020. Available from: https://www.researchgate.net/publication/346065771_Stages-Based_ECG_Signal_Analysis_From_Traditional_Signal_Processing_to_Machine_Learning_Approaches_A_Survey​
5. Koch M, Heuer S, Scholler J, Siebert C, Ehlis AC. Validation of a Low-Cost Electrocardiography (ECG) System for Psychophysiological Experiments. Sensors (Basel). 2021 Jul 7;21(14):4753.
</div>
