¿Que es NodeJS?
Ambiente de ejecución de código (Utilitario de un sistema operativo que ejecuta Javascript linea a linea)
Proyecto comunitario (Es un proyecto mantenido por una gran comunidad)
Cambio de paradigma (Distinta forma de utilizar Javascript)

Antecedentes
1995 a 2009 : Javascript en cliente
2009 : Origen de Node JS (Ryan Dahl)

Características
Libre (Open Source)
Realtime (Nativamente)
Orientado a eventos
Asíncrono
Multi-plataforma
Server-Side (Su función principal)
Robusto
Escalable
Expandible (Posibilidad de agregar módulos o plugins)
No bloqueante

Comunidad
NodeJS Fundation (Comunidad que le da respaldo,mantenimiento y soporte)

Próximas actualizaciones
Soporte para HTTP/2
Mejor manejo de módulos

HISTORIA Y ARQUITECTURA DE NODE


NodeJS: Aplicativo que hace uso de muchas librerías para ejecutar código JavaScript.

Dentro de sí contiene un motor V8 que es el encargado de ejecutar el Javascript.

Mantiene una arquitectura similar a un cliente web tradicional pero con el agregado que es capaz de ejecutarse fuera del ambiente de clientes web.

NodeJS está escrito en c++

Arquitectura
Desde el nivel mas alto al mas bajo encontramos:

Aplicación NodeJS
Librería estándar de NodeJS (API)
Enlaces de Node (Bindings)
Bindings: Enlaces que existen entre el código javascript y los módulos en mas bajo nivel
V8: Motor javascript y Librerias c/c++
LIBUV: librería que se encarga de manejar el bucle de eventos

Bucle de eventos

timers: Maneja los temporizadores de javascript
pending callbacks: Ejecuta los callbacks que están pendientes
idle, prepare: Usado en estado interno de node
poll: Es el que se comunica con las otras librerías de c++
check: Verificacion
close callbacks: Cierra los callbacks que ya han sido terminados.
Aplicaciones

Non Real Time Applications -->Generalmente aplicaciones Cliente-Servidor
Real Time Applications (RTA) --> Aplicaciones que utilizan canales bidireccionales de comunicación


REPL: “Read-Eval-Print-Loop”), también conocido como alto nivel interactivo o consola de lenguaje. (Wikipedia)

CLI: La interfaz de línea de comandos (en inglés, command-line interface, CLI) es un método que permite a los usuarios dar instrucciones a algún programa informático por medio de una línea de texto simple. (Wikipedia)



“Un objeto Promise representa un valor que puede no estar disponible aún.”

Internamente, Promise puede encontrarse en uno de tres estados:

Pending, cuando el valor final no está disponible aún. Este es el único estado que puede cambiar a uno de los otros dos estados.
Fulfilled, cuando y si el valor final esté disponible. Un valor fulfillment viene asociado permanentemente con Promise. Este puede ser cualquiera, incluyendo undefined.
Rejected, si un error impidió que el valor final se determine. Una valor rejection viene asociado permanentemente con Promise. Este puede ser cualquier valor, incluyendo undefined, aunque por lo general es un objeto Error, como en el manejo de excepciones.


Tipo de errores:

Standar Javascript errors
Errores de sintaxis, de evaluación, contrucción de URIs, etc.

System errors
Cuando se falla en la lectura de algún archivo, etc.

User-specified errors
Cuando lanzamos un Throw y especificamos un mensaje personalizado.

Assertion Errors
Errores que definen aspectos lógicos dentro de Node.js. Violaciones de lógica como TRUE == FALSE, por ejemplo

Código de estado HTTP
1xx: Information
2xx: Successful
3xx: Redirection
4xx: Client error
5xx: Server error

Detalle de cada código
https://developer.mozilla.org/es/docs/Web/HTTP/Status
https://i.imgur.com/bBN3VIq.png