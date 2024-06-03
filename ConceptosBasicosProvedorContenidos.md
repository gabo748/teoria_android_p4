# Conceptos básicos sobre proveedores de contenido

Un proveedor de contenido administra el acceso a un repositorio central de datos. Un proveedor forma parte de una aplicación para Android y a menudo proporciona su propia IU para trabajar con los datos. Sin embargo, los proveedores de contenido los usan principalmente otras aplicaciones que acceden al proveedor mediante un objeto de cliente del proveedor. Juntos, los proveedores y sus clientes ofrecen una interfaz estándar y coherente para los datos que también maneja la comunicación entre procesos y el acceso seguro a los datos.

Por lo general, se trabaja con proveedores de contenido en una de estas dos situaciones: implementar código para acceder a un proveedor de contenido existente en otra aplicación o crear un proveedor de contenido nuevo en tu aplicación para compartir datos con otras aplicaciones.

En esta página, se abordan los aspectos básicos para trabajar con proveedores de contenido existentes. Para obtener información sobre cómo implementar proveedores de contenido en tus propias aplicaciones

### Descripción general

Un proveedor de contenido presenta datos a aplicaciones externas en forma de una o más tablas que son similares a las tablas de una base de datos relacional. Una fila representa una instancia de algún tipo de datos que recopila el proveedor, y cada columna de la fila representa un ítem individual de los datos recopilados para una instancia.

Un proveedor de contenido coordina el acceso a la capa de almacenamiento de datos en tu aplicación para una serie de API y componentes diferentes. Como se ilustra en la figura 1, se incluyen los siguientes elementos:

- Compartir con otras aplicaciones el acceso a los datos de tu aplicación
- Enviar datos a un widget
- Mostrar sugerencias personalizadas de búsqueda para tu aplicación mediante el marco de trabajo de búsqueda usando `SearchRecentSuggestionsProvider`
- Sincronizar los datos de la aplicación con tu servidor mediante una implementación de `AbstractThreadedSyncAdapter`
- Cargar datos en tu IU usando `CursorLoader`

### Cómo acceder a un proveedor

Cuando quieres acceder a datos en un proveedor de contenido, usas el objeto `ContentResolver` en el Context de tu aplicación para comunicarte con el proveedor como cliente. El objeto `ContentResolver` se comunica con el objeto del proveedor, una instancia de una clase que implementa `ContentProvider`.

El objeto del proveedor recibe solicitudes de datos de clientes, realiza la acción solicitada y muestra resultados. Este objeto tiene métodos que llaman a métodos con el mismo nombre en el objeto del proveedor, una instancia de una de las subclases concretas de `ContentProvider`. Los métodos `ContentResolver` proporcionan las funciones básicas "CRUD" (creación, recuperación, actualización y eliminación) del almacenamiento persistente.

Un patrón común para acceder a un `ContentProvider` desde tu IU usa un `CursorLoader` para ejecutar una consulta asíncrona en segundo plano. El `Activity` o el `Fragment` de tu IU llaman a un `CursorLoader` para la consulta, lo que, a su vez, obtiene el ContentProvider mediante el `ContentResolver`.

Esto permite que la IU siga estando disponible para el usuario mientras se ejecuta la consulta. Este patrón contempla la interacción de una serie de objetos diferentes y del mecanismo de almacenamiento subyacente

Uno de los proveedores integrados en la plataforma de Android es el proveedor de diccionario del usuario, que almacena las palabras no estándar que el usuario quiere conservar.

Si quieres obtener una lista de palabras y sus configuraciones regionales del proveedor de diccionario del usuario, debes llamar a `ContentResolver.query()`. El método `query()` llama al método `ContentProvider.query()` definido por el proveedor de diccionario del usuario. Las siguientes líneas de código muestran una llamada `ContentResolver.query()`:

```kotlin
// Queries the UserDictionary and returns results
cursor = contentResolver.query(
        UserDictionary.Words.CONTENT_URI,  // The content URI of the words table
        projection,                        // The columns to return for each row
        selectionClause,                   // Selection criteria
        selectionArgs.toTypedArray(),      // Selection criteria
        sortOrder                          // The sort order for the returned rows
)
```

### URI de contenido

Un URI de contenido es un URI que identifica datos de un proveedor. Los URI de contenido incluyen el nombre simbólico de todo el proveedor (su autoridad) y un nombre que apunta a una tabla (una ruta de acceso). Cuando llamas al método del cliente para acceder a una tabla del proveedor, el URI de contenido de la tabla es uno de los argumentos.

En las líneas de código anteriores, la constante `CONTENT_URI` contiene el `URI` de contenido de la tabla Words del proveedor de diccionario del usuario. El objeto ContentResolver analiza la autoridad del URI y la usa para resolver el proveedor comparando la autoridad con una tabla del sistema de proveedores conocidos. Luego, ContentResolver puede enviar los argumentos de la consulta al proveedor correcto.

El `ContentProvider` usa la parte de la ruta de acceso del URI de contenido para seleccionar la tabla a la que quiere acceder. Un proveedor suele tener una ruta de acceso para cada tabla que expone.

En las líneas de código anteriores, el URI completo de la tabla Words es el siguiente:

```txt
content://user_dictionary/words
```

- La cadena `content://` es el esquema, que siempre está presente e identifica esto como un URI de contenido.
- La string `user_dictionary` es la autoridad del proveedor.
- La string `words` es la ruta de acceso de la tabla.