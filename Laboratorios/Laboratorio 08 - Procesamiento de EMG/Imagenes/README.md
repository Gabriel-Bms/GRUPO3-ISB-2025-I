# LABORATORIO 7: Filtros Wavelet

## **Tabla de contenidos:**
<div style="border: 2px solid gray; padding: 20px;border-radius: 15px; width: 40%; height: 180px;">

1. [**Transformada Wavelet aplicada a señales ECG**](#1-introducción)  
2. [**Transformada Wavelet aplicada a señales EMG**](#2-proposito-de-la-práctica)
3. [**Transformada Wavelet aplicada a señales EEG**](#3-materiales-y-metodos)

</div>
<br>

## **1) Introducción** 
La electroencefalografía (EEG) permite registrar la actividad eléctrica cerebral mediante electrodos colocados sobre el cuero cabelludo. [1] Esta actividad es el resultado de la sincronización de potenciales postsinápticos excitatorios e inhibitorios, principalmente en las neuronas piramidales de la corteza cerebral. El EEG refleja distintos estados neurofisiológicos como el sueño, la atención, la relajación o la carga cognitiva, y se organiza en bandas de frecuencia específicas: delta, theta, alfa, beta y gamma.[2]

<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%205%20-%20Adquisicion%20de%20EEG/Imagenes/444.jpeg><p>

  **Figura 1: Bandas de EEG, ocurrencias y tareas para activar las bandas. [2]**
  </p>
</div>
<br>

La EEG de superficie es una técnica no invasiva ampliamente utilizada en neurociencia, medicina del sueño y neurorehabilitación. Su aplicación va desde el monitoreo clínico de epilepsia hasta el análisis de estados mentales en tareas cognitivas. Las señales EEG son altamente sensibles a artefactos de movimiento, oculares y eléctricos, por lo que requieren una correcta colocación de electrodos y un riguroso procesamiento de señales. [3]

En esta práctica se empleará el sistema BITalino (r)evolution para adquirir señales EEG mediante el software OpenSignals. Se registrarán señales en posiciones Fp1, Fp2 y O2 según el sistema 10-20, bajo condiciones controladas (ojos abiertos/cerrados, tareas cognitivas, artefactos simulados) y se aplicarán filtros pasa banda (0.8–48 Hz) para el análisis de potencia espectral y detección de ritmos cerebrales.

El objetivo es explorar patrones característicos de las distintas bandas EEG y comprender la dinámica eléctrica cerebral en función de la actividad mental. A través de este enfoque, se busca fortalecer la competencia en adquisición, procesamiento y análisis de bioseñales cerebrales en un entorno experimental controlado.


## **2) Proposito de la práctica** 
### 2.1) Objetivos:
Configuración del BiTalino y Conexión al Software OpenSignals: Realizar una correcta configuración del dispositivo BiTalino y conectarlo al software OpenSignals para la adquisición de señales EEG, asegurando que la conexión inalámbrica mediante Bluetooth esté activa y estable.

Adquisición y Extracción de Señales EEG: Obtener y extraer las señales EEG utilizando el software OpenSignals (r)evolution para su posterior procesamiento y análisis.

Análisis de las Señales EEG: Procesar las señales EEG adquiridas mediante su visualización gráfica y análisis de las bandas de frecuencia
durante diferentes actividades (reposo, abrir y cerrar los ojos, tareas cognitivas).

### 2.2) Justificación de la Práctica:
El análisis de las señales EEG tiene como finalidad estudiar las respuestas del cerebro en distintas situaciones:

En reposo: Obtener la señal basal para establecer un patrón de referencia de la actividad cerebral sin estímulos externos.

Durante la tarea de abrir y cerrar los ojos: Evaluar los cambios en las señales EEG, particularmente en la banda alfa, que se asocia con la relajación y la reducción de la actividad cortical cuando los ojos están cerrados.

Durante tareas cognitivas (ejercicios de razonamiento): Analizar cómo se activan las bandas beta y gamma durante la resolución de problemas aritméticos sencillos y complejos, lo que indica un aumento en la actividad cerebral relacionada con el esfuerzo cognitivo.

### 2.3) Aplicación Biomédica:
El dispositivo BiTalino ha sido validado como una herramienta efectiva para la adquisición de señales EEG en investigaciones neurológicas y psicofisiológicas. Un estudio reciente mostró que las señales EEG obtenidas con BiTalino presentan una alta concordancia con las señales captadas por equipos médicos estándar, lo que valida su uso en contextos clínicos y de investigación. BiTalino ofrece una solución económica y portátil, ideal para el monitoreo de la actividad cerebral en escenarios donde la movilidad y la accesibilidad son esenciales. Además, permite su integración en aplicaciones de neurofeedback, interfaces cerebro-computadora (BCI) y en el estudio de trastornos neurológicos [4].

## **3) Materiales y métodos**

### 3.1) Materiales:

- 01 Kit BITalino  
- 01 Laptop  
- 03 Electrodos superficiales  

### 3.2) Métodos:
1. **Preparación del sistema de adquisión:** Se encendió la placa BITalino y se emparejó con la computadora mediante conexión Bluetooth.
2. **Colocación de electrodos:**
   
  - **Rojo (Electrodo activo)**: Se colocó en la posición de Fp1,  ubicada en el lado izquierdo de la frente, según se indica en la imagen 2.
  - **Blanco (Electrodo de referencia)**: Se colocó en la región del mastoide, el cual está ubicado en la región bajo la oreja. 
  - **Negro (Electrodo GND)**: Se colocó en la posición de Fp2, correspondiente al lado derecho de la frente, como se muestra en la imagen 2.

<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%205%20-%20Adquisicion%20de%20EEG/Imagenes/111.png><p>

  **Figura 2: Posición de los electrodos**
  </p>
</div>
<br>

<br>
</p>
<div align="center">
  <img src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%205%20-%20Adquisicion%20de%20EEG/Imagenes/555.jpeg" width="350"><p>

  **Figura 3: Posición de los electrodos en el usuario**
  </p>
</div>
<br>

<br>
</p>
<div align="center">
  <img src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%205%20-%20Adquisicion%20de%20EEG/Imagenes/666.jpeg" width="350"><p>

  **Figura 4: Posición de los electrodos en el usuario**
  </p>
</div>
<br>

3. **Adquisición de datos EEG**: Se realizó 5 diferentes condiciones experimentales para evaluar las diferentes patrones en las señales EEG obtenidas. Estas condiciones son:
   
  - **Basal 1:** El usuario tuvo los ojos abiertos y matuvo la mirada en un punto fijo por 1 minuto. 
  - **Basal 2:** El usuario tuvo los ojos cerrados por un minuto. 
  - **Tarea cognitiva:** Se realizó preguntas lógicas simples y complejas al usuario durante 2 minutos. Las preguntas fueron:
    <br>
</p>
<div align="center">
  <img src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%205%20-%20Adquisicion%20de%20EEG/Imagenes/777.png" width="550"><p>

  **Figura 5: Preguntas simples y complejas**