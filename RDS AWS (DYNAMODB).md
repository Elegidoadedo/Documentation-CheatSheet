<h1>Características de RDS</h1>
RDS (Relational Database Service) es un servicio de AWS enfocado a bases de datos relacionales con compatibilidad a 6 motores de bases de datos: Amazon Aurora, MySQL, MariaDB, PostgreSQL, Oracle y Microsoft SQL Server, cada uno con sus características, integraciones y limitaciones.

Entre sus características principales podemos destacar los backups automáticos con un tiempo de retención de hasta 35 días, es decir, si encontramos algún problema con nuestras bases de datos podemos restablecerlas a la hora, minuto y segundo que necesitemos dentro del periodo de retención. Recuerda que por defecto este periodo es de 7 días. También tenemos la opción de hacer backups manuales, podemos tomar snapshots manuales en cualquier momento si nuestra aplicación lo necesita. Además, AWS por defecto tomará un snapshot final de nuestras bases de datos antes de eliminarlas, así podremos restablecerla si tenemos algún inconveniente.

Todas las bases de datos relacionales utilizan un sistema de almacenamiento, si la carga de lectura y escritura son constantes, el sistema General Purpose funciona muy bien, sin embargo, podemos utilizar el sistema Provisioned Storage cuando requerimos de altas cantidades de consumo y operaciones de disco.

RDS es un sistema completamente administrado, esto quiere decir que AWS reduce nuestra carga operativa automatizando muchas tareas de nuestra base de datos, por ejemplo, las actualizaciones. A nivel de seguridad contamos con muchas opciones, una de ellas es la posibilidad de encriptar nuestra base de datos para que solo nosotros y las personas o roles que especifiquemos tengan acceso.

También tenemos integración con otros servicios de AWS, por ejemplo, IAM para administrar a los usuarios, roles, grupos y políticas de conexión a la base de datos por medio de tokens con máximo 20 conexiones por segundo (recomendado para escenarios de prueba), o la integración de Enhanced monitoring para hacer monitoreo en tiempo real nuestras bases de datos (recuerda que además de subir el precio, no está disponible para instancias small).


Por defecto hace backups diariamente y lo retiene 7 dias. Puedes ampliar a 35 días de retención. También es posible ahcer un snapshot manual de la base de datos.

Integracion con IAM mediante tokens de 10 a 20 conexiones por segundo.

Motores de DB admitidos -> Amazon Aurora, MySQL, MariaDB, PostgreSQL, Oracle y Microsoft SQL Server

IOPS -> input/output operations per second is an input/output performance measurement used to characterize computer storage devices like hard disk drives, solid state drives, and storage area networks.


RDS CON SQL

Puerto por defecto SQL 3306

Cuando utilizamos el servicio RDS con el motor de MySQL podemos crear multiples bases de datos con un solo endpoint (una sola conexión), ya que entre las características de este motor encontramos la cantidad de bases de datos ilimitada. Obviamente, debemos tener en cuenta que nuestras instancias deberían soportar la cantidad de bases de datos que vamos a utilizar, y las herramientas de monitoreo nos pueden ayudar a medir esta relación de tamaño y rendimiento.

Recuerda que si necesitamos un permiso de usuarios diferente para cada base de datos vamos a necesitar configuraciones diferentes en las keys (llaves de acceso) de nuestra instancia.

A nivel de monitoreo, AWS nos provee un servicio llamado CloudWatch que nos permite visualizar los niveles de lectura, escritura, CPU, disco y memoria de la instancia dónde corre nuestra base de datos, también podemos analizar las métricas de conexiones para determinar la carga y la concurrencia de nuestras instancias.

La primer estrategia para mejorar el performance son las replicas de lectura, copias asíncronas de nuestra base de datos principal con un nuevo endpoint que vamos a utilizar solo en tareas de lectura, así obtenemos mucha más disponibilidad para tareas de escritura en nuestra base de datos principal. Recuerda que este servicio no esta disponible para los motores de Oracle y SQL Server.

También podemos mejorar el storage de nuestra base de datos utilizando provisioned iops para soportar altas operaciones de entrada y salida sobre la base de datos, principalmente para transacciones OLTP (OnLine Transaction Processing).

Existen otras alternativas como las bases de datos en memoria (ElastiCache, por ejemplo). Estas opciones resultan muy útiles para guardar la información más consultada en cache, así aliviamos un poco la carga de nuestra base de datos principal. Si estamos muy saturados y agotamos todas las opciones para mejorar el performance, la recomendación es dividir nuestra base de datos en otras más pequeñas.

Multi AZ nos permite tener alta disponibilidad de nuestra base de datos, creando bases de datos replica que automáticamente vamos a utilizar cuando la base de datos principal tenga problemas 📡.
Recomendado para ambientes de producción 💥.
La replicación es síncrona 🎏.
Los backups se hacen en la base de datos Standby(la que no estamos utilizando) 👍.
El precio es el mismo que al tener dos bases de datos 😱.
No confundir con las replicas de lectura 😅.


DMS (Database Migration Service) es un servicio de AWS que nos permite migrar nuestras bases de datos con otros motores al servicio de RDS u otros servicios de bases de datos en AWS.

Este servicio tiene las siguientes características:

    - Podemos realizar migraciones de bases de datos on premise o en la nube a los servicios de bases de datos en AWS sin afectar el downtime de la base de datos que - vamos a migrar.
    - La carga de trabajo durante las migraciones es adaptable.
    - Solo pagamos por los recursos que utilizamos en la migración.
    - AWS administra la infraestructura necesaria para el trabajo de la migración, Hardware, Software, parches, etc.
    - Conmutación por error automática, si AWS detecta un error en el proceso automáticamente creará una nueva instancia para remplazar la anterior, así el proceso de - replicación no se ve afectado por estos problemas.
    - Los datos en reposo están cifrados con KMS (Key Management Service) y la migración utiliza el protocolo de seguridad SSL.


Las migraciones homogéneas son migraciones donde la base de datos de origen y la de destino puede tener diferentes versiones del mismo motor, o son bases de datos compatibles entre sí (MySQL y Aurora, por ejemplo).

También podemos realizar migraciones heterogéneas, donde la base de datos de origen no es compatible con la de destino. Estas migraciones NO siempre son posibles, y antes de realizar la migración vamos a necesitar convertir el esquema de la base de datos con la herramienta AWS Schema Conversion Tool.   