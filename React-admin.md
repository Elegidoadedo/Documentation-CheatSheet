<h1>REACT-ADMIN APUNTES</h1>

* Utiliza Redux como gestor de estado.

* Admite JSON, API, HAL y ODATA

dataProvider -> propiedad obligatoria en el componente Admin y ha de devolver una promise. Contiene la dirección de la fuente de información (JSON, API, etc)

<code>dataProvider= (type, resource, params) => new promise();</code>

<h2>Admin Component </h2>

Props:

<b>dashboard</b> -> Normalmente se muestra como default su 1er child asociado, pero con dashboard podemos cambiarlo.

<b>catchAll</b> -> Cuando no encuentra la URL como Resource, muestra este componte asociado.

<b>loginPage</b> -> Es la pantalla de Log in

<h2>Admin Component </h2>

Utilza react-router, y obtiene info del parent Admin como el dataProvider

Props:

<b>name</b> -> Obligado. Hace un fecth en dataProvider con este campo
<b>list</b> -> Hace un listado de los listados
