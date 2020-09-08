---
layout: post
title: Creación de una aplicación de ventas
---

En este post, muestro una aplicación básica de venta de productos, para la cual realizaremos un proceso muy simplificado de análisis, diseño y programación de la misma, para al final desplegarla en un entorno distribuido con kubernetes.

## Análisis de la aplicación

Crearemos una aplicación de ventas de productos para la empresa **TYRELL** (empresa ficticia por supuesto). Para lo cual nos serviría un poco de contexto sobre los productos que ofrecen:

_Esta es una empresa de tecnología con varios productos en su haber, en un principio enfocada en la creación de dispositivos para el uso gubernamental._

_En el último año ha destacado en el lanzamiento de dispositivos para el usuario común, como lo son teléfonos celulares, asistentes personales, audífonos y otros accesorios celulares._

_Dado el prestigio de la marca por tantos años, en los últimos meses han generado gran expectativa en los usuarios, los cuales esperan sus últimos 3 modelos de celular lanzados al mercado, así como su asistente personal. Estos productos se han convertido en los productos estrella y se espera una gran cantidad de ventas._

_En un principio se estarán lanzando estos productos, pero hay planes para cada 4 meses lanzar un producto nuevo, ya sea líneas de accesorios generales, accesorios gamer o bien otros gadgets._

_La empresa necesita una aplicación web que soporte una gran cantidad de visitas, que pueda ser visitada desde dispositivos móviles, que le permita al usuario una navegar con facilidad por los productos que ofrece._

_Esta aplicación se convertirá en el uno de los medios principales en los que se anunciarán nuevos productos_

De momento bastará con estos detalles para identificar los puntos que necesitará nuestro sistema.

En primer lugar, sobre los productos que ofrece, podríamos identificar lo siguiente. Ofrece 3 categorías de productos:

- Celulares: Con 3 modelos estrella
- Asistentes personales: Con 2 modelos principales
- Accesorios: audífonos, y otros accesorios gamer.

Sobre el comportamiento de la aplicación

- Se espera que cada 4 meses el catálogo de productos crezca
- Se espera gran cantidad de usuarios concurrentes
- Se espera que ofrezca anuncios sobre los próximos lanzamientos

Y las compras?

- De momento dejaremos de lado este gran tema.

Con esto en mente, y para los objetivos de esta serie de artículos, nos bastará con lo hasta ahora identificado. Así que, manos a la obra.

## ¿Qué? ¿Manos a la obra? y cómo piensas lograr eso? (Metodologías ágiles)

Sí, no podemos comenzar un nuevo proyecto sin tener bien definido qué es lo que vamos a hacer, o hasta dónde vamos a llegar, ¿en qué barco zarparemos?. Es necesario tomarnos el tiempo necesario para definir estos alcances, nuestro objetivo. Y para ello, hay diversas metodologías que nos recomiendan muchas cosas, las más famosas a este momento, las metodologías ágiles.

En este mismo blog encontrarás un post sobre las metodologías ágiles [aquí]({% post_url  2020-09-07-metodologias-agiles %}).

Para este proyecto utilizaremos un sistema basado en scrum y kanban (o scrumban), por lo que definiremos un backlog de macroactividades por realizar, para por cada una de ellas definir el análisis, diseño e implementación.

Utilizaremos para ello un herramienta que me gusta mucho y que se llama [Trello](https://trello.com). Esta nos ayudará a visualizar el proceso de desarrollo de nuestra aplicación con base en tarjetas, como con Kanban.

Las tareas principales se encuentran en Backlog, mientras que, el detalle para lograr completar esa macro-tarea la colocaré en "Cosas que hacer".

![](/assets/images/creacionAplicacion/trello_actividad1.png)



## Diseño de la aplicación

### Herramientas de diseño

En el mercado existen varias herramientas útiles en el proceso de desarrollo de aplicaciones, para cada fase del proyecto podemos encontrar distintas herramientas que podemos utilizar. Una de las fases más importantes en la planeación de nuestra aplicación es la generación de wireframes. Un wireframe es un esquema de la página, éste nos muestra los distintos componentes que se encontrarán en pantalla y cómo estarán funcionando entre ellos.

Puedes ver una descripción de algunas aplicaciones en este post: [7 principales herramientas de prototipado]({% post_url 2020-09-01-7-principales-herramientas-de-prototipado %})

En este proyecto, no nos enfocaremos en el detalle de colores, layouts complejos, y efectos deslumbrantes, por lo que usaremos [Balsamic Wireframes](https://balsamiq.com/wireframes/) como aplicación para generar los wireframes, esto nos dará de manera rápida la visión de qué es lo que desea el cliente sin enfocarnos aún en el detalle gráfico.

