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

## Análisis y diseño del modelo de datos

Es momento de identificar las propiedades de los productos que vamos a presentar en pantalla, y por ende que almacenaremos en una base de datos; pero a demás de eso, las demás entidades que estarán participando, promocionales, categorías de productos, subcategorías, etc.

Listemos simplemente los posibles atributos que podrían tener estos

Producto
    - sku
    - nombre
    - descripción general
    - detalle
    - precio
    - imagen
    - categoría
    - sub-categoría
    - stock


Categoría de producto
    - nombre
    - descripción
    - imagen

Sub-categoría
    - nombre
    - descripción
    - imagen

### Diseño

Para el proyecto que estamos realizando, y la cantidad de productos que se estarán manejando en el sistema, nos podría bastar con una simple base de datos relacional, pero a efectos de aprendizaje y ponernos interesantes, nuestra base de datos será no relacional, y usaremos para ello MongoDB.

Al ser una base de datos no relacional, no modelamos de acuerdo a entidad-relación, para esto usaremos UML. Nuestro modelo simple quedaría así:

![Modelo de datos](/assets/images/creacionAplicacion/modeloDatos.png)


## Instalación de MongoDB

La instalación de MongoDB es umy sencilla, existen instaladores para  distintos sistemas operativos, pero nosotros la vamos a instalar sobre Docker.

En este mismo sitio puedes encontrar un artículo sobre la instalación de Docker [aqui]({% post_url 2020-08-15-instalacion-Docker-linux %}).

En particular, la instalaré en un equipo linux remoto, que hará las funciones de servidor, por lo que me conectaré por ssh. Para habilitar ssh en linux puedes revisar [este post]({% post_url 2020-08-05-Habilitar-ssh-linux %}).

Me conecto por ssh al servidor:

```bash
ssh alan@192.168.56.101 
```

Para entonces descargar la imagen de mongo:

```bash
docker pull mongo
```

![obtener imagen de mongo](/assets/images/creacionAplicacion/01_obtenerImagenMongo.png)

Terminada de descargar la imagen, vamos a montarla. De nombre le daré tyrell, pero puedes darle el mejor nombre que te parezca. Los puertos son los típicos de una instalación de mongo.

```bash
docker run -d -p 27017:27017 --name tyrell mongo:latest
```

Ejecutemos ahora un bash en el contenedor desplegado. Recuerda que tyrell fue el nombre que yo le dí.

```bash
docker exec -it tyrell  bash
```

En el bash que nos dió el contenedor iniciamos mongo.

```bash
mongo
```

![MongoDB corriendo](/assets/images/creacionAplicacion/02_ejecutarMongo.png)

Ahora que sabemos que mongo está ejecutándose, ya podríamos crear bases de datos, ejecutar consultas, crear documentos y demás, pero, no lo haremos desde la línea de comandos, usaremos una aplicación un poco más amigable que se llama [Robo 3T](https://robomongo.org).

Robo 3T nos presenta al inicio la interfaz para poder administrar las conexiones.

![Robo3T](/assets/images/creacionAplicacion/03_instlacionRobo3T.png)

Le damos 'Crear' y colocamos los datos de nuestro servidor.

![Alta de conexión](/assets/images/creacionAplicacion/04_altaConexionRobo3T.png)

En la pantalla principal, podremos ahora crear una base de datos para nuestro proyecto Tyrell. Dando clic derecho en la raíz  del árbol, seleccionamos crear.

![Crear base de datos](/assets/images/creacionAplicacion/05_crearDatabase.png)

Demos nombre a la base de datos.

Y ahora, creemos el modelo que ya pensamos anteriormente.

Debemos crear una colección, en la cual se almacenarán nuestros productos,(nombremoslo productos) luego, sobre esa colección vamos a insertar un documento.

![Crear documento](/assets/images/creacionAplicacion/06_creacColeccion.png)

En el contenido del documento a insertar colocaremos una estructura que corresponda a lo que diseñamos.

![Insertar documento](/assets/images/creacionAplicacion/07_insertarDocumento.png)

Con las actividades realzadas hasta el momento, hemos avanzado en la creación de este módulo. Cómo se ve hasta ahora nuestro tablero?

![avance en el tablero](/assets/images/creacionAplicacion/trello_actividad02.png)

Ahora, para completar nuestro módulo de almacenamiento y consulta de productos, falta implementarlo en código, para lo cual usaremos spring.

## Programación de API para productos

Vamos a crear el API para nuestros productos, y para hacerlo de manera rápida usaremos spring boot. El proceso que seguiré es con ayuda del IDE IntelliJ, el cual es muy parecido a hacerlo con Spring Tool Suite (Eclipse). 

Vamos paso a paso.

Vamos a crear un nuevo proyecto, en el menú  File seleccionamos New -> Project

![New -> Project](/assets/images/creacionAplicacion/idea01_newProject.png)

Usaremos Spring initializer
![Spring initializer](/assets/images/creacionAplicacion/idea02_initializer.png)

En la siguiente pantalla, colocaremos los detalles del proyecto a crear.

![Detalles del proyecto](/assets/images/creacionAplicacion/idea03_projectSettings.png)

Nos mostrará una nueva pantalla donde debemos de agregar las dependencias, usaremos Spring Data Mongo DB, Rest Repositories y Spring Boot Actuator, esta última nos será útil después.

![Dependencias](/assets/images/creacionAplicacion/idea04_dependencias.png)

Por último, en la siguiente pantalla colocamos el nombre del proyecto y damos finalizar.

Esto nos creará la estructura básica del proyecto SpringBoot.

![estructura](/assets/images/creacionAplicacion/idea05_estructura.png)

Ahora, a codificar. Necesitamos crear la clase que modele la colección que dimos de alta en mongo. Nuestra clase se llama Producto y estará en el paquete `com.tyrel.store.apiproducts.data.collections` ésto sólo para darle un orden más adecuado.

```java
package com.tyrel.store.apiproducts.data.collections;

import org.springframework.data.annotation.Id;

public class Producto {

    @Id
    private String id;
    private String sku;
    private String nombre;
    private String descripcionGeneral;
    private String detalle;
    private double precio;
    private String imagen;
    private int stock;

    public Producto(){

    }

    public Producto(String id, String sku, String nombre, String descripcionGeneral, String detalle, double precio, String imagen, int stock) {
        this.id = id;
        this.sku = sku;
        this.nombre = nombre;
        this.descripcionGeneral = descripcionGeneral;
        this.detalle = detalle;
        this.precio = precio;
        this.imagen = imagen;
        this.stock = stock;
    }

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getSku() {
        return sku;
    }

    public void setSku(String sku) {
        this.sku = sku;
    }

    public String getNombre() {
        return nombre;
    }

    public void setNombre(String nombre) {
        this.nombre = nombre;
    }

    public String getDescripcionGeneral() {
        return descripcionGeneral;
    }

    public void setDescripcionGeneral(String descripcionGeneral) {
        this.descripcionGeneral = descripcionGeneral;
    }

    public String getDetalle() {
        return detalle;
    }

    public void setDetalle(String detalle) {
        this.detalle = detalle;
    }

    public double getPrecio() {
        return precio;
    }

    public void setPrecio(double precio) {
        this.precio = precio;
    }

    public String getImagen() {
        return imagen;
    }

    public void setImagen(String imagen) {
        this.imagen = imagen;
    }

    public int getStock() {
        return stock;
    }

    public void setStock(int stock) {
        this.stock = stock;
    }

    @Override
    public String toString() {
        return "Producto{" +
                "id='" + id + '\'' +
                ", sku='" + sku + '\'' +
                ", nombre='" + nombre + '\'' +
                ", descripcionGeneral='" + descripcionGeneral + '\'' +
                ", detalle='" + detalle + '\'' +
                ", precio=" + precio +
                ", imagen='" + imagen + '\'' +
                ", stock=" + stock +
                '}';
    }
}
```

La segunda clase importante que vamos a crear será `ProductRepository` y se encontrará en el paquete `com.tyrel.store.apiproducts.data.repositories`. Lo que estamos haciendo con esto es pedir a spring que nos cree el código para realizar operaciones CRUD sobre nuestra colección Producto.

```java
package com.tyrel.store.apiproducts.data.repositories;

import com.tyrel.store.apiproducts.data.collections.Producto;
import org.springframework.data.mongodb.repository.MongoRepository;

public interface ProductRepository  extends MongoRepository<Producto, String> {

}
```

Por default, Spring Data Mongo estaría intentando conectarse a localhost, pero en nuestro caso estamos usando un servidor externo, por lo que debemos de especificar los datos de conexión en el archivo `applications.properties`. Coloquemos esta línea:

```
spring.data.mongodb.uri=mongodb://192.168.56.101:27017/tyrell
```

¿Qué es lo que estamos haciendo? Con ayuda de Spring Data Mongo no sólo estamos generando el repository que nos permite realizar operaciones CRUD hacia nuestra colección producto, estamos generando los servicios REST que exponen estas funciones. Spring nos ahorra el trabajo de generar los controladores, definir endpoints, operaciones, parámetros y demás, simplemente indicándole la estructura de la colección que estará trabajando.

Veamos, agreguemos unas líneas a la clase ApiProductsApplication, dejándola como se muestra:

```java
@SpringBootApplication
public class ApiProductsApplication {

    @Autowired
    private ProductRepository productoRepository;

    @PostConstruct
    void init() {
        productoRepository.findAll().stream().forEach(System.out::println);
    }

    public static void main(String[] args) {
        SpringApplication.run(ApiProductsApplication.class, args);
    }
}
```

Estamos indicando que , después de que se construya la aplicación, se ejecute el método `init`, el cual hace uso del repositorio `ProductRepository` para obtener todos los documentos en esa colección e imprimirlo en pantalla. Esperamos entonces que:

- Se levante la aplicación y muestre en consola los resultados de ls búsqueda indicada
- Se creen enpoints con las operaciones CRUD sobre nuestra colección productos
- Se cree un endpoint que indique que la aplicación se encuentra disponible (esto gracias a Spring Actuator)

Ejecutemos nuestra aplicación.

Desde IntelliJ, podemos  abrir la pestaña **Services**, para agregar un servicio.

![](/assets/images/creacionAplicacion/runApp01_addService.png)

Del menú desplegable seleccionamos Spring Boot

![](/assets/images/creacionAplicacion/runApp_02_projectSpringBoot.png)

Una vez agregado, lo corremos, y podremos ver en la consola lo siguiente.

![](/assets/images/creacionAplicacion/runApp03_runService.png)

Se ha iniciado la aplicación, y en un punto de nuestra terminal, el resultado de la consulta que colocamos, mostrando el documento que inicialmente habíamos agregado a nuestra colección.

Ahí podemos ver un detalle, con la descripción general que arreglaremos más adelante, por ahora, podemos ver que inició la aplicación y realizó la consulta. Ahora, si nos cambiamos de pestaña a endpoints, nos muestra todos los que ha levantado la aplicación.

![](/assets/images/creacionAplicacion/runApp04_endpoints.png)

En caso de que no estes usando IntelliJ, como una aplicación vamen, lo podemos ejecutar desde la terminal.

```bash
mvn clean install
```
 y después ejecutar el jar construido

 ```bash
java -jar target/api-products-0.0.1-SNAPSHOT.jar 
 ```

Lo podemos ver más claro en el navegador:

![](/assets/images/creacionAplicacion/runApp05_navegador.png)

Y si vamos a la url que indica: **http://localhost:8080/productoes**

![](/assets/images/creacionAplicacion/runApp05_productoes.png)

Nos muestra el resultado de la consulta.

Hemos cumplido con el objetivo de nuestro primer punto en el backlog, ya podemos pasar el sticker a la lista de completadas.

![](/assets/images/creacionAplicacion/actividadTerminada.png)

Como ejercicio podrías crear las otras colecciones que corresponden  a categorías y subcategorías de productos.

