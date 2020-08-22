---
layout: post
title: Habilitar acceso por ssh a un equipo linux
---

Como parte de nuestros proyectos, siempre tenemos que conectarnos a distintos equipos que desempeñan distintos roles en nuestro proceso de desarrollo, ya sea un servidor de aplicaciones, un servidor de base de datos, almacén de contenidos, etc. Unas de las formas más comunes de conectarnos a estos es a través de ssh.

## ¿Qué es SSH?

SSH significa Secure Shell, y es un protocolo de comunicación que da acceso a un servidor, utilizando un canal seguro, ya que usa técnicas de cifrado para que lo que viaja a través de la conexión no sea legible.

Además de ser un protocolo, el programa que nos permite establecer esta conexión también tiene este nombre.

## OpenSSH

OpenSSH es el conjunto de herramientas que nos permitirán realizar la conexión entre 2 equipos, programado por el equipo de OpenBSD, éste ha sido portado a gran cantidad de sistemas operativos, y por supuesto los principales cuentan con una versión para instalarse.

Las herramientas que contiene esta suite nos permite tanto establecer la conexión cifrada con un servidor que implemente este protocolo, como servir de servidor ssh como tal, podemos configurar parámetros de utilización, generar llaves, etc.

## Instalación 

Como comentamos, existen paquetes para la mayoría de los sistemas existentes. En un sistema basado en Linux es muy probable que ya se encuentren agregados a las listas de paquetes permitidos para instalación.

En un sistema basado en Debian, podemos hacer la instalación con el siguiente comando:

~~~bash
sudo apt-get install openssh-server
~~~

![instalando openssh](https://lh3.googleusercontent.com/-Khex4p5qyFY/Xzi5b68EZqI/AAAAAAAAIiQ/jJsG0E5YLPMfshn26owhBF2VKIFmTa2ZQCLcBGAsYHQ/h240/Captura%2Bde%2BPantalla%2B2020-08-15%2Ba%2Bla%2528s%2529%2B23.41.31.png)

Ahora debemos habilitar el servicio.

~~~bash
sudo systemctl enable ssh
~~~

Y posteriormente iniciarlo

~~~bash
sudo systemctl start ssh
~~~

Para poder establecer una conexión básica entre computadoras, bastará con realizar la instalación, pero, si se desea establecer parámetros más específicos, deberás leer más sobre la configuración y entender cómo funciona la comunicación, a fin de sacarle el mayo provecho a ésta.

## Conexión a equipo remoto

Ya que tenemos habilitado el servidor ssh y éste se encuentra en ejecución, desde nuestro equipo podemos establecer la conexión con el siguiente comando:

~~~bash
ssh <usuario>@<ip.del.equipo>
~~~

![conexión al equipo](https://lh3.googleusercontent.com/-tmSmNWSu92w/Xzi_zm9CfLI/AAAAAAAAIic/Q9CbXv1j1JYjRg_JWuMXxsNqlsnZhOBXgCLcBGAsYHQ/h240/Captura%2Bde%2BPantalla%2B2020-08-16%2Ba%2Bla%2528s%2529%2B0.07.52.png)

Nos pedirá la contraseña del usuario y con eso nos dará el prompt del sistema operativo al que hemos accedido. A partir de ahora, las instrucciones que coloquemos en este terminal serán ejecutadas en el servidor.

Para desconectarnos, simplemente la instrucción:

~~~bash
exit
~~~

cerrará le conexión establecida.

Una muy buena documentación sobre este protocolo y herramientas se encuentra disponible [aquí](https://web.mit.edu/rhel-doc/4/RH-DOCS/rhel-rg-es-4/ch-ssh.html)