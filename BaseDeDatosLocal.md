## Aspectos de registro de datos en BD
- `Shared Preferences`: Es una forma de almacenar datos
clave-valor. En ella podemos almacenar pequeñas
cantidades de datos, como configuraciones de usuario.
- `SQLite`: Android ofrece soporte completo para SQLite,
que es una base de datos muy ligera para
almacenamiento persistente. Es útil cuando necesitamos
almacenar una cantidad considerable de datos
estructurados.

`Room:` Es una capa de abstracción sobre SQLite que permite
un acceso más robusto y fácil a la base de datos local de
SQLite. Room se encarga de muchas tareas tediosas que
normalmente necesitamos manejar con SQLite

`DataStore` Es una solución de almacenamiento de datos que
permite almacenar datos clave-valor o datos tipados con
protocol buffers. DataStore proporciona consistencia de datos
en transacciones asíncronas, así como manejo de errores
integrado.

`SQLite` En algún momento como desarrolladores nos
encontraremos con la necesidad de almacenar los datos
de nuestras aplicaciones para su posterior uso, esto
incluye aplicaciones web , de escritorio y aplicaciones
móviles.
Guardar datos en una base de datos es ideal para los
datos estructurados o que se repiten, como la información
de contacto

`SQLite` implementa un motor de base de datos SQL que tiene las
siguientes características:

- Es autónomo (no requiere otros componentes).
- Usa tecnología sin servidores (no requiere backend de servidor).
- No requiere configuración (no es necesario que esté configurada
para tu app).
- Admite transacciones (los cambios en una sola transacción en
SQLite pueden producirse o no).

Para desarrollar aplicaciones móviles en Android que
almacenen datos en SQLite, necesitamos las siguientes
librerías o APIs:

### SQLiteOpenHelper
SQLiteOpenHelper: Es una clase de ayuda para gestionar
la creación de la base de datos y la gestión de versiones.
Deberemos crear una clase que extienda la clase
SQLiteOpenHelper y sobreescribir los métodos
`onCreate()` y `onUpgrade()`

### android.database.sqlite
`android.database.sqlite:` Este paquete proporciona las
APIs para trabajar con SQLite. Incluye clases como
SQLiteDatabase, SQLiteQueryBuilder, y otras que nos
ayudan a gestionar las operaciones de la base de datos.

- El método `onCreate()` se usa para ejecutar comandos de
SQLite para crear las tablas de la base de datos.
- El método `onUpgrade()` se ejecutará cada vez que cambiemos
la versión de la base de datos y se usará para migrar los datos
de la base de datos anterior a la nueva versión.

### ¿Qué son las dataclases?

Las Data Classes en Kotlin son clases, las cuales su
función principal es la de almacenar y gestionar datos.
Son similares a las clases regulares que ya conocemos,
pero con algunas funcionalidades adicionales generadas
automáticamente por el compilador

`Constructor primario`, Las Data Classes tienen un
constructor primario que es generado automáticamente a
partir de las propiedades declaradas en la clase.

`Igualdad e identidad`, Las Data Classes implementan la
igualdad por contenido y la identidad por `referencia` de forma
automática, lo que significa que dos instancias de la clase se
consideran iguales si tienen los mismos valores en sus
propiedades, y se consideran distintas si son objetos diferentes
en memoria.

`Copia`, Las Data Classes proporcionan una función
`copy()` que permite crear una nueva instancia de la clase
con los mismos valores de las propiedades de la
instancia original

### ¿Qué es Companion Object?

- Es un tipo especial de objeto asociado con una clase en
lugar de una instancia de la clase.
- Es similar a los miembros estáticos de otros lenguajes de
programación, pero con algunas funciones adicionales.

Acceso estático, se puede acceder a los miembros del
objeto complementario directamente desde la clase
asociada utilizando el nombre de la clase seguido de
punto y el nombre del miembro.

```kotlin
class MathConstants {
    companion object {
        const val PI = 3.14159
        const val E = 2.71828
    }
}

fun main() {
    println(MathConstants.PI)
    println(MathConstants.E)
}
```

## ¿Qué es Binding?

El binding (enlace de datos) es un proceso que conecta
los datos de la aplicación con la interfaz de usuario (UI).
Esto permite que los cambios en los datos se reflejen
automáticamente en la IU, sin necesidad de escribir
código manual para actualizar las vistas.

`Data Binding:`

Es una biblioteca oficial de Google que simplifica el proceso
de enlace de datos. Utiliza expresiones declarativas para
definir cómo se deben enlazar los datos a las vistas de la
UI. Esto hace que el código sea más legible, mantenible y
menos propenso a errores.

`View Binding:`

Es otra forma de enlazar datos a las vistas de la UI en
Android. Con ViewBinding, Android Studio genera
automáticamente una clase de enlace para cada archivo
de diseño (layout) XML en el proyecto.