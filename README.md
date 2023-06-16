# Ejercicio práctico Docker

Bienvenido a este ejercicio práctico en el que vamos a aprender los conceptos básicos de **Docker** y cómo **dockerizar** un servidor web con una página alojada de forma muy sencilla.<br>
En primera instancia vamos a configurar correctamente nuestro entorno de trabajo:<br>

## Índice
- [Configuración del Entorno](#configuraci%C3%B3n-del-entorno)
    * [Comprobación de las herramientas](#comprobaci%C3%B3n-de-las-herramientas)
    * [Instalación de las herramientas]( #instalaci%C3%B3n-de-las-herramientas)
        

# Configuración del entorno

Este ejercicio se va a realizar en un entorno **linux**, específicamente en un entorno **Ubuntu**, aprenderemos a utilizar Docker Engine mediante comandos.<br>

*Se recomienda utilizar una máquina virtual como entorno de trabajo, utilizaremos visual code como editor de texto para generar el .dockerfile, hay dos opciones:*
    -*En un entorno Linux con escritorio instalar visual code desde los propios repositorios de la distribución.*
    -*Instalar ssh en el entorno linux y utilizar visual code de forma remota desde windows u otro entorno a elección con el plugin propietario 'Remote - SSH'*

## Comprobación de las herramientas

En este apartado vamos a comprobar que herramientas tenemos instaladas.
*Comprobaremos la versión de cada una de las herramientas, si esta versión no aparece o el comando no se reconoce, no está instalada.*

* Comprobación de ssh:
    ```bash
    ssh -V
    ```
* Comprobación de git:
    ```bash
    git -v
    ```
* Comprobación de docker:
    ```bash
    docker -v
    ```

*En caso de que no tengas instalada alguna herramienta instalala con las instrucciones a continuación.*

## Instalación de las herramientas

1. Actualización de los repositorios:
    ```bash
    sudo apt update && sudo apt upgrade
    ```
<br>

2. Instalación de ssh:

    ```bash
    sudo apt install openssh-server
    ```

    *Habilitamos el servicio de ssh*

    ```bash
    sudo systemctl enable ssh
    ```

    *Arrancamos el servicio ssh*

    ```bash
    sudo systemctl start ssh
    ```

    *Comprobamos que el servicio esté levantado y funcionando*

    ```bash
    sudo systemctl status ssh
    ```
<br>

3. Instalación de git:

    ```bash
    sudo apt install git
    ```
<br>

4. Instalación de Docker en **Ubuntu**: --- [Docker Docs](https://docs.docker.com/engine/install/ubuntu/)
    * *Seteamos los repositorios de docker*

        ```bash
        sudo apt-get update
        sudo apt-get install ca-certificates curl gnupg
        ```

        ```bash
        sudo install -m 0755 -d /etc/apt/keyrings
        curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
        sudo chmod a+r /etc/apt/keyrings/docker.gpg
        ```

        ```bash
        echo \
        "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
        "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
        sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
        ```
    <br>

    * *Instalación de Docker Engine*
        ```bash
        sudo apt-get update
        ```
        ```bash
        sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
        ```

# Comenzamos el Ejercicio

### Qué vamos a hacer
En este ejercicio vamos a aprender a **dockerizar** un servicio web de forma simple.<br>
Veremos como crear un dockerfile, cómo manejarnos con docker por medio de comandos y por último cómo utilizar docker para hacer un despliegue rápido de cualquier servicio por medio de nuestras imágenes o imágenes de [dockerhub](https://hub.docker.com/)

## Elementos de Docker
En los contenedores **Docker** tenemos tres elementos bien diferenciados pero que a menudo pueden llevar a confusión.
1. **Archivos de construcción**: Los archivos de construcción son los ya mencionados **Dockerfiles**, son archivos que llevan las instrucciones para crear la **imagen** que posteriormente construirá el **contenedor**.
2. **Imagenes**: Las imágenes son paquetes ejecutables que contienen todo lo necesario para crear un **contenedor**, contiene el sistema operativo, las bibliotecas, los archivos de configuración y el código de la aplicación que vamos a ejecutar. Las imagenes son **portátiles** y muy **fáciles de compartir**, quí reside la fuerza de los contenedores.
3. **Contenedores**: Los contenedores son entornos de ejecución que utilizan la tecnología de virtualización, pueden confundirse fácilmente con una máquina virtual, aunque no son iguales. El contenedor es creado a partir de la Imagen, a lo mismo que cuando instalamos un sistema operativo, nos descargamos previamente su imagen .iso.

## Comandos básicos de Docker

* Descarga una **Imagen** de un repositorio.
    ```bash
    docker pull nombre_imagen
    ```
* Construye una **Imagen** a partir de un **Dockerfile**.
    ```bash
    docker build -t nombre_imagen ruta_directorio
    ```
* Ejecuta un **Contenedor** a partir de una imagen.
    ```bash
    docker run nombre_imagen
    ```
* Detiene un **contenedor** en ejecución.
    ```bash
    docker stop ID_contenedor
    ```
* Crea y ejecuta contenedores a partir de un **docker-compose**.
    ```bash
    docker-compose up
    ```
* Descarga una **Imagen** de un repositorio.
    ```bash
    docker pull nombre_imagen
    ```
* Construye una **Imagen** a partir de un **Dockerfile**.
    ```bash
    docker build -t nombre_imagen ruta_directorio
    ```
* Ejecuta un **Contenedor** a partir de una imagen.
    ```bash
    docker run nombre_imagen
    ```
* Lista las **imagenes** disponibles en el sistema.
    ```bash
    docker images
    ```
* Lista los **contenedores** que hay en ejecución:
    ```bash
    docker ps
    ```
* Lista todos los **contenedores** que hay en el sistema, los que se están ejecutando y los que no.
    ```bash
    docker ps -a
    ```
* Elimina una **imagen** del sistema.
    ```bash
    docker rmi nombre_imagen
    ```
* Elimina un **contenedor** del sistema.
    ```bash
    docker rm ID_contenedor
    ```
* Abre una terminal en el **contenedor** en ejecución que permite introducirle comandos de forma interactiva *-it*.
    ```bash
    docker exec -it ID_contenedor
    ```

```bash

```
