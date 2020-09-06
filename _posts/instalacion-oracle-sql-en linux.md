---
layout: post
title: Instalación de Oracle SQL en linux
---

Uno de los sistemas de gestion de bases de datos más usados en las empresas es **Oracle Database**. Éste está disponible para una gran cantidad de sistemas operativos, aunque muchas veces la instalación de la suite completa no es tan fácil de realizar. En este post explicaré cómo realizar la instalación en un sistema linux utilizando Docker.

## Instalación sencilla

Una de las constantes sugerencias, y de las que más razón tienen, en el desarrollo de sistemas, es que los componentes en los que sea probada la aplicación sean lo más parecidos al entorno poductivo en el que se van a instalar finalmente. Sin embargo, hay ocasiones en las que necesitamos disponer de un sistema sencillo, quizá en el que probar localmente, desarrollar algún componente que necesitamos aislar, probar scripts en un entorno controlado, pueden ser muchas las razones por las que necesitemos un entorno más inmediato. Este es el objetivo de esta pequeña guía, proporcionar los pasos necesarios para realizar una instalación simple y funcional.

Esta instalación la realizaremos en un sistema linux, es necesario que hayamos instalado Docker previamente (puedes guiarte con el [post ubicado en este mismo blog]({% post_url 2020-08-15-instalacion-Docker-linux %})). Incluso en este se muestra un ejemplo rápido de instalación de MS-SQL Server.

Hecho esto, el proceso secillo es el siguiente:

Debemos tener una cuenta de [docker hub](https://hub.docker.com), cuando tengamos la cuenta, debemos iniciar sesión en nuestra terminal.

```bash
$ docker login
```

Debemos descargar la imagen correspondiente

```bash
$ docker pull store/oracle/database-enterprise:12.2.0.1
```
