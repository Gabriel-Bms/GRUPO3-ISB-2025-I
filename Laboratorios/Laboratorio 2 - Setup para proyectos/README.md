# Laboratorio 2 - Setup para proyectos
## Instalar un gestor de paquetes (conda, PIP)
### 1. En este caso, se utilizara Anaconda, que incluye el gestor de paquetes conda y un entorno predeterminado "base", con multiples librerias preinstaladas
### 2. Crear un entorno virtual especifico para los proyectos a desarrollar en el curso, definir la version de Python a usar
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 2/Lab2-CrearVenv.png">

### 3. Para modigicar el entorno creado, activamos el entorno
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 2/Lab2-ActivarVenv.png">
  
### 4. Verificar que el entorno se creo correctamente
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 2/Lab2-VerificarVenv.png">
  
### 5. Instalar las librerias básicas para análisis, procesado y visualización de datos en el entorno creado
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 2/Lab2-InstalarLibrerias.png">



### 6. Escoger el IDE, Anaconda incluye Jupyer Notebook, Jupyter Lab y Spyder, tambien es compatible con VSCode, en este caso usaremos Jupyter Notebook
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 2/Lab2-InstalarJupyter.png">

### 7. Abrimos Jupyter desde el Conda Prompt
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 2/Lab2-AbrirJupyter.png">

### 8. Creamos el primer cuaderno ipynb
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 2/Lab2-CrearIpynb.png">

### 9. Verificar que estamos trabajando en el entorno correcto y que las librerias estan instaladas correctamente
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 2/Lab2-VerificarLibrerias.png">

## Código para plotear 2 señales EMG y 2 señales ECG simuladas

### 1. Importamos las librerías necesarias para el análisis como numpy, pandas, scipy, sklearn y el neurokit2 para la simulación de señales. Además verificamos las librerías y que nos encontremos en el entorno virtual correcto
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 2/1.png">
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 2/2.png">

### 2. Importamos la librería matplotlib.pyplot para graficar las señales y la función welch para el cálculo del PSD
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 2/3.png">
  
### 3. Definimos los parámetros de frecuencia de muestreo y duración 
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 2/4.png">
  
### 3. Simulación de la primera señal EMG: Generamos 7 explosiones de actividad muscular con duraciones aleatorias entre 0.1 y 0.5 segundos.
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 2/5.png">

### 4. Simulación de la segunda señal EMG: Generamos 3 explosiones de actividad muscular con duraciones aleatorias entre 0.2 y 0.6 segundos.
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 2/6.png">

### 5. Simulación de las dos señales ECG: La pimera con frecuencia cardíaca de 60 bpm y la segunda con 90 bpm y se les añadió un ruido de 0.01 y 0.05 respectivamente 
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 2/7.png">

### 6. 
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 2/8.png">
  
### 7.
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 2/9.png">

### 8. imagen del emg
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 2/10.png">

### 9. imagen de ecg
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 2/11.png">
