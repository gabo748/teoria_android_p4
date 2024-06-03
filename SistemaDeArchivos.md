## ¿Qué es un sistema de archivos?

Es un sistema de almacenamiento de un dispositivo de
memoria, que estructura y ordena la escritura, búsqueda,
lectura, almacenamiento, edición y eliminación de archivos
de una manera determinada.

## ¿Cual es el nombre del sistema de archivos que utiliza android?

El sistema de archivos de Android utiliza el sistema de
archivos de Linux, llamado `ext4`. Este sistema de archivos
es rápido y eficiente, lo que permite un acceso rápido a los
archivos y un rendimiento óptimo del dispositivo

Ext4, el cuarto sistema de archivos extendido, se introdujo
en 2008 como una mejora de ext3. Ofrece tamaños de
archivos y particiones más grandes, hasta 16 TB y 1 EB
(exabyte) respectivamente. Además, su rendimiento es más
rápido debido a las extensiones, que son bloques de datos
contiguos.

## Árbol de carpetas en Android

En el sistema de archivos de Android, la carpeta principal se
llama `“/” o “root”`. 

Dentro de esta carpeta, se encuentran
varias carpetas importantes.
En el sistema de archivos de Android, normalmente hay seis
particiones principales en cada dispositivo dentro de “/”.
Algunos dispositivos pueden venir con un par de particiones
adicionales, que difieren de un modelo a otro, pero en cada

dispositivo Android se encuentran seis particiones primarias:

### Para Almacenamiento interno:
- /boot
- /system
- /recovery
- /data
- /cache
- /misc

### Para Almacenamiento Externo:
- /sdcard
- /sd-ext

### /boot
La partición /boot comprende la imagen de arranque y el
kernel necesarios para iniciar el sistema operativo Android.
El dispositivo no puede arrancar sin la partición /boot.

Esta partición es de solo lectura y el usuario no puede
modificarla. Para modificarlo, el dispositivo debe estar
rooteado y se debe instalar una recuperación personalizada.
Una vez que el dispositivo está rooteado, se puede acceder
a la partición /boot y modificarla mediante un administrador
de archivos o una interfaz de línea de comandos.

## ¿Qué es ROM?

`Read Only Memory`, más comúnmente conocida como ROM,
es la memoria flash interna que almacena el sistema
operativo, es decir, la memoria fija de nuestros dispositivos.
Los sistemas operativos oficiales tradicionales suelen ser
instalados directamente por los fabricantes en teléfonos
inteligentes, tabletas y otros dispositivos inteligentes.

Una ROM, también conocida como `firmware`, generalmente
se almacena en la memoria permanente del teléfono, a
diferencia de la RAM (memoria de acceso aleatorio), que es
la memoria volátil que almacena y realiza copias de
seguridad temporalmente de sus archivos y datos

### /system

Es la partición que alberga todo el sistema operativo
Android. Esto incluye la GUI de Android, así como las
aplicaciones del sistema que vienen preinstaladas en los
dispositivos Android.
Entonces, ¿qué pasa si borramos esta partición? aún
podríamos iniciar el dispositivo, pero sólo podemos poner
nuestro dispositivo en modo recovery o bootloader.

La partición /system contiene folders y archivos como:
- /app
- /bin
- /fonts
- /framework

El contenido de la partición /system es de solo lectura y
solo se puede modificar con un dispositivo rooteado para
eliminar aplicaciones preinstaladas o personalizar el
sistema operativo Android.

La eliminación de esta partición borrará todas las
aplicaciones del sistema preinstaladas y solo debe
realizarse cuando el usuario desee instalar una ROM
personalizada o solucionar un problema con el sistema
operativo.


## ¿Qué es el recovery mode?

El modo de recuperación de Android es un modo de inicio
único disponible en todos los dispositivos Android que
proporciona un conjunto de herramientas para diagnosticar
y resolver problemas que no se pueden solucionar desde
el sistema operativo.

Este modo se utiliza normalmente para realizar
actualizaciones del sistema, restablecimientos de fábrica o
instalar ROM personalizadas.

Comúnmente utilizado para solución de problemas y
mantenimiento, el modo de recuperación ofrece opciones
como borrar datos/restablecimiento de fábrica, borrar la
partición de caché, aplicar actualizaciones desde tarjetas
ABD o SD, y más. En esencia, el modo de recuperación
sirve como una partición de arranque separada que es
esencial para realizar tareas a nivel del sistema y realizar
cambios en el sistema de archivos del sistema Android.

### /recovery
La partición /recovery es una partición pequeña que incluye
la imagen de recuperación para recuperar el dispositivo si
ocurre alguna falla del software. Este es otro folder de sólo
lectura que no se puede modificar.


### ¿Qué es ADB?

`ADB` corresponde a las siglas `Android Debug Bridge`.
Es una herramienta mediante la cual la consola de comandos
de nuestra computadora servirá de puente entre este y el
teléfono.
Gracias a ella, podemos enviar instrucciones al dispositivo
móvil, así como cargar archivos entre una y otra plataforma.

Para empezar a trabajar con ADB es necesario activar la
`"Depuración USB"`

### /data
La partición /data contiene todos los datos del usuario y de
la aplicación. Los datos del usuario pueden estar en forma
de fotos, vídeos, música, contactos, preferencias,
configuraciones, aplicaciones de Android, etc. que se
hayan instalado en el dispositivo. También es conocida
como partición de datos del usuario

Esta es una partición de lectura y escritura que puede ser
modificada por los datos provenientes de varias aplicaciones
instaladas. Es importante realizar copias de seguridad de los
archivos de esta partición con regularidad.

### /cache
La partición `/cache` contiene todos los archivos temporales
utilizados por el sistema operativo y las aplicaciones. Esta
es una partición de lectura y escritura y también puede
borrarla el sistema o un usuario.

Se puede acceder rápidamente a los archivos que incluye
la partición /cache sin tener que recuperarlos ni del
almacenamiento interno ni de la tarjeta SD externa

Podemos eliminar los datos de la caché, ya que no tiene
ningún impacto en los detalles personales e importantes
requeridos por cualquier aplicación, pero borrará los datos y
los componentes a los que se accede con frecuencia

### /misc
La partición /misc en el sistema de archivos de Android está
destinada al almacenamiento de diversas configuraciones
del sistema como ID de operador o región, configuración de
USB y ciertas configuraciones de hardware.

### /sdcard
Suele ser una partición de almacenamiento externo
emulado al que pueden acceder tanto el usuario como el
sistema Android. El dispositivo de almacenamiento externo
emulado permite que las aplicaciones accedan a una parte
del almacenamiento interno del dispositivo como si fuera
almacenamiento externo y brinda compatibilidad con las
aplicaciones heredadas que no podían acceder al
almacenamiento interno directamente.

### /sd-ext
La partición /sd-ext es una partición opcional que se puede
utilizar para proporcionar espacio de almacenamiento
adicional para un dispositivo Android si el almacenamiento
interno es limitado. También se utiliza con mayor
frecuencia junto con la partición /data