# Uso de BITalino para EMG

## 1. Introducción
La contracción muscular se basa en dos variables: longitud y tensión. A través de la interacción de los filamentos de actina y miosina, los músculos se acortan y generan fuerza, sin necesariamente cambiar de longitud, como al sostener un objeto o mantener una postura. Este proceso se inicia con un potencial de acción que libera calcio del retículo sarcoplásmico, activando la contracción en los músculos estriados y lisos. La actividad eléctrica generada durante la contracción puede ser medida mediante electromiografía de superficie (sEMG).[1]

La electromiografía de superficie (sEMG) es una técnica principal para detectar las actividades eléctricas de los músculos a través de electrodos de superficie.[2]

Esta técnica ha sido ampliamente investigada en las últimas dos décadas, con avances significativos tanto en el hardware como en los métodos de procesamiento de señales utilizados para recopilar y analizar las señales de sEMG.[3]

A su vez ha sido ampliamente utilizada en evaluación, tratamiento, rehabilitación y entrenamiento en clínicas de deportes y fisioterapia. Específicamente, las mediciones de sEMG se han utilizado para identificar la tensión en la musculatura de las extremidades, así como en los músculos de otras partes del cuerpo humano.
La ventaja de la electromiografía de superficie es ser una medida objetiva y, en teoría, evaluar las actividades musculares de manera directa.[4]

En este informe se utilizará la electromiografía de superficie para analizar las señales EMG producidas por el sujeto de prueba y se procederá a analizar dichas señales con el fin de explorar más a fondo el tema, y reconocer los patrones generados en la contracción muscular humana.

## 2. PROPÓSITO DE LA PRÁCTICA
2.1. Objetivos
- Adquirir señales biomédicas de electromiografía (EMG) y electrocardiografía (ECG) utilizando el módulo BITalino.
- Realizar una correcta configuración de BiTalino y conectarlo al software OpenSignals.
- Extraer la información de las señales EMG y ECG del software OpenSignals (r)evolution para procesarlas posteriormente. 

2.2. Justificación de la práctica
Se realizará el análisis de las señales EMG y ECG con el objetivo de analizar las respuestas del sistema neuromuscular y cardiovascular ante estímulos como aplicación de fuerzas externas. Se utilizará el módulo BITalino como herramienta para adquirir estas señales biomédicas, para luego convertirlas en señales digitales por medio de un ADC. Además, el software OpenSignals permite visualizar y guardar estas señales en una pantalla al conectarse mediante bluetooth. 

2.3. Aplicación biomédica
El módulo BITalino fue utilizado y evaluado como herramienta para adquirir señales ECG en experimentos psicofisiológicos, esto se realizó mediante el registro de la actividad cardíaca en participantes expuestos a estímulos emocionales. El estudió demostró que el módulo es adecuado para el uso en aplicaciones clínicas y en investigaciones de salud mental, debido a que facilita el monitoreo en contextos que no requieren equipos médicos de costo elevado. [5]
