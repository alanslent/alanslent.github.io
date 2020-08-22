---
layout: post
title: Instalación de una máquina virtual con Virtual Box
---


Muchas veces, como desarrolladores, necesitamos usar otros sistemas operativos, que a veces no son los que más nos acomodan para uso diario. La solución es utilizar la virtualización.

La virtualización es utilizar un único hardware físico para simular otros sistemas basados en software.

## Creación de una máquina virtual con VirtualBox

La forma más común de realizar virtualización en nuestras computadoras personales, es utilizando un software de virtualización como [VirtualBox](https://www.virtualbox.org). En su página de descarga podemos encontrarlo para varios sistemas operativos, así como las instrucciones detalladas de instalación y configuración.  Para fines generales, la instalación básica (el clásico "next", "next", "next"  nos funcionará).

![Ventana principal de VirtualBox](https://lh3.googleusercontent.com/-BKv_xBwqzVg/Xw6WwdO7xmI/AAAAAAAAIZ0/0rt5ZlbQ94k0qgtFVp2ZX_l-RLXTToejwCLcBGAsYHQ/h240/virtualBox.png)

En este punto, podemos crear una nueva máquina virtual y sobre ello instalar un nuevo sistema operativo.

Cuando le damos clic en el ícono de "nueva", nos muestra su asistente para guiarnos en la creación.
![Selecciona sistema operativo](https://lh3.googleusercontent.com/-HcNU-90qPUo/Xw82Jn5RAdI/AAAAAAAAIaA/MzxVJ1K5A6c6Bq38XUDngZrScE-cl4NJwCLcBGAsYHQ/h240/virtualBox_seleccionaSO.png)

Y en la siguiente opción, seleccionamos la versión del sistema operativo que se va a instalar.
![Seleccionar versión del sistema operativo](https://lh3.googleusercontent.com/-Gkw_GHvdB8o/Xw82jcoSvcI/AAAAAAAAIaI/gDcJ473ehUQAht7Y0iWM-w_-04mN3sohwCLcBGAsYHQ/h240/virtualBox_seleccionaArquitectura.png)

En nuestro caso probaremos una versión de Linux que no está en la lista, pero sabemos que es de 64 bits, por lo que seleccionamos esa opción y le ponemos nombre a nuestra máquina virtual.

![Other linux y nombre](https://lh3.googleusercontent.com/-oqJN8CJ4lrk/XxCQtWQdNHI/AAAAAAAAIaU/buIw_h9Pij0u1WrOQJBDuYd6oc8QLg0GACLcBGAsYHQ/h240/virtualBox_nombre.png)

En la siguiente pantalla mostrará el tamaño de memoria que queremos asignarle, dependerá de la cantidad de memoria que tengámos disponible, la parte marcada en verde es una recomendación, de manera que el equipo host no se vea comprometido.

![Seleccionar memoria](https://lh3.googleusercontent.com/-d_Jk54xzCtw/XxCRtl_l95I/AAAAAAAAIac/lZQO0qnno0cObXC_IFdtXFbTAzCzHQEGwCLcBGAsYHQ/h240/virtualBox_memoria.png)

Ahora, nos pedirá crear un disco duro virtual.
![Disco duro virtual](https://lh3.googleusercontent.com/-LLIqYeAGf0Q/XxCTsqJCnsI/AAAAAAAAIao/OKtRl3gDNYofKWtjnLmJVysuUDcB3D2egCLcBGAsYHQ/h240/virtualBox_disco.png)

En las siguientes opciones indicaremos que queremos un disco duro de tipo VDI, y que el espacio sea reservado dinámicamente.

Finalmente nos indicará en dónde deseamos guardar el archivo de la unidad de disco.

![Ubicación del archivo de unidad de disco](https://lh3.googleusercontent.com/-vk7_DkWlBo4/XxT4almn0qI/AAAAAAAAIbU/avb1xzsCq1oPscNwGeD6zLnVCwTEq1kmACLcBGAsYHQ/h240/virtualBox_guardar.png)

Ya instalada la máquina virtual, podemos instalar sobre ella cualquier versión de Linux que queramos. Si ya tenemos la imagen ISO de la distribución de linux que vamos a instalar, vayamos a montarla.

Seleccionamos la máquina virtual que acabamos de instalar, y damos clic en la opción de configuración, lo que nos abrirá una ventana como esta.
![Configuración](https://lh3.googleusercontent.com/-Xy9TN8x46oY/XxT7xeZioPI/AAAAAAAAIbg/ENfmuK29tAsSYbdDbYHZj5e8N6OZcGtsACLcBGAsYHQ/h240/virtualBox_configuracion.png)

Nos aparecen varias opciones pora configurar, procesadores, memoria, puertos, discos, etc. Podemos ver la documentación que nos ofrece VirtualBox en su página oficial para conocer los detalles de ésta, pero para nuestros fines podemos dejar la configuración tal cual se encuentra y pasar directo a la opción de discos.

![Almacenamiento](https://lh3.googleusercontent.com/-qT-lxsP9MzY/XxT-vh3MRrI/AAAAAAAAIbs/nKPGXHVE1W09MXvAbqxflipI5g11l92mACLcBGAsYHQ/h240/virtualBox_discoOptico.png)

Ahí vamos a seleccionar la imagen de disco Linux que hayamos descargado.
![Imagen ISo seleccionada](https://lh3.googleusercontent.com/-yC53hEujb2U/XxUCTjQD9nI/AAAAAAAAIb8/We5tqolXXRAVBwGRbkFgROEfcQ8qVUTBgCLcBGAsYHQ/h240/virtualBox_imagenIso.png)

Con esta configuración será suficiente para poder instalar un sistema Linux en nuestra computadora virtual. Seleccionamos nuestra instalación (Linux Virtual) y ya nos mostrará una pantalla en la que se muestra nuestra máquina virtual iniciando.

![Iniciando máquina virtual](https://lh3.googleusercontent.com/-KaR-nOtXXYE/XxUDEbVVBvI/AAAAAAAAIcI/PnmHBLmgqTYg73Pml2Cd3_v7qGmW2veBwCLcBGAsYHQ/h240/virtualBox_running.png)

A partir de aquí, la instalación del sistema operativo depende de la versión utilizada, por lo que es necesario revisar sus páginas oficiales para obtener la documentación adecuada.

## Instalación a partir de un archivo de imagen VDI

Algunas distribuciones de Linux proporcionan archivos VDI que contienen por completo la imagen del disco virtual, ya con el sistema operativo instalado y configurado. Además, de que hay un repositorio donde podemos encontrar varias imágenes ya  listas para instalarse, este es [osboxes](https://www.osboxes.org), en donde podemos encontrar varios sistemas operativos listos para descargar y virtualizar.

![Imagenes disponibles](https://lh3.googleusercontent.com/-67Vo2FXo5xo/XxUSFT9wxbI/AAAAAAAAIcU/YGOze_tbdFkVtBGvjYYTHvtPZgXWOd1wgCLcBGAsYHQ/h240/osboxes_lista.png)

Para el caso de los VDI, realizamos el mismo proceso de creación que vimos anteriormente.

- Nuevo, colocar nombre, tipo de sistema operativo, versión.
- Tamaño de memoria

Pero en la parte de disco duro, debemos seleccionar *usar un archivo de disco virtual existente*
![Usar disco existente](https://lh3.googleusercontent.com/-7Zk1tl5oklE/XxUTRfQRXbI/AAAAAAAAIcc/IUweIPbmw8sWoFmHQ9J970A06wWlRedkwCLcBGAsYHQ/h240/virtualBox_usarDiscoExistente.png)

En el icono de navegación derecho nos permitirá seleccionar el archivo  vdi que vamos a usar.

![Discos existentes](https://lh3.googleusercontent.com/-24Qe84Mnavc/XxUT2K7MzFI/AAAAAAAAIck/TfnEraNAmZwfNKhpWDAmFQXtIvZ_wpNegCLcBGAsYHQ/h240/virtualBox_agregarDisco.png)

No se encontrará en la lista el que hemos descargado de osboxes, así que debemos agregarlo usando el botón correspondiente. Seleccionamos el vdi a usar y damos clic en "crear".

En la lista de maquinas virtuales ya podemos ver la que acabamos de crear y la podremos iniciar.

![Nueva máquina virtual agregada](https://lh3.googleusercontent.com/-n4pCGSWjIDA/XxUVSyVYeeI/AAAAAAAAIcw/nl_1QgpTgscxCTXUGUGcRZYrHD3GkjYmACLcBGAsYHQ/h240/virtualBox_agregado.png)

Ya no será necesario configurar discos ni realizar la instalación del SO, directamente ya podremos usar el sistema.

![osboxes corriendo](https://lh3.googleusercontent.com/-uxV2QLvUx6A/XxUWIm1gBkI/AAAAAAAAIc4/Wkiws9Gm8FMTsdpsmtHf8VtVMwJM1jR4gCLcBGAsYHQ/h240/virtualBox_runningOSbooxes.png)

La contraseña del sistema se encuentra a lado del lugar de donde se descargó, y en general es:
**Username:** osboxes  
**Password:** osboxes.org

