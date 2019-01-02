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

MYSQL ESTRUCTURA DE QUERYS NIVEL NOOB

MYSQL WORKBENCH-> Aplicación que ayuda a estructurar SQL DB

Ver el mapa conceptual de una DB:
    Importar la DB, Click en Revrse Engineer. 

    En el mapa, Leyenda:

        Llave = LLave primaria
        Rombo azul=  Not null
        Rombo Rojo= Llave foranea

TIPOS DE QUERYS:

SHOW columns FROM Schema.actor <-> Muestras las keys

SELECT * FROM Schema.actor <-> Muestra los valores

SELECT actor_id, last_name FROM Schema.actor <-> Se seleccionan varips campos ( también sirve con Schemas)

SELECT actor_id, last_name FROM Schema.actor ORDER BY last_name des <-> Ordena el resultado por last_name en orden descendente

SELECT actor_id, last_name FROM Schema.actor GROUP BY last_name <-> agrupa los resultados en last_name

            SELECT last_name, count(first_name) FROM schema.actor
            GROUP BY last_name ORDER BY last_name asc;
    
    Mostrará el número de personas con el mismo apellido ordenado por apellidos.

            SELECT C.first_name, A.address
            FROM schema.Customer as C, schema.address as A
            WHERE C.address_id = A.address_id
    El comando AS se utiliza como alias, podemos seleccionar los que no se repiten con:
             SELECT DISTINT Schema.data FROM schema
    
    Podemos utilizar query parcial (que empiza por ciertas palabras, contenga o termine en X):
            
            SELECT * FROM schema.film
            WHERE title LIKE 'ZO%'
                            '%ZO'
                            '%ZO%'

 MODIFICAR UAN TABLA:

        ALTER TABLE schema.film ADD COLUMN fecha timestamp

        ALTER TABLE schema.film DROP COLUMN fecha;

MODIFACR DATOS DE TABLA:

        UPDATE schema.film set title ='nombre' WHERE film_id=2

Modificará el item con id 2

        INSERT INTO schema.film VALUES(1002, 'nombre', 'blablabla', 2019-01-02)
Creará un nuevo item con los valores del paréntesis.

Borrar un item:
        DELETE FROM schema.film WHERE film=id='1002'


JOINS 
<img src="https://static.platzi.com/media/user_upload/10-%20SQL%20Joins-5b08f55f-29fc-4307-8ea4-5195f07af1b0.jpg">


<h1> Noo SQL Aplicado</h1>


**RDBMS**: Ofrece escalabilidad en una sola máquina, mejorando así los niveles de servicio de la base de datos.

**Ventajas**

Esquemas de Replicacion
Esquemas de Backup
Esquemas de Disaster Recovery
**Desventajas **

Crecimiento Limitado
Imposibilidad de de escalar varios sistemas en un mismo equipo


**Sharding:**

Se crean pequeños módulos o paquetes que van a tener pequeñas partes de la base de datos o pequeñas réplicas.
Esto lo que hará es permitir unir otros shard a la base de datos y escalarlo más fácil.
Utiliza llaves dentro de los shard. Pueden ser tablas hash o llaves compartidas.
Las llaves compartidas generalmente se trabaja dentro del nodo maestro. Es reccomenable clusterizar el nodo maestro para tener varios por si el principal falla.
Los diferentes shard se van a comunicar con el nodo maestro, el cuál le va a dar toda la indexación. Va a tener las llaves maestras para que todos los shard funcionen en el mismo sistema.
En cada shard se pueden manejar registros o transacciones diferentes.
En una BD NoSQL no se crea una base de datos hasta que no se tenga toda la data cargada. Las colecciones están en un módulo de datos que a su vez está en una base de datos y que será distribuida.
Aparte de pensar en la consistencia de los datos se debe pensar también en una estrategia de redes y comunicaciones.
Los shards tienden a estar en máquinas separadas con puertos diferentes para que los módulos controladores puedan saber dónde están.
MongoDB se divide en Shards. Los shards se llaman Mongod. Las estructuras principales se llaman Mongos. Un cliente se conecta (por ejemplo) a través de un JPA a los Mongos. Los nodos de configuración define toda la estructura de la base de datos.