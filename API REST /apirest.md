<h1>API </h1>

Normalmente en formato JSON o XML.

* **Funciones:**
    * Ofrecer datos a Apps
    * Ofrecer datos de forma Standard a otros desarolladores
    * Consumir datos ed otras webs o aplicaciones

<h2>API REST </h2>

 * **Características:**
    * REST = REpresentational State Transfer
    * Arquitectura que se apoya en HTTP
    * REST se compone de una lista de reglas que se deben incluir en el diseño de la arquitectura de la API
    * Si cumplen esta arquitectura de les llama **Servicios web restful**.

<h3> ACCESO A RECURSOS: </h3>
Se implementan con llamadas a la API como peticiones HTTP, donde la URL  representa el recurso.

    ej: http://www.dominio/api/recurso/1

El método HTTP Verb lo representa como un GET y el código de estado HTTP representa el resultado ( 200 -> Ok 404 -> Not Found)

<h3> CREACIÓN DE RECURSOS: </h3>

La URL estará abierta (el recurso no existe) y se realiza por el método POST.

        RESULTADOS:
        201 -> recurso creado OK
        400 -> Peticion incorrecta
        403 -> Acceso Prohibido
        500 -> Server error

<h3> ACTUALIZACIÓN DE RECURSOS: </h3>

Tenemos 2 métodos:

* Método PUT -> Cambiará todos los datos
* Métdo PATCH -> Solo cambiará algunos campos.

        RESULTADOS:
        200 -> Recurso modificado OK
        201 -> recurso creado OK
        400 -> Peticion incorrecta
        403 -> Acceso Prohibido
        500 -> Server error

<h3> ELIMINACIÓN DE RECURSOS: </h3>
* Modo DELETE

        RESULTADOS:
        200 -> Recurso eliminado OK
        400 -> Peticion incorrecta
        403 -> Acceso Prohibido
        500 -> Server error

Si el DELETE funciona ( code 200), al realizar un método GET en ese recurso ha de decolver un error 404.

<h2>ARQUITECTURA REST</h2>

* Peticiones sin estado
    * -> Mejor rendimiento, el server no recuerda peticiones anteriores.
* Interfaz uniforme
    * -> Se basa en recursos
* Cacheable
    * -> Las respuestas se deben marcar como cacheables o no. Ahorraremos peticiones.
* Sistema de capas
    * -> Se puede conectar desde el front o desde intermediarios, no afecta. El sistema de capas permite crear cachés, balanceos de carga, seguridad,etc.
* Separar l Front del Back
    * -> Los desarrollos se hacen por separado, no afectan a la API.

<h2>TIPS:</h2>

* Hacer versiones de API:

        ej: GET /V1/X/1.1
            GET /V2/X/1.1

        Así no nos cargamos posibles trabajos de los desarolladores externos que acceden a la API.

* Devolver siempre un código de estado HTTP (método PUT devuelve 201!)

* Añadir mensajes de error.

* Hacerlo en JSON, en XML hay que crear Schemas, Namespaces,...

* No se "permite" consultas entre dominios -> Uso de JSONP o CORS



