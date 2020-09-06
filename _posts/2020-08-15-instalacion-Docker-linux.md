---
layout: post
title: Instalación de Docker en Linux
---

Instalación de una de las herramientas más importantes en el proceso de desarrollo de software.

## ¿Qué es Docker?

Docker es una plataforma de software que le permite crear, probar e implementar aplicaciones rápidamente. Docker empaqueta software en unidades estandarizadas llamadas **contenedores** que incluyen todo lo necesario para que el software se ejecute, incluidas bibliotecas, herramientas de sistema, código y tiempo de ejecución. Un contenedor es un conjunto de procesos separados del resto del sistema.

A diferencia de una máquina virtual, Docker no necesita que sea instalado un sistema operativo. Utiliza las funcionalidades proporcionadas por el kernel de Linux para poder aislar los recursos, como memoria, CPU, red, etc.

Como programadores, podemos utilizar Docker de distintas maneras. El principal uso de Docker es en la creación y gestión de sistemas altamente distribuidos utilizando contenedores Docker, pudiendo crear, copiar y mover contenedores de un entorno a otro y así optimizar las aplicaciones en la nube. Aprovechando estas ventajas, podemos crear contenedores Docker para aislar la ejecución de gestores de bases de datos, servidores de aplicaciones, entro otros cientos de cosas.

Es conveniente que visitemos la [página principal del proyecto](https://www.docker.com) para conocer a fondo de todo lo que nos ofrece.

## Instalación en linux

Los comandos que se describen a continuación han sido ejecutados en una distribución basada en Ubuntu, que es una de las más comúnmente utilizadas.

Primero, remover la versión existente, en caso de que por algún motivo el equipo que tengamos cuente con una instalación vieja.

```bash
$ sudo apt-get remove \
    docker \
    docker-engine \
    docker.io \
    containerd \
    runc
```

Instalamos los paquetes actualizados necesarios

```bash
$ sudo apt-get update
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common
```

Agregamos las claves correctas y verificamos

```bash
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo apt-key fingerprint OEBFCD88

pub   rsa4096 2017-02-22 [SCEA]
      9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
sub   rsa4096 2017-02-22 [S]
```

Agregamos el repositorio

```bash
$ sudo apt-add-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
```

Instalamos Docker

```bash
$ sudo apt-get update
$ sudo apt-get install docker-ce
```

## Ejecutar Docker si ser super usuario

Cuando ejecutamos docker por primera vez, cualquier comando que ejecutemos (por ejemplo `docker ps -a`) nos estará indicando que no tenemos permisos para ejecutarlo, con un mensaje como: `Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock:`.

Para corregir esto, ejecutamos el siguiente comando

```bash
$ sudo usermod -aG docker ${USER}
```

Hecho esto, deberemos cerrar la sesión y volver a inciarla.

## Habilitar acceso remoto por TCP

Es posible habilitar el acceso al API de nuestra instalación de docker. Para ello, debemos de seguir estos pasos:

Crear un archivo en `/etc/systemd/system/docker.service.d/startup_options.conf` con las siguientes líneas

```bash
# /etc/systemd/system/docker.service.d/override.conf
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H fd:// -H tcp://0.0.0.0:2376
```

Recargar los archivos:

```bash
$ sudo systemctl daemon-reload
```

Reiniciar Docker con las nuevas opciones

```bash
sudo systemctl restart docker.service
```

## Integración con eclipse

Docker puede ser usado con eclipse, para lo cual sólo es necesario ir a Marketplace y buscar Docker.

Estas herramientas nos permiten ver varias cosas, según la perspectiva que utilicemos.

En una máquina remota que esté ejecutando Docker, será necesario que esté habilitada la conexión a través del API como se indicó en el punto anterior.

En la pestaña de Docker explorer podremos agregar una conexión.

![Conectar con Docker](https://1.bp.blogspot.com/-Mn7o4VhjoOc/XzneWX3Uk-I/AAAAAAAAIjI/GVI77eSjUiwiKqiRPORZf5SzaLRKtunXACPcBGAYYCw/s1048/003_instalacionDocker_conectarDocker.png)

Al completar la configuración, podremos ver los contenedores, imágenes y demás info de nuestro servidor con Docker.

![Info de servidores](https://1.bp.blogspot.com/-ZprCCyOaAXs/XznfGl11MmI/AAAAAAAAIjQ/m5ze-4SpJNc30IiyGMTU7QTP6ldpOV3dQCPcBGAYYCw/s1696/1b63979ad643471fa3c880618d650e8a.png)

## Imagen vs Contenedor

La imagen es una distribución, cuando se toma una imagen y se ejecuta, se convierte en un contenedor.

Es decir, la imagen es el binario, y el contenedor es la ejecución.

Imagen → Plantilla

Contenedor → Objeto que instancia una plantilla

## Instalando imágenes

Comunmente las imágenes se pueden descargar del [hub de Docker](https://hub.docker.com), por ejemplo, como indica la página de docker hub para [wildfly](https://hub.docker.com/r/jboss/wildfly/)

Bajando la imagen:

```bash
doker pull jboss/wildfly
```

Iniciando la imagen

```bash
docker run -it jboss/wildfly
```
### Instalando imágenes desde eclipse

Podemos descargar la imagen desde eclipse en la ventana de Docker explorer y después hacer el pull.
![](https://1.bp.blogspot.com/-6nkbhfZT-kU/XznhLaw39WI/AAAAAAAAIjg/utUcNGRLqK8-HE6ymfB0TO3udQCOSigdQCPcBGAYYCw/s646/8d4f89000eec43bcb24598d8138b0a78.png)

Donde podemos buscar la imagen. Para nuestro ejemplo haremos la instalación de un servidor de base de datos SQL Server.
![](https://1.bp.blogspot.com/-pq6wIG-JSQg/XznhZlrisHI/AAAAAAAAIjs/Tb6KmGc-VLcZFigiv5ii-KOxWuTnS1xJACPcBGAYYCw/s1058/44267a62fb1144e3a3f7a12fcfea6ffa.png)

![](https://1.bp.blogspot.com/-c-SCnzlohms/XznhfRXN_FI/AAAAAAAAIjw/sFediz830nYtq95ADutsx1mlbh77A8r9gCPcBGAYYCw/s1058/422f65a9ea764e29a78ebc9b6e5421d6.png)

![](https://1.bp.blogspot.com/-XxSY0Fur5uk/XznhmddVNQI/AAAAAAAAIj4/CERavUzHZGcWAp0IxSC5jD2d3qlj2dPvgCPcBGAYYCw/s1044/4e69a258afed4608a5499de374ba9d22.png)

Si deseamos correr la imagen que acabamos de descargar desde eclipse, podemos hacerlo con la herramienta propia de eclipse: run

![](https://1.bp.blogspot.com/-D-fiPfqgAOM/XznhwTiCqoI/AAAAAAAAIj8/xBhMuWw_MOgo7OHpbKPk1_45wIwqz3oJwCPcBGAYYCw/s1436/fa8be86dd254488298e7add727876a3c.png)
La pantalla siguiente nos permite colocar parámetros o variables de entorno, necesarios para poder ejecutar a modo la imagen que descargamos.

Por ejemplo, para la imagen que descargamos, [la documentación](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker?view=sql-server-ver15&pivots=cs1-bash) nos indica algunas variables:

![](https://lh3.googleusercontent.com/-1I9kT8OhnNY/XznjKCpveSI/AAAAAAAAIkE/AXX2vFg3rZ85jMxKTxHqxggsx5zAcDeJgCLcBGAsYHQ/h240/c3e48559b60c42e19656d068800189df.png)

![](https://1.bp.blogspot.com/-wVWBwc6KhO8/XznjYCDa5_I/AAAAAAAAIkQ/oIx0SxTx0fE-S99bzlt5oiMSj7c44ykUACPcBGAYYCw/s1436/d5bb558ea49f4c048eaa501f5113d1bc.png)

![](https://1.bp.blogspot.com/-je5jb31vmbc/Xznjh0VrY_I/AAAAAAAAIkY/ScNKwCmpQ0Mp8plgHEVh--uIYPla8oWPQCPcBGAYYCw/s1452/57d04baffc94454da664b78a12dfe630.png)

![](https://1.bp.blogspot.com/-YXgOZQM2yts/XznjvDVgXrI/AAAAAAAAIkc/2sI_aCgqFVYRVWmEgl-U6sZLXkF3s67agCPcBGAYYCw/s1452/fc7c3cf5c1704ea9aa8820f2ce465f21.png)

Al término de levantar la imagen, y crear el contenedor, podremos conectarnos a este servidor (contenedor Docker)
![](https://lh3.googleusercontent.com/-GLnINDZfFJM/XznkELwxgrI/AAAAAAAAIkg/D7YX0-HK8fQPPjKlwJdc0IdlO5t2XYPwQCLcBGAsYHQ/h240/56db0c621b6e46d99b6e5cbedb60b015.png)

Utilizando un cliente de base de datos, podremos establecer la conexión al servidor que acabamos de instalar.
![](https://1.bp.blogspot.com/-WYNQGVfpzDs/XznkVNrM1_I/AAAAAAAAIks/qW5U0N7bjnoQTzhvjZscCat3yDqAQA-rwCPcBGAYYCw/s1170/eece7a75782a464296d241d33438a741.png)

## Comunicar 2 contenedores

Es posible comunicar nuestros contenedores, ya sea que un servidor se conecte a una base de datos, 2 servidores de aplicaciones, etc.

Desde eclipse, se puede hacer al momento de ejecutar la imagen.

![](https://1.bp.blogspot.com/-hneO5eZuLgw/Xznl7tCPPkI/AAAAAAAAIk0/OLByByD_Bzo8w5pxjIRcxhmtWDwA6FwogCLcBGAsYHQ/s1308/723081f3c8e94c0ca544b7327396d1cb.png)

Esto, hará que se ejecute otra imagen (en este caso un tomcat) que tiene acceso al otro contenedor a través del alias que se indicó.

![](https://1.bp.blogspot.com/-W0tw7MCP4ec/XznmcqGyMMI/AAAAAAAAIk8/kzT6nR5glpovtinhXEfuWM2T9QhFZHMfQCLcBGAsYHQ/s1154/b509021888984497823f5485ee46e4a0.png)

![](https://1.bp.blogspot.com/-v80S7icquTU/XznmzvyBBsI/AAAAAAAAIlE/RWWNHTTb2xk-uHwb2Lyj0899nfOjcJkzgCLcBGAsYHQ/s864/fc10e2ae134f47e3a963fe822735bd0d.png)

Lo que hace docker al ejecutar estas imágenes, es que se crea en el archivo etc/hosts una entrada donde mapea el nombre del alias con la io que le asigna.

## Comandos útiles

ver la lista de imágenes

```bash
docker image ls
```

Ver las imágenes que se están ejecutando

```bash
doker ps -a
```

gestionar un volumen ejecutar una imagen

```bash
docker run -it --name wildfly -p 8080:8080 -v /usr/proyectos/docker/wild:/opt/wildfly/standalone/deployment
```

Entrar a un contenedor con linea de comandos

```bash
docker exec -it mssql-test bash
```

referenciar un contenedor desde otro

```bash
docker run -it --name tomcat --link mssql-test:mssql-link tomcat:tomcat-9.0.22
```

ver logs de un contenedor

```bash
docker logs -f tomcat-9.0.22
```

ver la ip de un contenedor

```bash
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container_name_or_id
```
