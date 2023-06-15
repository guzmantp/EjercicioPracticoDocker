# Ejercicio práctico Docker

Bienvenido a este ejercicio práctico en el que vamos a aprender los conceptos básicos de **Docker** y cómo **dockerizar** un servidor web con una página alojada de forma muy sencilla.<br>
En primera instancia vamos a configurar correctamente nuestro entorno de trabajo:<br>

## Índice
- [Configuración del Entorno](#Configuración-del-entorno)
    * [Comprobación de las herramientas](##-Comprobación-de-las-herramientas)
    * [Instalación de las herramientas](##-Instalación-de-las-herramientas)
        

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






```bash

```
