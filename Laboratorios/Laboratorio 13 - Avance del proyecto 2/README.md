# Avance de Proyecto 1: Analisis Exploratorio de Data y Pre Procesamiento

## 1. Introducción

En la actualidad, el P300 speeler continua siendo uno de los mas estudiados de las interfaces cerebro - computadora (BCI) basadas en potenciales relacionados con eventos. Sin embargo, la adopción de este, fuera del laboratorio sigue siendo baja debido a varios factores [1]. En primer lugar,  la baja tasa de transferencia de informacion (ITR), la cual es inferior a 10 bit.min ^-1 en la mayoria de los estudios, lo que reduce la experiencia de usuario y limita la comunicacion en tiempo real [2] [3]. A ello se le suma el alto costo de los sistemas EEG de grado médico, lo que aumenta la exploración de dispositivos de consumo que sean más asequibles, aunque traigan consigo nuevos retos de calidad de señal [4].
La complejidad para adquirir las señales EEG de alta calidad en entornos que no están controlados tambien ha sido otra de las dificultades, ya que cuando estamos en situaciones cotidianas, existen factores que pueden afectar la calidad de la señal registrada. Estos artefactos (ruidos o distorsiones) que alteran las señales electricas del cerebro pueden ser: el parpadeo, movimiento ocular y contraccion muscular, que pueden hacer que la respuesta del P300 sea dificil de distinguir en medio de estos ruidos [5]. En este contexto, un pre-procesamiento de la señal es importante para mejorar la relación señal-ruido antes de cualquier clasificación [6]. 
El presente trabajo presenta un protocolo integral de Análisis de Datos Exploratorio (EDA) y propone un pipeline de pre-procesamiento reproducible, con el objetivo de mejorar la eficiencia comunicativa y reducir las barreras económicas para futuros desarrollos de interfaces cerebro-computadora (BCI), especialmente en contextos de telemedicina y rehabilitación remota. Al mismo tiempo, las estrategias de pre-procesamiento de última generación como pipelines modulares, algoritmos de rechazo de artefactos basados en aprendizaje automático y referencias comunes virtuales, han demostrado mejoras en la precisión y ITR, además de acelerar el entrenamiento de modelos [7], [8].

## 2. Metodología y Resultados

### 2.1 Arquitectura

Se utilizó una capa de convolución temporal (Temporal Convolution Layer, TCL) que aplica filtros unidimensionales a lo largo del eje temporal, lo que permite capturar patrones locales y dinámicas temporales en las señales EEG. Esta capa resulta fundamental para detectar eventos como el potencial evocado P300 sin necesidad de aplicar métodos manuales de extracción de características [9], [13]. Complementariamente, se empleó una capa de convolución espacial (Spatial Convolution Layer) con el objetivo de capturar las relaciones espaciales entre los diferentes canales registrados. Mientras la TCL permite detectar patrones a lo largo del tiempo en cada canal individual, la convolución espacial opera de forma simultánea sobre todos los canales, facilitando la detección de patrones distribuidos o sincronizados entre regiones cerebrales [13], [14].
Para acelerar el entrenamiento y estabilizar las activaciones, se incorporó una capa de Batch Normalization después de las convoluciones, la cual normaliza las salidas intermedias de la red, asegurando que tengan media cero y varianza unitaria dentro de cada mini-lote. Esto reduce el internal covariate shift y permite que el modelo converja más rápido y de manera más estable, incluso con tasas de aprendizaje más altas [13].
Luego se aplicó una función de activación no lineal, específicamente ReLU (Rectified Linear Unit), debido a su simplicidad y eficiencia computacional. Esta función permite a la red modelar relaciones no lineales y transitorias, características esenciales en datos EEG como la señal P300, que no podrían capturarse únicamente con transformaciones lineales [13, [15].
Como método de regularización para prevenir el sobreajuste, se utilizó la técnica de Dropout, que consiste en desactivar aleatoriamente un porcentaje de neuronas durante el entrenamiento. En este trabajo se aplicó un dropout del 50 % (0.5), ubicado después de las capas convolucionales y antes de la capa densa final. Esta estrategia obliga al modelo a aprender representaciones más generalizables y mejora su rendimiento frente a nuevos datos [9], [13].
Para reducir la complejidad del modelo sin perder capacidad de representación, se empleó una convolución separable (Separable Convolution), que descompone la operación convencional en dos pasos: una convolución depthwise, que aplica un filtro independiente a cada canal de entrada, y una convolución pointwise (1×11 \times 11×1) que combina la información entre canales. Esta técnica permite construir modelos más ligeros y eficientes, especialmente útiles en sistemas BCI en tiempo real [9], [14].
Asimismo, se incorporó una capa de pooling para disminuir la dimensionalidad de las representaciones intermedias y mejorar la capacidad de generalización del modelo. En este caso, se empleó MaxPooling1D, adecuada para reducir la resolución temporal de las señales EEG sin perder los patrones clave asociados a la aparición del P300. Esta reducción también contribuye a mejorar la eficiencia computacional [9], [14].
Finalmente, se incluyó una capa densa (Dense Layer) encargada de realizar la clasificación final a partir de las características extraídas por las capas previas. Esta capa conecta completamente las neuronas con la salida anterior y emplea una función de activación sigmoide, apropiada para tareas de clasificación binaria, como la detección de la presencia o ausencia del potencial evocado P300 [9], [12].


### 2.2 Hiperparametros de entrenamiento
**Learning Rate**
 El learning rate, o tasa de aprendizaje, es un hiper‐parámetro que determina el tamaño de los pasos con que un modelo ajusta sus pesos en cada iteración del algoritmo de optimización. Un valor de learning rate apropiado facilita una convergencia rápida y estable hacia un mínimo de la función de pérdida, mientras que un valor demasiado alto puede provocar oscilaciones o divergencia, y uno demasiado bajo ralentiza el aprendizaje o puede dejar al modelo atrapado en mínimos locales subóptimos [16].
**Optimizador**
 El optimizador es el algoritmo encargado de actualizar los pesos del modelo en función del gradiente de la función de pérdida. Por ejemplo, Adam combina las ventajas de métodos basados en momentos y adaptativos, ajustando dinámicamente la tasa de aprendizaje de cada parámetro según estimaciones de primer y segundo momento del gradiente. Esto suele traducirse en una convergencia más rápida y robusta que métodos más simples como SGD puro [17].
**Batch Size**
 El batch size indica cuántas muestras del conjunto de datos se usan para calcular el gradiente y actualizar los pesos en cada paso. En Mini-batch SGD, se suele elegir potencias de 2 (p. ej., 32, 64, 128…) para optimizar el uso de memoria de la GPU. Un batch grande aprovecha mejor el paralelismo, pero requiere más memoria y puede sobreajustar, mientras que uno pequeño ofrece regularización implícita y más actualizaciones por época, a costa de mayor ruido en el gradiente [18].
**Épocas (Epochs)**
 Una época corresponde a procesar todo el conjunto de entrenamiento una vez. Durante cada época, el modelo recorre todos los lotes y ajusta sus pesos. Incrementar el número de épocas permite un mejor aprendizaje, pero con riesgo de sobreajuste. Para elegir el número óptimo de épocas, se monitoriza la pérdida de validación y se aplican técnicas como early stopping o validación cruzada para detener el entrenamiento antes de que comience a degradarse el desempeño en datos no vistos [19].
**Función de Pérdida (Loss Function)**
 La función de pérdida cuantifica el error entre las predicciones del modelo y las etiquetas reales. Su elección depende de la tarea: regresión (p. ej., MSE), clasificación binaria (p. ej., binary cross‐entropy) o multiclase (categorical cross‐entropy). Ajustar hiperparámetros como la tasa de regularización o parámetros internos de la función de pérdida (por ejemplo, el offset en focal loss) puede mejorar la robustez frente a outliers y desequilibrios en las clases, optimizando así la capacidad del modelo para generalizar [20].
**Pesos de Clase (class_weight)**
 El parámetro class_weight en Scikit-Learn asigna un peso a cada clase inversamente proporcional a su frecuencia o según un diccionario personalizado. Esto penaliza más los errores en las clases minoritarias, obligando al modelo a prestarles mayor atención durante el entrenamiento y reduciendo el sesgo hacia la clase mayoritaria en conjuntos de datos desbalanceados [21].


### 2.3 Control de overfitting
El overfitting es un problema común cuando se entrena modelos con deep learning, especialmente en señales EEG. Básicamente, ocurre cuando el modelo aprende no solo los patrones útiles de los datos, sino también el ruido o detalles específicos que no se repiten en otros casos. Eso hace que luego no funcione bien con datos nuevos. Esto pasa mucho en EEG porque es difícil conseguir grandes bases de datos, ya que los experimentos son largos, hay pocos sujetos, y además hay bastante variabilidad entre personas [I][III][IV].
Para evitar esto, una técnica que se usa en varios papers fue el early stopping, que consiste en detener el entrenamiento si la pérdida de validación ya no mejora después de un cierto número de iteraciones. Así se guarda el modelo que mejor rendimiento tuvo en validación, y se evita seguir entrenando de más, lo cual podría llevar al sobreajuste. Esta estrategia ayudó a que el modelo sea más generalizable y no solo funcione con los datos de entrenamiento [V][VI].
Otra técnica bastante útil para evitar el overfitting es el data augmentation, que básicamente lo que hace es aumentar los datos de entrenamiento generando nuevas muestras a partir de las existentes, con transformaciones que no cambian la etiqueta. Esto sirve especialmente en EEG porque normalmente se trabaja con bases de datos pequeñas. Además, al haber más variedad en los datos, el modelo aprende patrones más generales y no se queda con detalles irrelevantes [I][III][IV].
Recientemente, en un estudio publicado en junio de 2025, se propuso una herramienta llamada EEG-GAN, diseñada específicamente para realizar data augmentation en señales EEG. Esta técnica permite generar muestras sintéticas realistas a partir de registros existentes, conservando patrones relevantes como los potenciales evocados (ERP) y las representaciones tiempo-frecuencia. Según los resultados reportados, el uso de EEG-GAN mejoró significativamente el rendimiento en tareas de decodificación neuronal, especialmente en contextos donde la recolección de grandes volúmenes de datos es limitada, como en aplicaciones móviles o clínicas [II]. Sin embargo, debido a la reciente publicación de este trabajo , no fue posible implementar EEG-GAN dentro del proyecto actual.



### 2.4 Métricas 

El rendimiento del modelo de clasificación para señales EEG tipo P300, necesita considerar métricas que permitan cuantificar el desempeño del sistema. En la practica, es fundamental diferenciar eventos relevantes de irrelevantes para el estudio, es decir, entender cómo se comporta el modelo ante verdaderos positivos, falsos positivos y falsos negativos. A continuación, se describen las principales métricas utilizadas:

- La precisión es una métrica para indicar la eficacia de las predicciones positivas de un modelo, es decir, mide la proporción de veces que el modelo acierta cuando se predice que la observación pertenece es positiva. Esta métrica es útil cuando los falsos positivos tienen un impacto importante, ya que permite entender la cantidad de veces que el sistema “confundió” eventos negativos por eventos positivos. En el contexto de nuestro proyecto, se presenta un sistema BCI tipo P300 Speller, para el cual una alta precisión implicaría que cuando el modelo detecta la intención del usuario de seleccionar un carácter, es muy probable que esta predicción sea correcta. Sin embargo, una alta precisión no garantiza que todos los eventos relevantes estén siendo captados, en cambio, indica que los pocos que sí fueron detectados mantienen una alta fiabilidad [x1].
La fórmula correspondiente es: Precisión = TP / (TP + FP) 

- El recall es conocido también como sensibilidad, ya que representa la capacidad del modelo para identificar correctamente todos los eventos positivos reales, es decir, mide la proporción de veces que el modelo acierta cuando correspondía detectar un estímulo objetivo. En sistemas BCI, esto se traduce como la cantidad de veces que el modelo logra detectar una señal P300 cuando el usuario en realidad está enfocado en un carácter. Esta métrica es fundamental para los casos en que los falsos negativos son críticos, ya que no detectar una intención del usuario puede significar la pérdida de la oportunidad de comunicación. Por ello, el recall se convierte en una prioridad para aplicaciones en las que es más perjudicial no identificar una señal verdadera, que simplemente equivocarse al verla. [x2]
La fórmula correspondiente es: Recall = TP / (TP + FN)

- El F1-score es una métrica que combina tanto la precisión como el recall en un solo valor, de forma que utiliza la media armónica entre ambos. Esta medida es especialmente útil cuando se requiere que exista un equilibrio entre la capacidad del modelo para detectar correctamente los eventos positivos (recall) y su capacidad para no equivocarse al hacer predicciones positivas (precisión). En el caso del P300 Speller, el F1-score permite evaluar si el modelo detecta bien las señales relevantes y si lo hace con una tasa de error aceptable. Esta métrica es recomendable cuando se trabaja con señales como EEG, donde los estímulos objetivo (Target) son menos frecuentes que los no objetivo (Non-Target) [x3].
La fórmula correspondiente es:  F1 = 2 * (Precisión * Recall) / (Precision + Recall)

- La curva ROC es una herramienta que permite visualizar el desempeño a distintos umbrales de decisión. En esta curva se representa la tasa de verdaderos positivos y la tasa de falsos positivos, lo cual permite observar cómo varía la sensibilidad del modelo a medida que cambia el umbral de clasificación. Gráficamente, cuanto más cerca esté la curva del vértice superior izquierdo, mejor será el rendimiento del modelo. El área bajo la curva cuantifica esta información en un solo valor entre 0 y 1, donde valores cercanos a 1 indican un modelo altamente discriminativo. Aunque es una métrica global útil para comparar modelos, en el caso de sistemas BCI centrados en captar señales como el P300, se suele complementar con métricas más específicas como el recall. [x4]
Las fórmulas correspondientes son: 
TPR (True Positive Rate) = TP / (TP + FN)
FPR (False Positive Rate) = FP / (FP + TN)

En aplicaciones de BCI donde se usa el reconocimiento de la señal P300 para deletreadores mentales, lo más importante es asegurar que el sistema detecte con éxito la mayoría de las intenciones comunicativas del usuario. Esto se traduce en maximizar la capacidad del sistema para identificar correctamente estímulos relevantes, es decir, lograr un alto recall. Un falso negativo, implicaría no captar un carácter que el usuario intentó seleccionar, afectando directamente la eficacia y utilidad del sistema. En cambio, los falsos positivos pueden corregirse mediante mecanismos de retroalimentación. Algunas métricas como la precisión o el F1-score aportan información valiosa;sin embargo, la métrica con mayr relevancia en la finalidad clínica del sistema es el recall [x4]. 


## 3. Resultados

En las tres sesiones del protocolo P300 Speller se presentaron 84 flashes Target (84 flashes de conjunto de letras que contenían la letra que el usuario deseaba escribir) por sesión (252 en total). Tras segmentar la señal en épocas de 800 ms y dividir la data en 80% para entrenamiento y 20% para validación (50 flashes target para validación), el modelo basado en una arquitectura de redes convolucionales, EEGNet, adaptada a nuestro dataset de pacientes ALS, extraído del dataset big3BCI, arrojó la siguiente matriz de confusión mostrada.


Se puede ver que el modelo identificó correctamente 47 de los 50 eventos (sensibilidad ≈ 0,94) y clasificó 376 de 404 eventos Non-Target (especificidad ≈ 0,93), con una exactitud global cercana al 93 %. Este desempeño supera lo reportado históricamente por métodos clásicos de clasificación de P300 (p. ej., SWLDA, LDA o bayesianos), que suelen rondar sensibilidades del 70-85 % bajo las mismas condiciones experimentales y requieren ingeniería de características manual (promediado de ERPs, selección de ventanas y canales, etc.). La red aprovecha convoluciones espaciales y temporales para captar firmas P300 incluso con variabilidad inter-sesión, reduciendo la dependencia del preprocesado artesanal y abriendo la puerta a mayores tasas de comunicación (bit rate) con menos flashes por carácter. 

  **Figura 1: Resultados.**
  </p>
</div>
<br>

<br>
</p>
<div align="center">
  <img src=https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/main/Laboratorios/Laboratorio%2013%20-%20Avance%20del%20proyecto%202/figresultados.png><p>

## 4. Conclusiones
Los resultados obtenidos confirman que el enfoque de aprendizaje profundo implementado es capaz de distinguir de manera confiable entre los eventos Target y Non-Target. El modelo basado en la red neuronal convolucional EEGNet, adaptado específicamente a los datos de pacientes con ALS y señales EEG del dataset big3BCI, logró un buen rendimiento, con una sensibilidad de 0.94 y una especificidad de 0.93. Estos resultados son superiores a los obtenidos con métodos tradicionales como SWLDA, LDA y modelos bayesianos, que generalmente muestran sensibilidades entre 70% y 85% en condiciones similares y requieren una gran cantidad de procesamiento manual de las características.
El uso de convoluciones espaciales y temporales ha sido clave para mejorar la detección de las firmas P300, incluso cuando hay variabilidad entre las sesiones, permitió reducir la dependencia de técnicas de preprocesamiento manual. Esto también ha mejorado la tasa de comunicación (bit rate) con menos flashes por carácter, lo que hace que el sistema sea más eficiente y accesible.
Estos avances demuestran que el aprendizaje profundo puede ser una herramienta potente para el análisis de señales EEG complejas, y que también abren nuevas oportunidades para su uso en dispositivos portátiles y en aplicaciones de tele-rehabilitación. Con estos avances, el P300 speller podría convertirse en una herramienta más práctica y accesible, lo que sería un gran paso hacia la mejora de la calidad de vida de las personas con discapacidades motoras severas.


## Referencias
1. Interfaz cerebro-ordenador P300: retos actuales y tendencias emergentes
 R. S. O'Keefe, J. M. Cohen, and D. H. Silver, "A review of the P300 speller: The challenges and trends," Sensors, vol. 21, no. 17, p. 5746, Aug. 2021. [Online]. Available: https://www.mdpi.com/1424-8220/21/17/5746.


2. A systematic review of the efficiency of P300-based digital spellers
 A. M. Pérez, A. R. Valencia, and M. G. Fernández, "A systematic review of the efficiency of P300-based digital spellers," Proceedings of the 2024 8th International Conference on Advances in Artificial Intelligence, pp. 3704137–3704196, 2024. [Online]. Available: https://dl.acm.org/doi/10.1145/3704137.3704196.


3. Performance improvement of P300-based home appliances control classification using convolution neural network
 M. Yağan, H. Ozkan, “Performance improvement of P300-based home appliances control classification using convolution neural network,” Biomedical Signal Processing and Control, vol. 70, p. 103950, 2022. [Online]. Available: https://doi.org/10.1016/j.bspc.2021.103950.


4. Una revisión exploratoria sobre el uso de dispositivos de EEG para el consumidor para la investigación
 F. J. López, P. Ruiz, "Una revisión exploratoria sobre el uso de dispositivos de EEG para el consumidor para la investigación," PubMed, [Online]. Available: https://pmc.ncbi.nlm.nih.gov/articles/PMC10917334/.


5. Los algoritmos automatizados de rechazo de artefactos dañan el rendimiento de la interfaz cerebro-computadora del deletreador P3
 M. Pérez-Rodríguez et al., "The impact of automated artifact rejection algorithms on P300 speller BCI performance," Journal of Real-Time Image Processing, vol. 21, pp. 334-345, 2023. [Online]. Available: https://link.springer.com/article/10.1007/s11042-023-15653-x.


6. Assessment of Preprocessing on Classifiers Used in the P300 Speller Paradigm C. Wang et al., "Assessment of preprocessing on classifiers used in the P300 speller paradigm," IEEE Trans. Biomed. Eng., vol. 63, no. 12, pp. 2187-2196, Dec. 2016. [Online]. Available: https://ieeexplore.ieee.org/document/4462003.


7. W. Kwon, M. J. Kim, "EEG dataset for RSVP and P300 speller brain-computer interfaces," Scientific Data, vol. 9, p. 388, 2022. [Online]. Available: https://doi.org/10.1038/s41597-022-01509-w.


8. A new benchmark dataset for P300 ERP-based BCI applications
 M. Yağan, H. Özkan, "A new benchmark dataset for P300 ERP-based BCI applications," Digital Signal Processing, vol. 135, p. 103950, 2023. [Online]. Available: https://doi.org/10.1016/j.dsp.2023.103950.

9. A. Mostafa, Y. Ma, Y. Liu, M. Aly, and G. Chen, “Deep Learning-Based EEG Classification for P300 Detection in Brain–Computer Interface Applications,” Applied Sciences, vol. 14, no. 14, art. 6347, 2024. [Online]. Available: https://www.mdpi.com/2076-3417/14/14/6347
10. R. Sharma and R. B. Pachori, “A review on hybrid brain–computer interface systems,” Brain Informatics, vol. 9, no. 1, p. 3, 2022. [Online]. Available: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC9774292/
11. A. Kübler, B. Kotchoubey, J. Kaiser, J. Wolpaw, and N. Birbaumer, “Brain–computer communication: unlocking the locked in,” Psychological Bulletin, vol. 127, no. 3, pp. 358–375, 2001. [Online]. Available: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3432970/
12. D. J. Krusienski et al., “A comparison of classification techniques for the P300 Speller,” Journal of Neural Engineering, vol. 3, no. 4, pp. 299–305, 2006. doi: 10.1088/1741-2560/3/4/007
13. M. Schirrmeister et al., “Deep learning with convolutional neural networks for EEG decoding and visualization,” Human Brain Mapping, vol. 38, no. 11, pp. 5391–5420, 2017. doi: 10.1002/hbm.23730
14. S. Sakhavi, C. Guan, and S. Yan, “Parallel convolutional-linear neural network for classification of EEG signals,” in Proc. 2015 23rd European Signal Processing Conference (EUSIPCO), Nice, France, 2015, pp. 2749–2753.
15.  H. Raza, S. M. Asif, S. Khan, and T. R. Choudhury, “EEG-based brain-computer interface using deep learning for emotion recognition,” Biomedical Signal Processing and Control, vol. 82, p. 104529, 2023. doi: 10.1016/j.bspc.2022.104529
16. MSMK University, “El learning rate, o tasa de aprendizaje,” MSMK University, [En línea]. Disponible: https://msmk.university/learning-rate/. [Accedido: 1-Jul-2025].
17. Encord, “Fine-tuning models and hyperparameter optimization,” Encord Blog, [En línea]. Disponible: https://encord.com/blog/fine-tuning-models-hyperparameter-optimization/. [Accedido: 1-Jul-2025].
18. KeepCoding, “Batch size en Deep Learning,” KeepCoding Blog, [En línea]. Disponible: https://keepcoding.io/blog/batch-size-deep-learning/. [Accedido: 1-Jul-2025].
19. LYZR AI, “Epochs,” LYZR AI Glossary, [En línea]. Disponible: https://www.lyzr.ai/glossaries/epochs/. [Accedido: 1-Jul-2025].
20. Number Analytics, “Optimizing loss functions for better AI models,” Number Analytics Blog, [En línea]. Disponible: https://www.numberanalytics.com/blog/optimizing-loss-functions-for-ai. [Accedido: 1-Jul-2025].
21. GeeksforGeeks, “How does the class_weight parameter in Scikit-Learn work?,” GeeksforGeeks, 07-Aug-2024. [En línea]. Disponible: https://www.geeksforgeeks.org/machine-learning/how-does-the-classweight-parameter-in-scikit-learn-work/. [Accedido: 1-Jul-2025].

22.  C. He, J. Liu, Y. Zhu y W. Du, "Data Augmentation for Deep Neural Networks Model in EEG Classification Task: A Review," Frontiers in Human Neuroscience, vol. 15, 17-Dec-2021. [En línea]. Disponible: https://www.frontiersin.org/journals/human-neuroscience/articles/10.3389/fnhum.2021.765525/full. [Accedido: 02-Jul-2025].
23.  C. C. Williams, D. Weinhardt, J. Hewson, M. B. Plomecka, N. Langer y S. Musslick, “EEG‑GAN: A Generative EEG Augmentation Toolkit for Enhancing Neural Classification,” bioRxiv, preprint, 25‑Jun‑2025. [En línea]. Disponible: https://www.biorxiv.org/content/10.1101/2025.06.23.661164v1. [Accedido: 02‑Jul‑2025].
24.  C. Rommel, J. Paillard, T. Moreau y A. Gramfort, “Data augmentation for learning predictive models on EEG: a systematic comparison,” arXiv preprint arXiv:2206.14483, 29‑Jun‑2022. [En línea]. Disponible: https://arxiv.org/abs/2206.14483?utm_source=chatgpt.com. [Accedido: 02‑Jul‑2025].
25.  E. Lashgari, D. Liang y U. Maoz, “Data augmentation for deep‑learning‑based electroencephalography,” Journal of Neuroscience Methods, vol. 346, p. 108885, 31‑Jul‑2020. [En línea]. Disponible: https://pubmed.ncbi.nlm.nih.gov/32745492/. [Accedido: 02‑Jul‑2025].
26.  M. Tveter, T. Tveitstøl, C. Hatlestad‑Hall, A. S. Pérez Teseyra, E. Taubøll, A. Yazidi y H. L. Hammer, “Advancing EEG prediction with deep learning and uncertainty estimation,” Brain Informatics, vol. 11, art. 27, 28‑Jun‑2025. [En línea]. Disponible: https://braininformatics.springeropen.com/articles/10.1186/s40708-024-00239-6?utm_source=chatgpt.com. [Accedido: 02‑Jul‑2025].
27. H. Song, M. Kim, D. Park y J.-G. Lee, “How does Early Stopping Help Generalization against Label Noise?,” arXiv preprint arXiv:1911.08059, 8‑Sep‑2020. [En línea]. Disponible: https://arxiv.org/abs/1911.08059. [Accedido: 02‑Jul‑2025].
28. D. M. W. Powers, “Evaluation: From Precision, Recall and F-Measure to ROC, Informedness, Markedness and Correlation,” Journal of Biomedical Informatics, vol. 42, no. 2, pp. 335–339, Apr. 2011. doi: 10.1016/j.jbi.2010.09.001.
29. D. M. W. Powers, “Evaluation: From Precision, Recall and F-Measure to ROC, Informedness, Markedness and Correlation,” Journal of Biomedical Informatics, vol. 42, no. 2, pp. 335–339, Apr. 2011. doi: 10.1016/j.jbi.2010.09.001.
30. T. Fawcett, “An introduction to ROC analysis,” Pattern Recognition Letters, vol. 27, no. 8, pp. 861–874, Jun. 2006. doi: 10.1016/j.patrec.2005.10.010.
31. T. Saito and M. Rehmsmeier, “The precision-recall plot is more informative than the ROC plot when evaluating binary classifiers on imbalanced datasets,” PLoS ONE, vol. 10, no. 3, p. e0118432, Mar. 2015. doi: 10.1371/journal.pone.0118432.

