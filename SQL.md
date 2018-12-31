**Redundancia **: Eliminación de Renundancia de Datos
Concurrencia : Posibilidad de accedes a datos de manera concurrente.
Aislamiento: Permite realizar operaciones independientes
Integridad: PK, not null, true , false o FK
Inconsistencia: Permite evitar la insconsistencia de datos (Bogotá con tilde en un registro, Bogota sin tilde en otro registro) refiriendose al mismo dato
Seguridad: Autenticación, LDAP, Kerberos
Acceso : Permite manejas esquemas de seguridad, ROLES ó noveles de accesos
Atomicidad :

DML: DATA MODEL LANGUAGE
DDL: DATA DEFINITION LANGUAGE

Mysql fue adquirido por Oracle. Maria db es una especie de fork de mysql pero cuenta con una buena comunidad.



DDL: Data Definition Language
create table Permite crear una tabla.
create view Permite crear una vista.
create procedure Permite crear un proceso.
create index Permite crear un índice.
create schema Permite crear un esquema.
Nota:Alter aplica para “table, view y procedure”. Alter = Alterar.
DML: Data Manipulation Language
select Permite seleccionar uno o muchos atributos de una o muchas tablas.
join Permite combinar registros de dos o más tablas.
insert Permite insertar en una table una nueva tupla.
update Permite actualizar uno o muchos atributos.
delete Permite eliminar uno o muchos atributos.
replace Permite reemplazar un atributo.

Bases de Datos no Relacionales (Not Only SQL)
ACID este concepto es uno de los pilares de las bases de datos relacionales.con el cual se asegura la integridad y consistencia de los datos a pesar de la concurrencia proporcionando un entorno seguro para las operaciones que realizan.
Atomicidad: Es una de las principales características de las bases de datos Relacionales, que no siempre se cumplen en las Bases de Datos NoSQL
Consistencia: no siempre una base de datos noSQL es consistente en sus datos, esto se debe a su descentralizacion. Es decir que sus datos pueden estar replicados.
Aislamiento: los sistemas de datos NoSQL no siempre utilizan aislamiento debido a que manejan de manera distinta la concurrencia, mientra que bases de datos relacionales bloquean los accesos a los datos para garantizar la consistencia de los mismos. En la bases de datos NoSQL los procesos se replican, es decir se realizan copias de los mismo para cada usuario que lo solicite.
Durabilidad: es otro principio que no aplica necesariamente en los sistemas NoSQL, esto se debe a que en algunas instancias los datos no son consistentes por lo tanto no se puede garantizar la persistencia en el tiempo de los mismos. Una manera de solucionarlo esto es replicar los datos para garantizar la consistencia y durabilidad de los datos
**CAP**
Consistency = Consistencia: Debe retornar un dato válido, me debe permitir a cualquier estructura de su base de datos
Availability = Disponibilidad: Cuando haga una solicitud no me va a importar que nodo del sistema esta up time o down time o sin funcionamiento. Un dato debe estar replicado en al menos tres nodos.
Partition = Particionamiento: Es como yo parto esa información por lo menos en tres nodos para evitar que se pierdan mensajes.

También hay que tener en cuenta que:

El escalamiento vertical (Scale UP) = requiere apagar el servidor para así aumentar sus recursos de memoria y procesamiento. Ejemplo: tengo un servidor de 1 Tera de disco y a futuro voy a necesitar mas memoria de disco, así que lo que hago es quitar esa memoria de disco de 1 Tera y remplazarlo por un disco de 2 Teras y para eso tuve que desconectar el servidor, quitar la base de datos y de mas para hacer este procedimiento quedando al final un solo disco de 2 Teras.

El escalamiento horizontal (Scale Out) = no es necesario apagar el servidor ya que permite ir acomplando mas memoria de disco sin necesidad de apagar o desconectar el servidor. Ejemplo: tengo un servidor de 1 Tera de disco y a futuro voy a necesitar mas memoria de disco, así que lo que hago es poner otro disco de 1 Tera sin necesidad de quitar el otro, en ese caso tendría dos discos de un Tera (1 Tera + 1 Tera).
