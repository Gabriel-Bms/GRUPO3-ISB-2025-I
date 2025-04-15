# Uso de BITalino para EMG

## 1. Introducción
La contracción muscular se basa en dos variables: longitud y tensión. A través de la interacción de los filamentos de actina y miosina, los músculos se acortan y generan fuerza, sin necesariamente cambiar de longitud, como al sostener un objeto o mantener una postura. Este proceso se inicia con un potencial de acción que libera calcio del retículo sarcoplásmico, activando la contracción en los músculos estriados y lisos. La actividad eléctrica generada durante la contracción puede ser medida mediante electromiografía de superficie (sEMG).[1]

La electromiografía de superficie (sEMG) es una técnica principal para detectar las actividades eléctricas de los músculos a través de electrodos de superficie.[2]

A su vez ha sido ampliamente utilizada en evaluación, tratamiento, rehabilitación y entrenamiento en clínicas de deportes y fisioterapia. Específicamente, las mediciones de sEMG se han utilizado para identificar la tensión en la musculatura de las extremidades, así como en los músculos de otras partes del cuerpo humano.
La ventaja de la electromiografía de superficie es ser una medida objetiva y, en teoría, evaluar las actividades musculares de manera directa.[4]

Esta técnica ha sido ampliamente investigada en las últimas dos décadas, con avances significativos tanto en el hardware como en los métodos de procesamiento de señales utilizados para recopilar y analizar las señales de sEMG.[3]

Una de las muchas tecnologías desarrolladas para analizar sEMG es el BITalino, el cual es una plataforma asequible y de código abierto para biosignales, diseñada para la educación y creación de prototipos. Incluye un software fácil de usar (OpenSignals) y bloques de hardware con sensores para ECG, EMG, EDA, EEG, movimiento y más, ideales para entornos de laboratorio y aula.[5]

En este informe, se utilizará el software de BITalino junto con su kit de herramientas para ejecutar la electromiografía de superficie y analizar las señales EMG generadas por el sujeto de prueba. Posteriormente, se procederá a examinar estas señales con el objetivo de profundizar en el tema y identificar los patrones asociados a la contracción muscular humana.

## 2. PROPÓSITO DE LA PRÁCTICA
### 2.1. Objetivos
- Adquirir señales biomédicas de electromiografía (EMG) y electrocardiografía (ECG) utilizando el módulo BITalino.
- Realizar una correcta configuración de BiTalino y conectarlo al software OpenSignals.
- Extraer la información de las señales EMG y ECG del software OpenSignals (r)evolution para procesarlas posteriormente. 

### 2.2. Justificación de la práctica
Se realizará el análisis de las señales EMG y ECG con el objetivo de analizar las respuestas del sistema neuromuscular y cardiovascular ante estímulos como aplicación de fuerzas externas. Se utilizará el módulo BITalino como herramienta para adquirir estas señales biomédicas, para luego convertirlas en señales digitales por medio de un ADC. Además, el software OpenSignals permite visualizar y guardar estas señales en una pantalla al conectarse mediante bluetooth. 

### 2.3. Aplicación biomédica
El módulo BITalino fue utilizado y evaluado como herramienta para adquirir señales ECG en experimentos psicofisiológicos, esto se realizó mediante el registro de la actividad cardíaca en participantes expuestos a estímulos emocionales. El estudió demostró que el módulo es adecuado para el uso en aplicaciones clínicas y en investigaciones de salud mental, debido a que facilita el monitoreo en contextos que no requieren equipos médicos de costo elevado. [5]

## 3. Materiales y Métodos

### 3.1. Materiales
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Laboratorios/Laboratorio%203%20-%20Adquisici%C3%B3n%20de%20se%C3%B1al%20EMG/Imagenes/materiales.png">


### 3.1.2 Métodos
1. Selección de músculos a evaluar
Consultar guías clínicas especializadas para identificar los músculos adecuados para el estudio.

2. Revisión de protocolos de electromiografía (EMG)
Buscar documentación técnica y científica que describa protocolos de adquisición de señales EMG en los músculos seleccionados, para asegurar una toma de datos estandarizada y confiable.

3. Preparación del sistema de adquisición
Encender la placa BITalino y emparejarla con el dispositivo de adquisición (computadora o dispositivo móvil) a través de conexión Bluetooth.

4. Colocación de electrodos EMG
- Rojo (electrodo activo +): Se coloca sobre el vientre del músculo que se desea evaluar, donde se espera captar mayor actividad mioeléctrica.

- Blanco (electrodo de referencia -): Se posiciona aproximadamente a dos dedos de distancia del electrodo activo, alineado con las fibras musculares. Trabaja en conjunto con el rojo para medir la diferencia de potencial eléctrico.

- Negro (electrodo de tierra - GND): No capta señal, pero es esencial para estabilizar el sistema y reducir interferencias eléctricas. Se coloca sobre una zona ósea o eléctricamente neutra.

5. Registro audiovisual del procedimiento
Grabar en vídeo el proceso de colocación de electrodos y la adquisición de datos, mostrando en pantalla los resultados en tiempo real mediante la aplicación correspondiente (por ejemplo, OpenSignals).

6. Adquisición de datos EMG
Iniciar la toma de datos con BITalino, registrando la actividad muscular en tres condiciones distintas:

7. Reposo muscular
Contracción sin carga (fuerza sin peso)
Contracción con carga (fuerza con peso)

- Se recomienda realizar tres repeticiones por cada estadio para obtener datos representativos y comparables.

8. Almacenamiento y análisis de datos
Guardar los archivos generados por la sesión de adquisición. Posteriormente, analizarlos utilizando herramientas de procesamiento de señales para evaluar los patrones de activación muscular en cada condición.


## 4. Resultados 
Se analizaron tres grupos musculares en diferentes condiciones:
- Músculos del antebrazo (flexión/extensión de muñeca)
- Bíceps braquial (flexión de codo)

Condiciones de evaluación:
- Reposo 
- Contracción voluntaria sin carga
- Contracción contra resistencia externa

### Prueba 1: Análisis del antebrazo
Configuración experimental:
- Músculo estudiado: Flexor radial del carpo
- Movimiento evaluado: Flexión/extensión de la muñeca 

Posición de los electrodos:
- Electrodo positivo: Línea media del flexor radial del carpo, región proximal del antebrazo
- Electrodo negativo: Región distal del flexor radial del carpo
- Tierra: Epicóndilo medial

Condiciones:
- Reposo (brazo extendido relajado)
- Contracción sin carga (solo peso del antebrazo)
- Contracción con carga (mochila)

Resultados:
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Laboratorios/Laboratorio%203%20-%20Adquisici%C3%B3n%20de%20se%C3%B1al%20EMG/Imagenes/tabla1.png">

<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Laboratorios/Laboratorio%203%20-%20Adquisici%C3%B3n%20de%20se%C3%B1al%20EMG/Imagenes/tabla2.png">

### Prueba 2: Análisis del Bíceps Braquial
Configuración experimental:
- Músculo estudiado: Bíceps braquial (cabeza larga y corta)
- Movimiento evaluado: Flexión de codo (90° de rango)

Posición de electrodos:
- Electrodo positivo: Línea media del vientre muscular
- Electrodo negativo: Inserción distal
- Tierra: Epicóndilo lateral

Condiciones:
- Reposo (brazo relajado)
- Movimiento muscular sin carga (Flexión de codo utilizando solo el peso del antebrazo)
- Movimiento muscular con una carga
- Carga moderada: Resistencia ligera aplicada por la persona
- Carga máxima: Resistencia máxima aplicada por la persona

Resultados: 
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Laboratorios/Laboratorio%203%20-%20Adquisici%C3%B3n%20de%20se%C3%B1al%20EMG/Imagenes/bicepsresultados1.png">
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Laboratorios/Laboratorio%203%20-%20Adquisici%C3%B3n%20de%20se%C3%B1al%20EMG/Imagenes/bicepsresultados2.png">

## 5. Análisis y Discusión
### Prueba 1: Análisis del antebrazo
Fundamento Fisiológico: 
El flexor radial del carpo es un músculo superficial del compartimiento anterior del antebrazo. Se origina a nivel del epicóndilo medial del húmero por debajo del origen del pronador redondo. Este músculo asegura la flexión y extensión radial de la muñeca [6]. Además, estudios electromiográficos demuestran que:
- El aumento de la fuerza de flexión de la muñeca se asocia con un aumento significativo del promedio de la amplitud obtenida para el análisis del músculo flexor radial del carpo [7]. 
- El músculo flexor radial del carpo se activa durante la flexión de la muñeca en la supinación del antebrazo [8], lo que sugiere que la posición del antebrazo afecta la activación muscular. 

Con respecto a las gráficas obtenidas, se puede observar que:
- En condición de reposo, las señales Raw y Cleaned muestran baja actividad muscular, como era de esperarse en esta condición. Sin embargo, en la gráfica de activación muscular se observan dos picos con una amplitud de alrededor de 0.20 mV, lo cual podría ser causa del ruido del entorno. A pesar de ello, las otras fluctuaciones no superan los ±0.05 mV, confirmando que no hay actividad muscular significativa. 
- En condición de movimiento muscular sin carga, las señales Raw y Cleaned muestran oscilaciones que indican actividad muscular, se puede observar que hay 3 oscilaciones, lo que indicaría 3 repeticiones del mismo movimiento. La señal de la activación muscular ofrece una mejor visualización de los picos de activación, teniendo picos definidos con una amplitud alrededor de 0.15 mV. 
- En condición de movimiento muscular con carga, las señales Raw y Cleaned reflejan una activación muscular más significativa con oscilaciones amplias. La señal procesada elimina el ruido del entorno, logrando así una mejor observación de los picos de activación, donde existe un esfuerzo muscular intenso a comparación del resto, eso se refleja en la amplitud de la señal que aumenta hasta 0.6 mV. Así mismo, se observan las 4 oscilaciones representando a las 4 repeticiones realizadas del movimiento indicado. 

### Prueba 2: Análisis del Bíceps Braquial
Fundamento Fisiológico:
Basado en evidencia científica, el bíceps braquial presenta patrones característicos de activación durante movimientos de flexión del codo. Estudios electromiográficos demuestran que:
- La activación muscular aumenta progresivamente con el ángulo de flexión, alcanzando su máximo alrededor de los 90° de flexión [9].
- Mantiene una activación estable tanto en posiciones neutras como rotadas (supinación/pronación) del antebrazo [9].
- Participa activamente tanto en contracciones dinámicas (concéntricas/excéntricas) como isométricas [9].

Con respecto a las gráficas obtenidas, se puede observar que:
- En la condición de reposo, las señales obtenidas muestran un patrón de inactividad muscular. La señal cruda presenta pequeñas fluctuaciones, con amplitudes que no superan los ±0.3 mV, lo cual corresponde principalmente a ruido del sistema. La señal filtrada, por su parte, se mantiene estable, con valores entre 0.0002 y 0.0008 mV, confirmando que no hay actividad muscular significativa durante este estado de relajación.
- Durante el movimiento sin carga, la señal cambia. Se observan picos definidos de aproximadamente 0.1-0.2 mV en la señal cruda, sincronizados con cada fase del movimiento de flexión. La señal procesada muestra una actividad más limpia, con oscilaciones entre 0.0002 y 0.0006 mV, mostrando la activación rítmica del músculo durante este tipo de contracción moderada.
- Al aplicar la carga externa, los resultados se muestran según la intensidad:
Con carga moderada, la amplitud de la señal aumenta, alcanzando valores de 2 a 3 veces los observados en el movimiento sin carga. La actividad muscular se vuelve más constante durante toda la contracción.
- En condiciones de carga máxima, la señal muestra un esfuerzo muscular mucho más intenso, con momentos de saturación que superan 1 mV en la señal cruda. La activación se mantiene constante, sin los periodos de relajación que se observan en las condiciones menos exigentes.

## 6. Limitaciones 
- Durante el laboratorio pudo haber un desplazamiento de electrodos durante movimiento, lo cual trajo posibles fallas en la adquisición o procesamiento. Se sugiere utilizar electrodos adhesivos de mayor calidad y reforzar su fijación con cinta. También marcar la posición exacta de los electrodos con un marcador para recolocarlos fácilmente si se mueven.
- Se notaba una pequeña interferencia de 60 Hz en todas las mediciones (probablemente por los cables o el mismo equipo). Aunque aplicamos filtros, no se eliminó completamente. Se sugiere alejar los cables del sistema EMG de fuentes de interferencia, y ajustar mejor los filtros notch (específicos para 50/60 Hz) durante el procesamiento.
- Cuando alguien nos hacía resistencia manual (en las pruebas de carga máxima), no siempre podíamos asegurar que la fuerza aplicada fuera exactamente igual en cada repetición. Se sugiere el uso de bandas elásticas con niveles de resistencia definidos en lugar de resistencia manual, y si es que se debe usar asistencia de otra persona, establecer puntos de referencia.
- Después de varias repeticiones, sobre todo en las pruebas con carga, el brazo empezaba a fatigarse y ya no daba el mismo esfuerzo, lo que podía afectar los resultados. Se recomienda aumentar el tiempo de descanso entre series (2-3 minutos) y limitar el número de repeticiones por serie.

## 7. Conclusiones
- Se logró la adquisición y visualización de las señales EMG de los músculos flexor radial del carpo y bicep braquial mediante el módulo BiTalino, lo cual demuestra que la técnica del sEMG es efectiva en la detección de la actividad muscular en tiempo real. 
- El procesamiento de las señales permitió identificar y analizar los patrones de la activación muscular en condiciones de esfuerzo, mediante los picos de activación y la amplitud de la señal. 
- Con respecto al músculo flexor radial del carpo, se observa como aumenta la amplitud de la señal cuando el movimiento es con carga, lo que cumpliría con lo visto teóricamente, que a mayor fuerza de flexión de la muñeca, mayor será la amplitud obtenida. 
- La comparación de las gráficas de condición de reposo, sin carga y con carga permite observar el aumento significativo de la amplitud de la señal, lo cual confirma  que la activación muscular aumenta proporcionalmente con la intensidad de la carga aplicada. 

## 8. Referencias
[1]Gash MC, Kandle PF, Murray IV, Varacallo MA. Physiology, Muscle Contraction. In: StatPearls [Internet]. Treasure Island (FL): StatPearls Publishing; 2025 Jan-. Disponible en: https://www.ncbi.nlm.nih.gov/sites/books/NBK537140/​


[2]Alcan V, Zinnuroğlu M. Current developments in surface electromyography. Turk J Med Sci. 2023;53(5):1019-1031. doi:10.55730/1300-0144.5667.


[3]Alcan V, Zinnuroğlu M. Current developments in surface electromyography. Turk J Med Sci. 2023;53(5):1019-1031. doi:10.55730/1300-0144.5667.

[4]Sommerich CM, Joines SMB, Hermans V, Moon SD. Is Surface Electromyography (sEMG) a Useful Tool in Identifying Muscle Tension Dysphonia? J Voice. 2021;35(5):737.e1-737.e8. doi:10.1016/j.jvoice.2020.07.018.​

[5] Koch M, Heuer S, Scholler J, Siebert C, Ehlis AC. Validation of a Low-Cost Electrocardiography (ECG) System for Psychophysiological Experiments. Sensors (Basel). 2021 Jul 7;21(14):4753.

[6] Elleuch F, Elleuch W, Mohameden A, Harbi H, Ghroubi S, Elleuch H. Flexor carpi radialis muscle: Anatomic features and electromyography technique under ultrasound control. Cureus [Internet]. 2022;14(8):e27936. Disponible en: http://dx.doi.org/10.7759/cureus.27936

[7] Green LA, McGuire J, Gabriel DA. Flexor carpi radialis surface electromyography electrode placement for evoked and voluntary measures: Novel FCR Electrode Placement. Muscle Nerve [Internet]. 2015;52(5):818–25. Disponible en: http://dx.doi.org/10.1002/mus.24631

[8] Ikeda K, Kaneoka K, Matsunaga N, Ikumi A, Yamazaki M, Yoshii Y. Effects of forearm rotation on wrist flexor and extensor muscle activities. J Orthop Surg Res [Internet]. 2025;20(1):53. Disponible en: http://dx.doi.org/10.1186/s13018-024-05363-x
  
[9] R. G. LeFavi, G. K. Limbaugh, J. D. Eitner, y B. L. Riemann, “Medial And Lateral Gastrocnemius Activation Differences During Heel Raise Exercise With Three Different Foot Positions: 1809: Board #159 May 27 3:30 PM - 5:00 PM”, Medicine & Science in Sports & Exercise, vol. 41, núm. 5, p. 137, may 2009, doi: 10.1249/01.MSS.0000354974.32823.a1. Disponible en: https://journals.lww.com/acsm-msse/Fulltext/2009/05001/Medial_And_Lateral_Gastrocnemius_Activation.2009.aspx.
