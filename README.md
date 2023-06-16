# Ejercicio práctico Docker

Bienvenido a este ejercicio práctico en el que vamos a aprender los conceptos básicos de **Docker** y cómo **dockerizar** un servidor web con una página alojada de forma muy sencilla.<br>
En primera instancia vamos a configurar correctamente nuestro entorno de trabajo:<br>

## Índice
- [Configuración del Entorno](#configuracin-del-entorno)
    * [Comprobación de las herramientas](#comprobaci%C3%B3n-de-las-herramientas)
    * [Instalación de las herramientas]( #instalaci%C3%B3n-de-las-herramientas)
- [Conozcamos un poco de Docker](#conozcamos-un-poco-de-docker)
    * [Qué vamos a hacer](#qu%C3%A9-vamos-a-hacer)
    * [Elementos de Docker](#elementos-de-docker)
    * [Comandos básicos de Docker](#comandos-b%C3%A1sicos-de-docker)
- [Comenzamos el ejercicio](#comenzamos-el-ejercicio)
    * [Creación del dockerfile](#creaci%C3%B3n-del-dockerfile)
    * [Creación del dockerignore](#creaci%C3%B3n-del-dockerignore)
    * [Creamos el contenedor](#creamos-el-contenedor)



![Logo Docker](https://1000logos.net/wp-content/uploads/2021/11/Docker-Logo-2013.png)<br>


# Configuración del entorno

Este ejercicio se va a realizar en un entorno **linux**, específicamente en un entorno **Ubuntu**, aprenderemos a utilizar Docker Engine mediante comandos.<br>

*Se recomienda utilizar una máquina virtual como entorno de trabajo, utilizaremos visual code como editor de texto para generar el dockerfile, hay dos opciones:*
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

# Conozcamos un poco de Docker

### Qué vamos a hacer
En este ejercicio vamos a aprender a **dockerizar** un servicio web de forma simple.<br>
Veremos como crear un dockerfile, cómo manejarnos con docker por medio de comandos y por último cómo utilizar docker para hacer un despliegue rápido de cualquier servicio por medio de nuestras imágenes o imágenes de [dockerhub](https://hub.docker.com/)

## Elementos de Docker
En los contenedores **Docker** tenemos tres elementos bien diferenciados pero que a menudo pueden llevar a confusión.
1. **Archivos de construcción**: Los archivos de construcción son los ya mencionados **Dockerfiles**, son archivos que llevan las instrucciones para crear la **imagen** que posteriormente construirá el **contenedor**.
2. **Imagenes**: Las imágenes son paquetes ejecutables que contienen todo lo necesario para crear un **contenedor**, contiene el sistema operativo, las bibliotecas, los archivos de configuración y el código de la aplicación que vamos a ejecutar. Las imagenes son **portátiles** y muy **fáciles de compartir**, quí reside la fuerza de los contenedores.
3. **Contenedores**: Los contenedores son entornos de ejecución que utilizan la tecnología de virtualización, pueden confundirse fácilmente con una máquina virtual, aunque no son iguales. El contenedor es creado a partir de la Imagen, a lo mismo que cuando instalamos un sistema operativo, nos descargamos previamente su imagen .iso.

En este ejercicio no vamos a entrar en más profundidad de todas las partes que tiene docker, pero si tienes curiosidad y quieres seguir investigando te dejo algunos conceptos extras que seguro que te mantendrán entretenido un ratito más ;)
* **Volúmenes**: Seguro que te son muy útiles si quieres crear una base de datos o compartir recursos.
* **Docker compose**: Esto está chulisimo, mucho mucho, ¿Te imaginas poder levantar varios contenedores de un plumazo?
* **Redes de docker**: Esto es más avanzado aún, pero mereze la pena echarle un vistacito.

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

# Comenzamos el ejercicio

Para este ejercicio vamos a utilizar una imagen ya creada de [Apache](https://hub.docker.com/_/httpd) de **DockerHub**. En primer lugar crearemos el dockerfile para la creación de la imagen, en segundo lugar configuraremos un dockerignore muy sencillito para evitar que se copie el README.md de este repositorio y por último crearemos la imagen y levantaremos nuestro contenedor con el servidor web listo para ser utilizado.

## Creación del dockerfile
Como ya hemos descrito anteriormente, el dockerfile es un archivo que determina cómo se va a construir nuestra imagen. El primer paso que se suele dar en un dockerfile es determinar cual va a ser el sistema operativo base que vamos a utilizar en el contenedor, como en este caso vamos a utilizar una imagen ya creada, no necesitamos especificar el so, ya que viene integrado en la imagen base que vamos a utilizar, aunque si que es buena práctica indicarle, en caso de que tenga varias versiones, cual vamos a utilizar, así nos evitamos problemas de incompatibilidades en un futuro. En este caso indicaremos la versión de apache a utilizar y como está construida con varios so, también indicaremos el so a utilizar.<br>
Creamos un archivo y lo nombramos asi: 'dockerfile'
* Indicamos la imagen base a utilizar:
   ```dockerfile
   FROM httpd:2.4.57-alpine
   ```
Acto seguido tendremos que copiar todos los archivos que componen la web al directorio que utiliza apache. En la primera ruta ponemos un punto para indicar que el contenido que queremos copiar se encuentra en la misma ubicación del dockerfile y acto seguido ponemos la ruta donde queremos copiar los archivos dentro del contenedor. **MUY IMPORTANTE** Estamos trabajando con entornos separados, es decir, la primera ruta hace referencia a nuestra máquina local y la segunda hace referencia al contenedor, el cual tiene otra estructura de directorios y archivos.
* Copiar archivos al direcorio base de Apache.
   ```dockerfile
   COPY . /usr/local/apache2/htdocs/
   ```

## Creación del dockerignore
El dockerignore, a lo mismo que el gitignore, es un archivo que indica que directorios o ficheros tinene que ignorar docker a la hora de trabajar, así que en este caso lo necesitaremos para no copiar el README.md que contiene este repositorio. En este ejemplo se fuerza un poco a utilizarlo para un primer contacto con el, pero realmente sería muy fácil solventarlo sin un dockerignore, tendríamos dos opciones:
* Nos cargamos el README.md :)
* Metemos toda la web en un directorio y modificamos la ruta del dockerfile para que únicamente copie los archivos de esa carpeta.

Para marear un poco la perdíz, vamos a crearlo de todas las maneras:
Creamos un archivo y le ponemos de nombre 'dockerignore'
* Ponemos el nombre del archivo que queremos ignorar:
   ```dockerignore
   README.md
   ```
En este caso únicamente tenemos que descartar un archivo, pero debajo os dejo otras formas de ignorar elementos por si lo necesitais:
* Ignorar archivos con extensión .txt
   ```dockerignore
   *.txt
   ```
* Ignorar directorios llamados 'datos':
  ```dockerignore
  datos/ 
  ```
* Ignorar todos los archivos del directorio 'archivos_temporales':
   ```dockerignore
   archivos_temporales/*
   ```
## Creamos el contenedor
Por fín llegamos a lo bonito, que es ver como todo empieza a funcionar :)
Como primer paso tenemos que abrir una terminal y posicionarnos en el directorio donde tenemos el dockerfile. Una vez estemos ahí, ejecutamos el **build**.
```bash
sudo docker build -t servidor_apache .
```
Una vez tengamos la imagen creada podremos verla ejecutando:
```bash
sudo docker images
```
Para crear el contenedor lo único que debemos de hacer es ejecutar el **run**. En el propio comando exponemos el puerto 80 del contenedor y de nuestra máquina para poder acceder al servidor.
```bash
sudo docker run -p 80:80 servidor_apache
```
<br>

## Accedemos a nuestro servidor
Por último, únicamente quedaría comprobar en una terminal si nuestro contenedor esta ejecutándose, para comprobarlo introducimos este comando en la terminal:
```bash
sudo docker ps
```
Si nuestro contenedor está ejecutandose correctamente aparecerá listado en nuestra terminal.
<br>
Por último, abrimos un navegador web y accedemos al servidor a través de él, los contenedores se ejecutan en local, por lo que si accedes desde la propia máquina virtual tendrás que acceder a través de **localhost:80** si en cambio, quieres acceder desde otro lado, tendrás que especificar la dirección ip de la máquina host, indicando el puerto.

<br><br>
Esperamos que os haya servido de ayuda para descubrir lo que es docker y que os haya proporcionado un poco de curiosidad para seguir aprendiendo esta tecnología.
<br>
Gracias.

   

