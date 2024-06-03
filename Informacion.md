# Informacion acerca de los proveedores de contenido.

Los proveedores de contenido pueden ayudar a una aplicación a administrar el acceso a los datos almacenados por sí misma o por otras apps y proporcionar una forma de compartir datos con otras apps. Encapsulan los datos y proporcionan mecanismos para definir su seguridad. Los proveedores de contenido son la interfaz estándar que conecta datos en un proceso con código que se ejecuta en otro proceso.

La implementación de un proveedor de contenido tiene muchas ventajas. Lo más importante es que puedes configurar un proveedor de contenido para permitir que otras aplicaciones accedan a los datos de tu app y los modifiquen de manera segura

Usa proveedores de contenido si tienes pensado compartir datos. Si no planeas compartir datos, no es necesario que los uses, pero puedes optar por hacerlo porque proporcionan una abstracción que te permite realizar modificaciones en la implementación de almacenamiento de datos de tu aplicación sin afectar a otras aplicaciones que dependen del acceso a tus datos.

En esta situación, solo tu proveedor de contenido se ve afectado y no las aplicaciones que acceden a él. Por ejemplo, puedes cambiar una base de datos SQLite por almacenamiento alternativo

Varias clases dependen de la clase `ContentProvider`:

- `AbstractThreadedSyncAdapter`
- `CursorAdapter`
- `CursorLoader`

El framework de Android incluye proveedores de contenido que administran datos como audio, video, imágenes e información de contacto personal. Puedes ver algunos de ellos en la documentación de referencia del paquete android.provider . Con algunas restricciones, cualquier aplicación para Android puede acceder a esos proveedores.

Se puede utilizar un proveedor de contenido para administrar el acceso a una variedad de fuentes de almacenamiento de datos, incluidos los datos estructurados, como una base de datos relacional SQLite, o los datos no estructurados, como los archivos de imagen. Para obtener más información sobre los tipos de almacenamiento disponibles en Android

## Ventajas de los proveedores de contenido

Los proveedores de contenido ofrecen un control detallado sobre los permisos de acceso a los datos. Puedes optar por restringir el acceso solo a un proveedor de contenido que se encuentre dentro de tu aplicación, otorgar permiso general para acceder a los datos de otras aplicaciones o configurar diferentes permisos de lectura y escritura de datos. Para obtener más información sobre cómo usar los proveedores de contenido de forma segura, consulta las sugerencias de seguridad para el almacenamiento de datos y los Permisos del proveedor de contenido.

Puedes usar un proveedor de contenido para abstraer los detalles de acceso a diferentes fuentes de datos en tu aplicación. Por ejemplo, tu aplicación puede almacenar registros estructurados en una base de datos SQLite, así como archivos de audio y video. Puedes usar un proveedor de contenido para acceder a todos estos datos.

Además, los objetos `CursorLoader` dependen de los proveedores de contenido para ejecutar consultas asíncronas y, luego, mostrar los resultados en la capa de la IU de tu aplicación. Si quieres obtener más información sobre el uso de un `CursorLoader` para cargar datos en segundo plano, consulta Cargadores.
