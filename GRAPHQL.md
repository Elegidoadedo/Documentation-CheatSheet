**Orígenes de GraphQL**

Para comenzar debemos entender que GraphQL es un query language, es decir, un lenguaje de consultas. Un lenguaje es un sistema compartido por dos partes que les permite comunicarse entre sí.

Un lenguaje de consultas como GraphQL nos permite hacer consultas y esperar una respuesta predecible. Un ejemplo de una lenguaje de consultas es SQL, el cual se enfoca en las consultas a una base de datos.

Aunque suene un poco confuso, SQL no tiene nada que ver con GraphQL, ya que el primero está pensado para trabajar con bases de datos, y GraphQL es para comunicar clientes y servidores.

GraphQL es una herramienta que se presenta como una alternativa a REST. La principal mejora que propone es la optimización, además de trasladar la información del servidor al cliente.

Una de las ventajas más importantes de GraphQL es que es agnóstico de plataforma, lo que quiere decir que se puede implementar en más de 20 lenguajes.

El principal objetivo de GraphQL es evitar las múltiples consultas al servidor.


**DIFERENCIA ENTRE REST Y GRAPHQL**

Rest
Es solo una convención: Es una manera de comunicarse entre el servidor y cliente, cada uno tiene sus reglas.
GraphQL
Lenguaje tipado y validable: Le damos una forma de lo que recibe y lo que devolvemos. Ademas que le agrega seguridad

Rest
Servidor expone recursos: Los clientes se tienen que adecuarse a como están expuestos
GraphQL
El cliente define que recibe: Haciendo una consulta, de la estructura que define como respuesta

Rest
Hace overfetching: Envía más información que necesita
GraphQL
Envía lo necesario: Se tiene control total de las respuestas que se esperan del servidor

Rest
Multiples request por vista: Muy costoso en performance, básicamente es una aplicación en blanco que aún no ha cargado datos o tiene custom endpoints
GraphQL
Hace solo un request por vista: Enviados en un solo row

Rest
Documentación ajena al desarrollo: No hay un estándar por lo que depende mucho del desarrollador para mantenerla.
GraphQL
Documentado por definición.
Documentado por definición: Al ser un lenguaje tipado se define un schema que ya esta documentado por definiciòn

**SCHEMA**


En el schema se define lo que puede pedir el cliente. Compuesto por types:

Los types o tipos de datos que pueden usarse en un schema son:

Scalars
Objects
Enums
Interfaces
Unions


Scalars: Los scalars nos van a permitir definir la mayoría de las propiedades de nuestras entidades:

Int - Números enteros
Float - Números decimales
String - Cadenas de texto
Boolean - Verdadero o Falso
ID - Identificador único

Objects: El Type Objects permite definir entidades

        type Curso{
        id : ID!
        descripcion: String
        profesores: [Profesor]
        rating: Int
        }

        type Profesor{
        nombre: String
        edad: Int
        tieneMascota: Boolean
        }

Enum: Enum es un tipo que nos permite definir algo que puede tomar el valor de una lista de opciones.

        enumTipo {
            PROFESOR
            ESTUDIANTE
        }

Interface: Proporciona la capacidad de describir campos que se comparten en diferentes tipos, es la definición de campos requeridos que sabemos que todas las implementaciones se van a cumplir, si en un futuro necesitáramos que todas las implementaciones de perfil tuvieran un nuevo campo, solamente debemos agregarlo a la Interface.

        // Al usar interface se indica el uso de interface
            interface Perfil {
                // para este ejemplo se setea
                // el uso de campos obligados
                nombre: String!
                email: String!
                edad: Int!
            }
            
            // Al usar implements se indica que usar al interface Perfil
            type Alumno implements Perfil {
                // De igual manera tenemos que declarar
                // los cambpos que se utilizan en la interface
                nombre: String!
                email: String!
                edad: Int!
                cruso: String
            }
Es importante mencionar que el concepto de extender la lógica no existe en GraphQL es una manera de asegurarse que las implementaciones están al dia, de una manera mas sencilla podríamos mencionar que el uso de interface funciona con una validación previa al ejecutar un query.

Union: Entiendo UNION como la forma de realizar una busqueda de un dato en diferentes ambientes.

Es como decir buscar sobre Platzi en facebook lo que nos arroja un resultado de:

Platzi como Pagina
Platzi como Comunidad o Grupo
etc

**Modificadores de tipo**

Existen dos modificadores de tipo:

Requerido: Signo de admiración al final, y significa que ese campo no puede ser null
Corchetes: Para denotar que tenemos una lista de lo que sea que está en medio.
Tenemos también la posibilidad de hacer una lista requerida de la siguiente forma:

[string!]!