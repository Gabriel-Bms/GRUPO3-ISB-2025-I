# Uso de BITalino para EMG

## 1. Introducción
La contracción muscular se basa en dos variables: longitud y tensión. A través de la interacción de los filamentos de actina y miosina, los músculos se acortan y generan fuerza, sin necesariamente cambiar de longitud, como al sostener un objeto o mantener una postura. Este proceso se inicia con un potencial de acción que libera calcio del retículo sarcoplásmico, activando la contracción en los músculos estriados y lisos. La actividad eléctrica generada durante la contracción puede ser medida mediante electromiografía de superficie (sEMG).[1]

La electromiografía de superficie (sEMG) es una técnica principal para detectar las actividades eléctricas de los músculos a través de electrodos de superficie.[2]

Esta técnica ha sido ampliamente investigada en las últimas dos décadas, con avances significativos tanto en el hardware como en los métodos de procesamiento de señales utilizados para recopilar y analizar las señales de sEMG.[3]

A su vez ha sido ampliamente utilizada en evaluación, tratamiento, rehabilitación y entrenamiento en clínicas de deportes y fisioterapia. Específicamente, las mediciones de sEMG se han utilizado para identificar la tensión en la musculatura de las extremidades, así como en los músculos de otras partes del cuerpo humano.
La ventaja de la electromiografía de superficie es ser una medida objetiva y, en teoría, evaluar las actividades musculares de manera directa.[4]

En este informe se utilizará la electromiografía de superficie para analizar las señales EMG producidas por el sujeto de prueba y se procederá a analizar dichas señales con el fin de explorar más a fondo el tema, y reconocer los patrones generados en la contracción muscular humana.

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

