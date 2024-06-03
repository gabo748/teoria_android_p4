# Cómo crear un proveedor de contenido

Un proveedor de contenido administra el acceso a un repositorio central de datos. Un proveedor se implementa como una o más clases en una aplicación para Android, junto con elementos en el archivo de manifiesto. Una de tus clases implementa una subclase de `ContentProvider`, que es la interfaz entre tu proveedor y otras aplicaciones.

Si bien los proveedores de contenido hacen que los datos estén disponibles para otras aplicaciones, puedes tener actividades en tu aplicación que le permitan al usuario consultar y modificar los datos que administra tu proveedor.

En esta página, se incluye el proceso básico para crear un proveedor de contenido y una lista de las APIs que se deben usar.

### Antes de que empieces a crear

Antes de que empieces a crear un proveedor, haz lo siguiente:

- Decide si necesitas un proveedor de contenido. Debes compilar un proveedor de contenido si quieres proporcionar una o más de las siguientes funciones:
- Te recomendamos que ofrezcas datos o archivos complejos para otras aplicaciones.
- Quieres permitir que los usuarios copien datos complejos de tu app en otras apps.
- Te recomendamos que proporciones sugerencias personalizadas usando el marco de trabajo de búsqueda.
- Quieres exponer los datos de tu aplicación a widgets.
- Quieres implementar las clases AbstractThreadedSyncAdapter, CursorAdapter o CursorLoader.

No necesitas un proveedor para usar bases de datos ni otros tipos de almacenamiento persistente si el uso ocurre completamente dentro de tu aplicación y no necesitas ninguna de las funciones anteriores mencionadas. En su lugar, puedes usar uno de los sistemas de almacenamiento que se describen en Descripción general del almacenamiento de datos y archivos.

A continuación, sigue estos pasos para crear un proveedor:

## 1. 
## Diseña el almacenamiento sin formato para tus datos. Un proveedor de contenido ofrece datos de dos maneras:

### Datos de archivos
Datos que normalmente se presentan en archivos, como fotos, audio o videos. Almacena los archivos en el espacio privado de tu aplicación. En respuesta a una solicitud de un archivo por parte de otra aplicación, tu proveedor puede ofrecer un controlador para el archivo.

### Datos "estructurados"
Datos que normalmente se encuentran en una base de datos, un array o una estructura similar. Almacena los datos en un formato que sea compatible con tablas de filas y columnas. Una fila representa una entidad, como una persona o un elemento en el inventario. Una columna representa algunos datos de la entidad, como el nombre de la persona o el precio de un elemento. Una forma común de almacenar este tipo de datos es en una base de datos SQLite, pero puedes usar cualquier tipo de almacenamiento persistente. Para obtener más información sobre los tipos de almacenamiento disponibles en el sistema Android, consulta la sección Cómo diseñar el almacenamiento de datos.

## 2.

Define una implementación concreta de la clase `ContentProvider` y sus métodos obligatorios. Esta clase es la interfaz entre tus datos y el resto del sistema Android. Para obtener más información sobre esta clase, consulta la sección Cómo implementar la clase ContentProvider. 

## 3
Define la string de autoridad del proveedor, los URI de contenido y los nombres de columnas. Si quieres que la aplicación del proveedor controle intents, define también acciones de intent, datos adicionales y marcas. Define también los permisos que requieres para las aplicaciones que quieran acceder a tus datos. Procura definir todos estos valores como constantes en una clase Contract independiente. Más adelante, puedes exponer esta clase a otros desarrolladores. 

## 4
Agrega otras piezas opcionales, como datos de muestra o una implementación de `AbstractThreadedSyncAdapter` que pueda sincronizar datos entre el proveedor y los datos basados en la nube.


# Cómo diseñar el almacenamiento de datos

Un proveedor de contenido es la interfaz para los datos guardados en un formato estructurado. Antes de crear la interfaz, decide cómo almacenar los datos. Puedes almacenar los datos en cualquier formato que desees y luego diseñar la interfaz para leerlos y escribirlos según sea necesario.

Estas son algunas de las tecnologías de almacenamiento de datos disponibles en Android:

- Si trabajas con datos estructurados, considera usar una base de datos relacional, como SQLite, o un almacén de datos de clave-valor no relacional, como LevelDB. Si trabajas con datos no estructurados, como contenido multimedia de audio, imagen o video, considera almacenar los datos como archivos. Puedes combinar y combinar varios tipos diferentes de almacenamiento y exponerlos con un solo proveedor de contenido si es necesario.

- El sistema Android puede interactuar con la biblioteca de persistencias Room, que proporciona acceso a la API de base de datos SQLite que usan los proveedores de Android para almacenar datos orientados a tablas. Para crear una base de datos con esta biblioteca, crea una instancia de una subclase de RoomDatabase, como se describe en Cómo guardar contenido en una base de datos local con Room.
- No es necesario que uses una base de datos para implementar tu repositorio. Un proveedor aparece externamente como un conjunto de tablas, similar a una base de datos relacional, pero esto no es un requisito para la implementación interna del proveedor.

- Para guardar datos de archivo, Android tiene una variedad de API orientadas a archivos. Para obtener más información sobre el almacenamiento de archivos, consulta la Descripción general del almacenamiento de datos y archivos. Si estás diseñando un proveedor que ofrece datos relacionados con contenido multimedia, como música o videos, puedes tener un proveedor que combine archivos y datos de tablas.
- En raras ocasiones, podrías beneficiarte de la implementación de más de un proveedor de contenido para una sola aplicación. Por ejemplo, es posible que desees compartir algunos datos con un widget mediante un proveedor de contenido y exponer un conjunto diferente de datos para compartirlos con otras aplicaciones.
- Para trabajar con datos basados en la red, usa las clases en java.net y android.net. También puedes sincronizar datos basados en la red con un almacén de datos local, como una base de datos, y, luego, ofrecer los datos como tablas o archivos.

# Consideraciones del diseño de datos 

- Los datos de tabla siempre deben tener una columna de “clave primaria” que el proveedor mantiene como un valor numérico único para cada fila. Puedes usar este valor para vincular la fila con filas relacionadas en otras tablas (usándola como "clave externa"). Si bien puedes usar cualquier nombre para esta columna, el uso de `BaseColumns._ID` es la mejor opción, ya que vincular los resultados de una consulta del proveedor a una `ListView` requiere que una de las columnas recuperadas tenga el `nombre _ID.`

- Si quieres proporcionar imágenes de mapas de bits u otros datos muy grandes orientados a archivos, almacena los datos en un archivo y, luego, proporciónalos indirectamente, en lugar de guardarlos directamente en una tabla. Si lo haces, debes indicarles a los usuarios de tu proveedor que deben usar un método de archivo ContentResolver para acceder a los datos.

- Usa el tipo de datos de objeto binario grande `(BLOB)` para almacenar datos que varíen en tamaño o tengan estructuras diferentes. Por ejemplo, puedes usar una columna `BLOB` para almacenar un búfer de protocolo o una estructura JSON.

- También puedes usar un `BLOB` para implementar una tabla independiente del esquema. En este tipo de tabla, defines una columna de clave primaria, una columna de tipo de `MIME` y una o más columnas genéricas como `BLOB`. El significado de los datos en las columnas `BLOB` se indica mediante el valor de la columna de tipo de `MIME`. Esto te permite almacenar diferentes tipos de filas en la misma tabla. La tabla "datos" `ContactsContract.Data` del Proveedor de contactos es un ejemplo de una tabla independiente de esquemas.

# Cómo diseñar URI de contenido

Un URI de contenido es un URI que identifica datos de un proveedor. Los URI de contenido incluyen el nombre simbólico de todo el proveedor (su autoridad) y un nombre que apunta a una tabla o un archivo (una ruta de acceso). La parte del ID opcional apunta a una fila individual de una tabla. Cada método de acceso a los datos de ContentProvider tiene un URI de contenido como argumento. Esto te permite determinar la tabla, la fila o el archivo al que se accederá.

## Diseñar una autoridad

Un proveedor generalmente tiene una sola autoridad, que sirve como su nombre interno en Android. Para evitar conflictos con otros proveedores, usa la propiedad del dominio de Internet (en sentido inverso) como base de la autoridad de tu proveedor. Dado que esta recomendación también se aplica a los nombres de paquetes de Android, puedes definir la autoridad de tu proveedor como una extensión del nombre del paquete que contiene al proveedor.

Por ejemplo, si el nombre de tu paquete de Android es `com.example.<appname>`,` otórgale a tu proveedor la autoridad `com.example.<appname>.provider.`

## Diseña una estructura de ruta

Por lo general, los desarrolladores crean `URI` de contenido a partir de la autoridad anexando rutas de acceso que apuntan a tablas individuales. Por ejemplo, si tienes dos tablas, table1 y table2, puedes combinarlas con la autoridad del ejemplo anterior para obtener los URI de `contenido com.example.<appname>.provider/table1` y `com.example.<appname>.provider/table2`. Las rutas de acceso se limitan a un solo segmento, y no es necesario que haya una tabla para cada nivel de la ruta.

## Cómo controlar los IDs de URI de contenido

Por convención, los proveedores ofrecen acceso a una sola fila en una tabla si aceptan un URI de contenido con un valor de ID para la fila al final del URI. También por convención, los proveedores hacen coincidir el valor de ID con la `columna _ID` de la tabla y realizan el acceso solicitado en la fila que coincide.

Esta convención facilita un patrón de diseño común para aplicaciones que acceden a un proveedor. La app realiza una consulta al proveedor y muestra el Cursor resultante en una ListView mediante un CursorAdapter. La definición de CursorAdapter requiere que una de las columnas de Cursor sea _ID

Luego, el usuario selecciona una de las filas que se muestran de la IU para observar o modificar los datos. La app obtiene la fila correspondiente del Cursor que respalda el ListView, obtiene el valor _ID para esta fila, lo agrega al URI de contenido y envía la solicitud de acceso al proveedor. Luego, el proveedor puede realizar la consulta o la modificación en la fila exacta que seleccionó el usuario.

## Patrones de URI de contenido

Para ayudarte a elegir qué acción realizar para un URI de contenido entrante, la API del proveedor incluye la clase de conveniencia UriMatcher, que asigna patrones de URI de contenido a valores enteros. Puedes usar los valores de números enteros en una declaración switch que elijan la acción deseada para los URI de contenido que coincidan con un patrón específico.

Un patrón de URI de contenido compara URI de contenido usando caracteres comodín:

- coincide con una string de cualquier carácter válido de cualquier longitud.
- coincide con una string de caracteres numéricos de cualquier longitud.

Como ejemplo de diseño y programación de manejo de URI de contenido, considera un proveedor con la autoridad `com.example.app.provider` que reconozca los siguientes URI de contenido que apuntan a tablas:

`content://com.example.app.provider/table1: Una tabla llamada table1.`
`content://com.example.app.provider/table2/dataset1: Una tabla llamada dataset1.`
`content://com.example.app.provider/table2/dataset2: Una tabla llamada dataset2.`
`content://com.example.app.provider/table3: Una tabla llamada table3.`
El proveedor también reconoce estos URI de contenido si tienen un ID de fila anexado, como content://com.example.app.provider/table3/1 para la fila identificada por 1 en table3.
