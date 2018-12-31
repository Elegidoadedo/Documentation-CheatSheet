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
