# Laboratorio 1 - Creación de Repositorio en Git
## Creación de Repositorio Local
### 1. Abrir la consola de comandos
### 2. Escoger la ruta del directorio donde se va a crear el repositorio con el comando "cd (ruta del directorio)"
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 1/Lab1-Ruta.png">
### 3. Inicializar el repositorio local con el comando "git init"
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 1/Lab1-IniciarLocal.png">

## Creación de Repositorio Remoto
### 1. Crear repositorio en https://github.com/, hacer el repositorio público y desmarcar la opción "Include README.md"
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 1/Lab1-CrearRemoto.png">
### 2. Copiar el link del repositorio creado, debe ser como: "https://github.com/Gabriel-Bms/RDP-2025-1.git"

## Enlazar Repositorio Local con el remoto
### 1. En la consola de comandos usar "git remote add origin (Link del repositorio remoto">
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 1/Lab1-Enlazar.png">
### 2. Verificar con "git remote -v", se deberia obtener la siguiente salida
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 1/Lab1-VerificarRemoto.png">

## Crear estructura de arhcivos en el repositorio local
### 1. Crear las carpetas "Proyecto", "Laboratorios", "Certificados" y el archivo README.md
### 2. Incluir un archivo de texto o markdown en cada subcarpeta, ya que GitHub no maneja carpetas vacias.
### 3. Verificar que la estructura creada es la deseada con "tree /F"
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 1/Lab1-Estructura.png">
### 4. Crear la rama principal con "git branch -M (nombre de rama principal)"
### 5. Añadir los archivos creados al repositorio con "git add ."
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 1/Lab1-CrearMain.png">

## Enviar los cambios al Repositorio remoto
### 1. Guardar los cambios realizados con "git commit -m (Nombre del cambio)"
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 1/Lab1-Commit.png">
### 2. Enviar los cambios con "git push -u origin (Nombre de rama)"
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 1/Lab1-Send.png">
### 3. Verificar cambios en GitHub
<image src="https://github.com/Gabriel-Bms/GRUPO3-ISB-2025-I/blob/master/Imagenes/Laboratorio 1/Lab1-Final.png">

## Obtener los cambios del Repositorio remoto
1. En el caso de que la estructura de archivos se haya creado en GitHub, se pueden sincronizar con el repositorio local con "git pull origin (nombre de rama)"
2. Si se realiza algun cambio en el repositorio remoto, y luego se cambia algo en el local, primero se deben sincronizar los cambios del remoto con "git pull" y luego enviar los cambios del local con "git push"
