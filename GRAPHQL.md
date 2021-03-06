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

ejemplo:

        String! NOT NULL
        [String] LISTA
        [String] ! LISTA QUE NO PUEDE SER NULL PERO QUE SIN EMBARGO SUS ELEMENTOS PUEDEN SER NULL
        [String!] ! LISTA QUE NO PUEDE SER NULL NI TAMPOCO CONTENER NI UN SOLO ELEMENTO NULL

**Root Type: Query**

Podríamos verlos como una analogía a los endpoints que tenemos en una arquitectura .REST.

**Root Type: Mutation**

Graphql también nos permite hacer modificaciones, y para hacerlas, tenemos un tipo especial de endpoints que se llaman Mutation.
A través de ellos vamos a poder insertar elementos, modificar elementos, borrar elementos, etc.

**La Interfaz de GraphiQL**

GraphiQL es la herramienta que más vamos a utilizar para interactuar con un esquema de GraphQL.
Esta herramienta fue desarrollada por la misma gente de Facebook y nos permite hacer consultas, ver la documentación, interactuar con el esquema de GraphQL y así entender las queries que vamos a ejecutar.

Para usar variables es necesario usar la forma completa de la query.

        query <nombreQuery>(<$variable>: type = <valor por defecto>) {
            ...
        }

**ALIAS**
Uno de los motivos de usar un alias es al momento de pedir varios recursos del mismo Type con diferente ID para que la Key (En este caso curso) no se pise o se sobre escriba (Graphql no deja que eso pase).

        {
        cursoMasVotado: curso(id: 1) {
            titulo
            rating
        }
        cursoMasVisto: curso(id: 2) {
            titulo
            descripcion
        }
        }

**FRAGMENTS**

Los Fragments son una manera que nos permite GraphQL en las consultas de agrupar campos para poder utilizarlos de una manera conveniente para nuestra consulta.

    {
    curso(id: 1) {
        ...CamposNecesarios
    }
    cursos {
        ...CamposNecesarios
    }
    }

    fragment CamposNecesarios onCurso {
    titulo
    descripcion
    }

**DIRECTIVAS**

Las Directivas nos permiten pedir ciertos valores de una consulta dependiendo de si una variable es true o false.

Existen 2 tipos:

@include incluye el campo si el argumento es true.
@skip omite el campo si el argumento es true. (revirtiendo la condición)

Declaramos la variable:

        {
        "conDescription": true
        }

Realizamos la consulta:


        query Cursos($conDescription: Boolean!) {
        cursos {
            titulo
            descripcion @include(if: $conDescription)
        }
        }

**INPUT TYPE**

Los Input Types nos permiten pasar objetos complejos (y/o completos) en las mutaciones de manera sencilla, en lugar de pasar parametro por parametro vamos a pasar un solo parametro, el Input Type NuevoProfesor.

Implementación del Input Type en server:

        inputNuevoProfesor {
            nombre: String!
            genero: Genero
        }
Consulta del lado del cliente:

        mutation {
        profesorAdd(profesor: {
            nombre: "Laura"
            genero: FEMENINO
            nacionalidad: "Mexico"
        }) {
            id
        }
        }

**EJEMPLO DE SCHEMA EN GRAPHQL**

    const { gql } = require('apollo-server-express')

    const typeDefs = gql`

        """Esto es un curso en el sistema"""
        typeCurso {
            id: ID!
            titulo: String!
            """Esta es la descripción del curso"""
            descripcion: String!
            profesor: Profesor
            rating: Float
            comentarios: [Comentario]
        }

        typeProfesor{
            id: ID!
            nombre: String!
            nacionalidad: String!
            genero: Genero
            cursos: [Curso]
        }

        enum Genero{
            MASCULINO
            FEMENINO
        }

        typeComentario{
            id: ID!
            nombre: String!
            cuerpo: String!
        }

        typeQuery{
            cursos: [Curso]
            profesores: [Profesor]
            curso(id: Int): Curso
            profesor(id: Int): Profesor
        }
    `

        module.exports = typeDefs
**@DEPRECATED(REASON:COMENTARIO)**

La directiva @deprecated indica a GraphQL que el campo con esta directiva es un campo obsoleto o que está en desuso … a manera de advertencia, y a pesar que no se muestra en la documentación de GraphiQL, aún se podría consultar y pedir en los resultados porque aún forma parte del esquema (por el momento, aunque no será así en el futuro)

**MOCK**
La herramienta de addMockFunctionsToSchema viene con el paquete de apollographql, y permite emular el retorno de las queries.
       
    addMockFunctionsToSchema({
        schema,
        mocks:{
            Curso: () =>{
                return{
                id:1,
                titulo:'grapxxx'
                }
            }
        }
    })

Tenemos también la librería Casula que permite general nombres falso para dev.

**SQLITE**
Permite trabajar con DB SQL en un archivo.
            
     yarn add knex objection sqlite3

**KNEX**

Paquete que ayuda con la migración en DBs 


**añadir mutation**

Definimos la query 

    type mutation{
        profesorAdd( porfesor:Nuevoprofesor) :profesor
    }
En una mutation siempre devuelve el objeto a cambiar.

Definimos los campos Nuevoprofesor en el Schema de profesor
    
    input Nuevoprofesor{
        Nombre: String!
        Nacionalidad: String!
        genero: Genero //Genero está definido en Schema como enum
    }

Modificamos los Resolver para tratar la query

    Mutation:{
        profesorAdd:(_, arg) =>{
            return Profesor.query().insert(args.profesor)
        }
    }
**objectionJS** Hasta el día de hoy Objetion en su documentación API recomenienda que las operaciones de persistencia CRUD a la BD se hagan de forma asíncrona ( con justa razón debido al single Thread) para evitar esto cambia el código por este en el resolver.js:

    profesorAdd: async (_, args) => {
        //console.log(args)
        const profesorAdded = await Profesor.query().insert(args.profesor)
        return profesorAdded
        }

**Edit Mutation**

Definimos la query 

    type mutation{
        profesorEdit(profesorId, profesor:ProfesorEditable):profesor
    }
En una mutation siempre devuelve el objeto a cambiar.

Definimos los campos Nuevoprofesor en el Schema de profesor
    
    input ProfedorEditable{
        nombre: String
        nacionalidad: String //No hacer requerido * para edit
        genero: Genero //Genero está definido en Schema como enum
    }

Modificamos los Resolver para tratar la query

    Mutation:{
        profesorAdd:(_, arg) =>{
            return Profesor.query().patchAndFetchById(args.profesorId, args.profesor)
        }
    }

La query en este caso sería así

    mutation NombreQuery{
        profesorEdit(profesorId:1, profesor:{
            nombre:"Juan"
        }){
            //lo que nos devuleve la query
            id
            nombre
        }
    }

**Delete Query**

La query sería así:

    mutation BorrarProfedor{
        profesorDelete(profesorId:1){
            nombre
        }
    }

Con apollo el delete devuelve el nombre de filas eliminadas, para retornar un valor de ese objeto borrado hemos de hacer un findById antes y guardarlo.

En resolver añadimos:

    profesorDelete(_,args) =>{
        return Profesor.query().findById(args.profesorId)
        .then((profesor)=>{
            return profesor.query().deleteById(args.profesorId)
            .then(()=> profesor)
        })
    }
**SEARCH QUERY**

La query sería así:

    {
        buscar(query:"GRAPHQL"){
            __typename
            ... on Profesor{
                nombre
            }
            ... on Curso{
                titulo
            }
        }
    }

En resolver añadimos:

    buscar: (_, args) =>{
        return [
            Profesor.query().findById(1)
            Curso.query().findbyId(1)
        ]
    }

    ResultadoBusqueda:{
        __resolvetype:(obj)=>{
            if(obj.nombre) return profesor //usar un parámetro único
            return curso
        }
    }


**APOLLO VS RELAY**
Un cliente es una librería (Js, en este caso) que nos permite tener ciertas ventajas al realizar un request a GraphQL

Consultas más fáciles
Caching
Normaliza datos
Maneja Optimistic UI
Helpers para manejar paginación.
Los más usados son Apollo y relay.

--Relay--

Creado por fb
Es el cliente más maduro
Optimizado para alto performance
Solo para React

--Apollo--

Creado por Meteor
API sencilla
Funciona con cualquier framework y vanilla js
Estructura flexible
Adopción incremental
Tiene clientes para iOS y android


**CHEATSHEET**

https://raw.githubusercontent.com/sogko/graphql-shorthand-notation-cheat-sheet/master/graphql-shorthand-notation-cheat-sheet.png

<img src="https://raw.githubusercontent.com/sogko/graphql-shorthand-notation-cheat-sheet/master/graphql-shorthand-notation-cheat-sheet.png">

**GRAPHQL VOYAGER -> HACE ESQUEMA DE UN GRPAHQL**

https://github.com/APIs-guru/graphql-voyager

**LISTA DE LINKS DE LIBRERIAS PARA GRAPHQL**

https://github.com/chentsulin/awesome-graphql