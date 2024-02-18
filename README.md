# Taller 2: Despliegue de TensorFlow Extended (TFX) con Docker y Docker Compose

## Estudiantes
Juan David Torres Jimenez
William David Prada Buitrago
Ricardo Macias Bohorquez

## Descripción
El proposito del taller es generar la configuración y el despliegue de un ambiente de desarrollo para proyectos de Machine Learning utilizando TensorFlow Extended (TFX), haciendo uso de Docker y Docker Compose para facilitar el proceso. Se explorará el despliegue de una imagen pre-construida de TensorFlow en un contenedor Docker, accediendo a Jupyter Notebook para ejecutar ejemplos prácticos de TensorFlow Data Validation (TFDV) y ML Metadata.

## Requisitos Previos
- Docker y Docker Compose instalados en el sistema.
- Conocimientos básicos de Docker, Docker Compose, y línea de comandos de Unix/Linux.
- Familiaridad con TensorFlow y conceptos básicos de Machine Learning.

## Configuración de Docker Compose
Para simplificar el proceso de despliegue, convertiremos el comando Docker proporcionado

```bash
sudo docker run -it --name tfx --rm -p 8888:8888 -p 6006:6006 -v $PWD:/tfx/src --entrypoint /run_jupyter.sh  tensorflow/tfx:1.12.0
```

 en una configuración de Docker Compose. Siga los pasos a continuación para configurar y utilizar Docker Compose.

### Paso 1: Creación del Archivo `docker-compose.yml`
Cree un archivo llamado `docker-compose.yml` en el directorio de su proyecto con el siguiente contenido:

```yaml
version: '3'
services:
  tfx:
    image: tensorflow/tfx:1.12.0
    ports:
      - "8888:8888"
      - "6006:6006"
    volumes:
      - "$PWD:/tfx/src"
    entrypoint: /run_jupyter.sh
    stdin_open: true
    tty: true
    container_name: tfx
    restart: "no"
```

Este archivo de configuración replica el comando Docker proporcionado, estableciendo un contenedor para TensorFlow Extended con el nombre `tfx`, y mapeando los puertos y volúmenes necesarios para el taller.

### Paso 2: Iniciar el Contenedor
En el directorio donde se encuentra el archivo `docker-compose.yml`, ejecute el siguiente comando para iniciar el contenedor:

```bash
sudo docker-compose up
```

### Paso 3: Acceso a Jupyter Notebook
Una vez el contenedor esté en ejecución, acceda a Jupyter Notebook navegando a `http://localhost:8888` en su navegador. Utilice los notebooks proporcionados en clase para explorar TFDV y ML Metadata. (para ingresar es indispensable tomar el token que se genera al momento de finalizar el proceso de inciación del contenedor)