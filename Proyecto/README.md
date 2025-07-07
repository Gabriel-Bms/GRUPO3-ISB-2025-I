# A Lightweight Deep Learning Model for P300 Detection on Microcontroller-Based BCI Systems for communication in ALS patients


### **Proyecto: Un modelo ligero de aprendizaje profundo para la detección de P300 en sistemas BCI basados en microcontroladores para la comunicación en pacientes con ELA**

## 1. Resumen

La esclerosis lateral amiotrófica (ELA) limita progresivamente la capacidad de comunicación de los pacientes, sobre todo en fases avanzadas donde el habla y el control motor se ven gravemente afectados. Las interfaces cerebro-computadora (BCI) basadas en potenciales evocados, como el P300, han probado ser útiles como alternativa no muscular para la comunicación. Sin embargo, muchas de las soluciones actuales requieren hardware costoso o infraestructura compleja, lo cual limita su aplicación en contextos clínicos reales o de bajos recursos.

Este proyecto propone una solución accesible para la comunicación asistida en personas con esclerosis lateral amiotrófica (ELA), mediante un modelo de aprendizaje profundo ligero capaz de detectar potenciales P300 en señales EEG. A diferencia de los sistemas BCI convencionales, que requieren hardware especializado y costoso, esta propuesta se enfoca en la implementación sobre microcontroladores usando técnicas de TinyML.

Se trabajó con el estudio F del dataset público bigP3BCI, que contiene señales EEG de pacientes con ELA durante tareas de deletreo. Las señales fueron preprocesadas y etiquetadas para clasificar eventos como “target” o “non-target”. Se evaluaron dos arquitecturas: EEGNet, por su eficiencia en recursos, y DeepConvNet, por su capacidad expresiva.


## 2. Motivación

Los pacientes con ELA, especialmente en etapas avanzadas, enfrentan una pérdida casi total del habla y del movimiento, lo que hace que su única forma de comunicación sea mediante tecnologías asistidas. Si bien existen BCI comerciales, su costo y requerimientos técnicos los hacen poco viables en hospitales públicos o contextos con recursos limitados. Este proyecto nace de la necesidad de desarrollar una alternativa funcional  y portátil, que permita a estos pacientes comunicarse de forma efectiva usando su actividad cerebral.

## 3. Principales hallazgos 

- Se entrenó un modelo CNN ligero (EEGNet) capaz de detectar potenciales P300 en señales EEG de pacientes con ELA.

- El modelo alcanzó un 90 % de precisión y 80 % de recall.

- El tamaño final del modelo fue de 98 KB, compatible con microcontroladores y ejecución en tiempo real.

- La propuesta demostró que es posible implementar sistemas BCI de bajo costo sin sacrificar rendimiento, viables para entornos clínicos reales.


## Referencias
1. C. Wolfson, D. E. Gauvin, F. Ishola, y M. Oskoui, “Global prevalence and incidence of amyotrophic lateral sclerosis: A systematic review: A systematic review”, Neurology, vol. 101, núm. 6, pp. e613–e623, 2023. [Online].Available:https://pmc.ncbi.nlm.nih.gov/articles/PMC10424837/
2. C. Wolfson, D. E. Gauvin, F. Ishola, y M. Oskoui, “Global prevalence and incidence of amyotrophic lateral sclerosis: A systematic review: A systematic review”, Neurology, vol. 101, núm. 6, pp. e613–e623, 2023. [Online]. Available: https://pubmed.ncbi.nlm.nih.gov/34879411/
3. T. Makkonen, H. Ruottinen, R. Puhto, M. Helminen, y J. Palmio, “Speech deterioration in amyotrophic lateral sclerosis (ALS) after manifestation of bulbar symptoms”, Int. J. Lang. Commun. Disord., vol. 53, núm. 2, pp. 385–392, 2018. [Online]. Available: https://pubmed.ncbi.nlm.nih.gov/29159848/
4. D. Beukelman, S. Fager, y A. Nordness, “Communication support for people with ALS”, *Neurology Research International*, vol. 2011, art. e714693, 2011. [Online]. Available: https://doi.org/10.1155/2011/714693
5. J. Chmiel y M. Stępień-Słodkowska, “Resting-state EEG oscillations in amyotrophic lateral sclerosis (ALS): Toward mechanistic insights and clinical markers”, J. Clin. Med., vol. 14, núm. 2, 2025. [Online]. Available: https://www.mdpi.com/2077-0383/14/2/545
6. B. O. Mainsah et al., “Increasing BCI communication rates with dynamic stopping towards more practical use: an ALS study”, J. Neural Eng., vol. 12, núm. 1, p. 016013, 2015.[Online]. Available: https://pmc.ncbi.nlm.nih.gov/articles/PMC4631027/
7. N. Jin, L. Allison, X. Zhang, Y. Wang, T. Kaufmann, A. Kübler, and C. Neuper, “Increasing BCI Communication Rates with Dynamic Stopping,” Frontiers in Human Neuroscience, vol. 9, p. 207, 2015. [Online].Available:https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4631027/
8. C. Liu, M. Xiao, B. Wu, and J. Duan, “A P300-Detection Method Based on Logistic Regression and a Convolutional Neural Network,” Frontiers in Computational Neuroscience, vol. 16, 2022. [Online]. Available:https://www.frontiersin.org/articles/10.3389/fncom.2022.909553/full
9. J. Käthner, T. Halder, and A. Kübler, “A P300-based brain–computer interface for people with amyotrophic lateral sclerosis,” Clinical Neurophysiology, vol. 126, no. 3, pp. 645–655, 2015. [Online]. Available: https://pubmed.ncbi.nlm.nih.gov/25703940/
10. B. Mainsah, C. Fleeting, T. Balmat, E. Sellers y L. Collins, “bigP3BCI: An Open, Diverse and Machine Learning Ready P300‑based Brain‑Computer Interface Dataset (versión 1.0.0)”, PhysioNet, 19 de mayo de 2025. doi: 10.13026/0byy-ry86.
11. R. T. Schirrmeister, J. T. Springenberg, L. D. J. Fiederer, M. Glasstetter, K. Eggensperger, M. Tangermann, F. Hutter, W. Burgard, and T. Ball, “Deep learning with convolutional neural networks for EEG decoding and visualization,” Journal of Neural Engineering, vol. 14, no. 5, p. 056011, Aug. 2017. [Online]. Available: https://doi.org/10.1088/1741-2552/aace8c
12. R. T. Schirrmeister et al., “Deep learning with convolutional neural networks for EEG decoding and visualization”, Hum. Brain Mapp., vol. 38, núm. 11, pp. 5391–5420, 2017.
