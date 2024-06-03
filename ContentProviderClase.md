## ¿ContentProvider?

Un Content Provider es un mecanismo que implementa
Android para compartir datos entre aplicaciones.

- Este mecanismo permite desacoplar la capa de aplicación
de la capa de datos

- Un Content Provider puede ayudar a una aplicación a
gestionar el acceso a los datos almacenados por sí
misma o almacenados por otras aplicaciones, y
proporciona una forma de compartir datos con otras
aplicaciones.

Android nos proporciona una serie de Content Providers ya
existentes, que nos permiten acceder a diferentes datos de
nuestro dispositivo, como el historial de navegación, el
registro de llamadas, las preferencias del dispositivo, los
recursos multimedia del dispositivo, la lista de contactos,
entre otros.

`Acceso estandarizado:`

Proporcionan una interfaz estandarizada para acceder y
modificar datos, independientemente del tipo de fuente de
datos. Esto facilita que las aplicaciones interactúen con
diferentes fuentes de datos de manera uniforme.

`Seguridad:`

Implementan mecanismos de seguridad para controlar el
acceso a los datos, asegurando que solo las aplicaciones
autorizadas puedan acceder y modificar los datos

`Abstracción:`
Ocultan los detalles de implementación de la fuente de
datos, permitiendo a las aplicaciones trabajar con los
datos de forma independiente de la tecnología de
almacenamiento subyacente.

`Reutilización:`
Pueden ser reutilizados por diferentes aplicaciones,
evitando la necesidad de duplicar código para acceder
a la misma fuente de datos

### Usos de los ContentProviders

 - `Compartir datos entre aplicaciones`, son ideales para
permitir que diferentes aplicaciones de un mismo dispositivo
o de diferentes dispositivos accedan y compartan datos de
manera segura y eficiente

- `Sincronización de datos`, pueden utilizarse para
sincronizar datos entre diferentes dispositivos o entre una
aplicación y un servidor remoto.

- `Acceso a datos externos`, pueden utilizarse para acceder
a datos almacenados en fuentes externas, como servicios
web o bases de datos en la nube.

### URI del proveedor
la URI es la dirección única
que identifica al proveedor de contenido. Se define
utilizando la clase `UriMatcher`.

### Tipo MIME
Definir el tipo de `MIME` de los datos, indica el formato de
los datos que el proveedor de contenido puede
proporcionar. Se define utilizando la clase
`MimeTypeUtils`

### Manifest
Registrar el Content Provider en el archivo
`AndroidManifest.xml`. Esto permite que otras
aplicaciones puedan interactuar con el Content Provider

```xml
<provider
    android:name=“.MiContentProvider”
    android:authorities=“sv.edu.ufg.fis.amb.aplicacion.provider”
    android:exported=“false”>
</provider>
```

