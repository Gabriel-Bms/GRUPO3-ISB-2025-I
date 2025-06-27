# LABORATORIO 5: Adquisición de EEG

## **Tabla de contenidos:**
<div style="border: 2px solid gray; padding: 20px;border-radius: 15px; width: 40%; height: 180px;">

1. [**Introducción**](#1-introducción)  
2. [**Proposito de la práctica**](#2-proposito-de-la-práctica)
3. [**Materiales y metodos**](#3-materiales-y-metodos)
4. [**Procesamiento**](#4-procesamiento)
5. [**Resultados**](#5-resultados)  
7. [**Referencias**](#7-referencias)

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
  </p>
</div>
<br>

  - **Artefactos:** El usuario parpadeo aproximadamente cada 2 segundos durante 1 minuto y masticó durante otro minuto. 
  - **Libre:** El usurió escuchó música que lo alteraba durante 6 minutos.
    
4. **Almacenamiento y análisis de los datos**:Los archivos generados durante la sesión de adquisición fueron guardados y posteriormente analizados mediante herramientas de procesamiento de señales.


## **4) Procesamiento**
El procesamiento de las señales EEG de los archivos mostrados (ojocerrado.txt, random.txt, puntofijo.txt, entre otros) se realizó con los datos crudos, los cuales se leyeron desde archivos de texto generados por el dispositivo BITalino, utilizando una función específica (leer_eeg_bitalino) que convierte los valores digitales en microvoltios mediante una fórmula de calibración. Esta conversión nos sirve para interpretar correctamente las amplitudes de las señales en unidades físicas. La frecuencia de muestreo se estableció en 1000 Hz, lo que permite capturar adecuadamente los componentes de interés en señales fisiológicas.

Posteriormente, los datos se cargaron en un entorno de procesamiento de señales (MNE-Python) donde se aplicó un filtrado pasa banda entre 0.5 Hz y 40 Hz. Este rango de frecuencias es típico para análisis EEG, ya que elimina tanto el ruido de baja frecuencia (como la deriva basal y movimientos corporales) como el ruido de alta frecuencia (como interferencias eléctricas o artefactos musculares). El filtrado se implementó creando primero un objeto RawArray con la señal cruda y luego aplicando el método filter() de MNE. 

Para evaluar diferencias en el ritmo alfa entre condiciones de ojos abiertos y cerrados, se calculó la densidad espectral de potencia (PSD) utilizando el método de Welch con ventanas de 2 segundos y solapamiento del 50%, lo que permite caracterizar cambios en la banda α (8-13 Hz) asociados a estos estados [5]. Tambien se analizó la activación cortical durante tareas cognitivas, en donde se comparó la potencia en la banda β (13-30 Hz) entre la línea base y la ejecución de la tarea mediante pruebas estadísticas (t-test pareado), lo que ayuda a identificar incrementos significativos relacionados con el procesamiento cognitivo. Por último, se implementó un algoritmo para detectar automáticamente artefactos de parpadeo en los registros EEG, estableciendo un umbral de amplitud (>80 μV) que permite identificar y contabilizar estos eventos en cada condición experimental. Estos procedimientos permiten una evaluación sistemática de los patrones neurales asociados a diferentes estados fisiológicos y cognitivos.

## **5) Resultados**

<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%205%20-%20Adquisicion%20de%20EEG/Imagenes/Punto%20fijo.png><p>

  **Figura 6: Señal EEG mirando a un punto fijo.**
  </p>
</div>
<br>

<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%205%20-%20Adquisicion%20de%20EEG/Imagenes/Parpadeo1.png><p>

  **Figura 7: Señal EEG con parpadeos consecutivos.**
  </p>
</div>
<br>

<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%205%20-%20Adquisicion%20de%20EEG/Imagenes/Masticar.png><p>

  **Figura 8: Señal EEG mientras el usuario mastica.**
  </p>
</div>
<br>

<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%205%20-%20Adquisicion%20de%20EEG/Imagenes/Ojos%20cerrados.jpg><p>

  **Figura 9: Señal EEG con ojos cerrados.**
  </p>
</div>
<br>

<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%205%20-%20Adquisicion%20de%20EEG/Imagenes/musica%20que%20no%20le%20gusta.png><p>

  **Figura 10: Señal EEG mientras el usuario escucha música que no le gusta.**
  </p>
</div>
<br>

<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%205%20-%20Adquisicion%20de%20EEG/Imagenes/musica%20que%20le%20gusta.png><p>

  **Figura 11: Señal EEG mientras el usuario escucha música que sí le gusta.**
  </p>
</div>
<br>

<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%205%20-%20Adquisicion%20de%20EEG/Imagenes/Ejercicios%20cognitivos.png><p>

  **Figura 12: Señal EEG mientras el usuario realiza ejercicios cognitivos.**
  </p>
</div>
<br>

<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%205%20-%20Adquisicion%20de%20EEG/Imagenes/comparacion.png><p>

  **Figura 13: Comparacion de la PSD de las señales EEG de todas las actividades.**
  </p>
</div>
<br>

### 5.1)  ¿Qué banda de frecuencia predomina al cerrar los ojos?

La banda de frecuencia que predomina al cerrar los ojos es la alfa (8 a 12 Hz). Este ritmo, conocido como ritmo alfa dominante posterior, aparece de forma característica en las regiones occipitales del EEG de un adulto despierto y relajado. Es más evidente cuando la persona cierra los ojos y está en reposo mental, y se atenúa (disminuye) al abrir los ojos o al realizar un esfuerzo cognitivo, lo que lo convierte en un marcador importante del estado de reposo con los ojos cerrados.[6]

### 5.2)  ¿Qué filtro es imprescindible para EEG y por qué?

Un ruido de línea es una interferencia eléctrica que proviene del sistema de alimentación eléctrica y se presenta como una señal senoidal de frecuencia fija, generalmente 50 o 60 Hz. Las grabaciones de EEG incluyen este ruido de línea de 50 / 60 Hz que puede corregirse mediante un filtro notch, por lo que este filtro resulta imprescindible[7].

También se sabe que el método más utilizado para clasificar las formas de onda del EEG es según la frecuencia. Las formas de onda más comúnmente estudiadas incluyen delta (de 0.5 a 4 Hz); theta (de 4 a 7 Hz); alfa (de 8 a 12 Hz); sigma (de 12 a 16 Hz), beta (de 13 a 30 Hz) y gamma (de 30 Hz a más). [6]. El ancho de banda convencional del EEG clínico se centra en el análisis de formas de onda que van desde 0.5 Hz hasta 70 Hz. Este análisis se realiza mediante el uso de un filtro pasabanda aplicado a las señales registradas del EEG.

### 5.3) ¿Puedes modular conscientemente tu señal EEG? Da un ejemplo.
La modulación de forma voluntaria de las señales EEG son posibles y según la actividad realizada es posible obervar y detectar con mayor facilidad estos cambios. Durante la sesión práctica se realizaron diferentes ejercicios para comparar la forma de onda, el ejemplo mas sencillo es simplemente mantener los ojos cerrados, ya que así se incrementa la actividad alfa [8]. Por otro lado, el ejercicio   en el que se pudo visualizar mejor la diferencia es al momento de realizar algun ejercicio cognitivo como realizar operaciones matematicas o responder preguntas de razonamiento.

### 5.4) ¿Se observan diferencias entre Fp1 y Fp2? ¿Por qué podrían ocurrir?
Sí, es posible observar diferencias entre Fp1 y Fp2 en señales de EEG. Esto sucede principalmente debido a la asimetría funcional del cerebro humano:  Fp1 corresponde al hemisferio izquierdo y Fp2 al hemisferio derecho [9]. La actividad frontal izquierda se asocia con emociones positivas o aproximación motivacional, y la activdad frontal derecha se relaciona con emociones negativas o evitación. Algunas tareas cognitivas pueden activar de forma diferente estos lóbulos, generando variaciones en la actividad alfa o beta. Sin embargo, durante la sesión práctica solo trabajamos con la señal en Fp1, ya que el canal activo de color rojo se encontraba en la izquierda.

## **6) Referencias**
1. MedlinePlus. Electroencefalograma (EEG) [Internet]. Bethesda (MD): U.S. National Library of Medicine; [actualizado 2022 Oct 31; citado 2025 May 5]. Disponible en: https://medlineplus.gov/spanish/ency/article/003931.htm
2. PLUX Wireless Biosignals. Home Guide 3: EEG [Internet]. Lisbon: PLUX; 2022 Apr [citado 2025 May 5]. Disponible en: https://support.pluxbiosignals.com/wp-content/uploads/2022/04/HomeGuide3_EEG.pdf
3. García González J, Delgado Bolívar G, López Espuela F, Jiménez Antona C, Ortega Calvo M, Márquez G. Electroencefalografía: utilidad clínica de los potenciales evocados. Rev Neurol [Internet]. 2009 [citado 2025 May 5];49(6):321-6. Disponible en: https://scielo.isciii.es/scielo.php?script=sci_arttext&pid=S1137-66272009000600006
4. Serna-Rojas C, Rios Arismendy S, Ochoa Gómez JF. Revisión de electroencefalografía portable y su aplicabilidad en neurociencias. Rev Politéc. 2021;17(34):131-152. Disponible en: https://doi.org/10.33571/rpolitec.v17n34a9.
5. Virtanen P, Gommers R, Oliphant TE, et al. SciPy 1.0: fundamental algorithms for scientific computing in Python. Nat Methods. 2020;17(3):261-272. doi:10.1038/s41592-019-0686-2.
6. Nayak CS, Anilkumar AC. EEG Normal Waveforms. [Updated 2023 Jul 24]. In: StatPearls [Internet]. Treasure Island (FL): StatPearls Publishing; 2025 Jan-. Available from: https://www.ncbi.nlm.nih.gov/books/NBK539805/
7. N. S. Amer and S. B. Belhaouari, "EEG Signal Processing for Medical Diagnosis, Healthcare, and Monitoring: A Comprehensive Review," in IEEE Access, vol. 11, pp. 143116-143142, 2023, doi: 10.1109/ACCESS.2023.3341419.
8. Barry RJ, Clarke AR, Johnstone SJ, Magee CA, Rushby JA. EEG differences between eyes-closed and eyes-open resting conditions. Clin Neurophysiol. 2007;118(12):2765–73. doi:10.1016/j.clinph.2007.07.028
9. Harmon-Jones E. Asymmetrical frontal cortical activity, emotion, and psychopathology: Affective neuroscience approach. Clin Psychol Rev. 2004;24(6):715–34. doi:10.1016/j.cpr.2004.06.003

