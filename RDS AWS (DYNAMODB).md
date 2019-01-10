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
**AURORA**


AWS recomiendo a Aurora (está desarollada por ellos) asegurando 5x velocidad a motores SQL y 3 x a mototres POSTGRESQL

Además de ser una base de datos muy potente y robusta, Aurora nos permite un nivel de customización muy alto, puede crecer hasta 64 TB y nuestra data esta replicada en múltiples Az.

    Otras características de Aurora:

        - Autoreparación: Guardar la información de la parte dañada en otra parte del disco y reparar el problema automáticamente.
        - Cache Warm: Hacer un precalentamiento de la caché al iniciar las consultas más comunes y sus resultados.
        - Recuperación de accidentes: Si falla la instancia principal, Aurora promueve una réplica de lectura o crea una nueva instancia principal.

        
**DYNAMODB**

DynamoDB es el servicio para bases de datos NOSQL de AWS completamente administrado (AWS se encarga de todo el background para que nosotros trabajemos nuestra aplicación), compuesto de varios nodos y distribuido en varias regiones (altamente disponible con replicación en diferentes locaciones), es una base de datos de baja latencia con almacenamiento en caché y es completamente escalable sin downtime de nuestra aplicación.

Este servicio se basa en dos conceptos importantes: las unidades en lectura (RCU, 4kb de bloques por segundo) y las unidades de escritura (WRU, 1kb de bloques por segundo). Con base en estos dos parámetros se determina el costo de nuestras bases de datos y el autoescalamiento.

La unidad fundamental de DynamoDB son las tablas, que están compuestas por items, que están compuestos por atributos (por ejemplo, la tabla trabajadores está compuesta por, trabajadores, cada uno con su nombre, edad, identificación y toda su información). También debemos entender los conceptos de partition key (llaves primarias para el espacio de almacenamiento) , sort keys (para organizar y ordenar la información) y local and global secondary index (otros atributos que podemos utilizar junto a las partition keys u otros atributos para obtener información más especifica y con mejor rendimiento).

    - **Consitencia de Lectura**

La consistencia eventual de lectura NO puede mostrar los resultados de una tarea de escritura reciente cuando consultamos una tabla recién actualizada, además, consume los 4kb de bloques por segundo en las unidades de lectura.

Por otra parte, la consistencia fuerte de lectura funciona correctamente cuando consultamos una tabla y recibimos la respuesta más reciente, pero consume el doble que la consistencia eventual, así que será más costosa. Este tipo de consistencia es el adecuando para aplicaciones y casos de uso muy específicos donde la consulta y la escritura deben estar tan sincronizadas como sea posible.

CASOS DE USO PARA DYNAMODB

El servicio de DynamoDB es muy útil en los siguientes casos:

Aplicaciones móviles
Internet de las cosas (IoT, gracias al real time y su capacidad para ingesta de información)
Aplicaciones Web
Gaming (gracias a su alta disponibilidad, conexión y por ser no relacional)
Manejo de sesiones
RealTime (ya que no solo nos permite almacenar nuestra información, también podemos utilizar toda la data en tiempo real para alimentar otros servicios y generar otras arquitecturas)


PARTICIONES DYNAMO

    - En DynamoDB las tablas se almacenan en particiones 📦
    - La base de datos asigna las particiones de cada tabla y puede aumentar su tamaño para mejorar el desempeño o añadir más particiones cuando la partición esta llena 🛳
    - Las particiones pueden aumentar su tamaño hasta 10GB siempre y cuando no superemos los 3.000 niveles de lectura y 1.000 de escritura 🐘
    - Para almacenar elementos utilizamos claves principales simples o compuestas, DynamoDB utiliza estas claves para asignar las particiones 🤔
    - Entre más aleatorias sean las claves principales, mejor performance tiene la base de datos 🎉
    - Cuando utilizamos claves compuestas, el orden de los elementos depende de la clave de ordenación 💡


**scan**

Las Operaciones Scan se encargan de escanear por completo nuestras tablas para examinar todos sus elementos y comprobar si presentan los valores solicitados, pero son muy poco eficientes ya que utilizan bastantes unidades de lectura y aumentan los costos de nuestra base de datos, debemos evitar estas operaciones para tablas grandes.

AWS nos recomienda realizar operaciones pequeñas a lo largo del tiempo en vez de hacer una sola operación muy larga, también podemos configurar límites de tamaño para evitar los escaneos completos y duplicar nuestras tablas para realizar estas operaciones sobre tablas no principales y no afectar su rendimiento.

    - Las operaciones scan examinan los elementos de nuestras tablas para comprobar sus valores 🤓
    - Son completamente ineficientes y deberíamos evitarlas 👎 😥😠
    - Pueden gastar todos los niveles de lectura de la base de datos
    - Haciendo operaciones pequeñas a lo largo del tiempo y configurando límites podemos evitar el escaneo completo y subir los precios 🤔
    - Si duplicamos las tablas para las operaciones NO afectamos el performance de las tablas principales 🆗

**QUERY**

Las Operaciones Query (operaciones de consulta) nos permiten buscar elementos en cualquier tabla o índice secundario en base a su clave principal compuesta para optimizar la petición.

En vez de escanear toda la tabla (como en las operaciones Scan), vamos a especificar los criterios de búsqueda utilizando una expresión de condición clave (una cadena que determina los elementos que vamos a leer en la tabla o el índice), especificamos el nombre y valor la clave de partición como una condición de igualdad, podemos realizar consultas utilizando diferentes operadores para encontrar los resultados con mejor precisión.

También podemos limitar el número de elementos que esperamos en los resultados para agilizar las operaciones, pero no obtenemos información tan detallada de la capacidad de lectura que consumimos.

El desafío de esta clase es responder en la sección de comentarios un caso de uso de DynamoDB y cuáles serian sus ventajas frente a los servicios RDS.

**STREAMS Y REPLICACIÓN**

DynamoDB Streams nos proporciona una secuencia ordenada por tiempo de cambios de los elementos de cualquier tabla, es decir, guarda los cambios de nuestros elementos para que podamos procesar y consumir esta información, podemos ampliar el poder de DynamoDB con replicación entre regiones, análisis continuo con integración a Redshift, notificación de cambios y muchos otros escenarios.

Estos streams capturan una secuencia en orden cronológico de las modificaciones de los elementos de una tabla y almacenan la información por 24 horas. Cada registro de secuencia contiene la información sobre una sola modificación a los datos de un elemento de la tabla. Nuestras aplicaciones pueden obtener acceso a este registro y ver los elements de datos tal y como se encontraban antes y después.

**DAX o DINAMODB ACCELERATOR**

DAX (DynamoDB Accelerator) es un cluster de caché completamente administrado por AWS y de alta disponibilidad para DynamoDB con un rendimiento de hasta 10 veces superior (de milisegundos a microsegundos) y soporta millones de solicitudes por segundo.

Entre sus características encontramos la encriptación en reposo, podemos utilizar hasta 10 nodos y se puede seleccionar la zona de disponibilidad donde se desplegará el cluster. Podemos utilizar instancias small y medium para cargas de prueba, de resto todas son de tipo R (optimizadas en memoria).


**CONCLUSIONES:**

- Conclusiones del servicio RDS:

Siempre que desplegamos bases de datos en producción es muy recomendado utilizar los despliegues en diferentes zonas con el servicio Multi AZ.
Tenemos diferentes estrategias para optimizar el performance de nuestra base de datos, por ejemplo, implementar réplicas de lectura, utilizar bases de datos en memoria y dividir la base de datos en otras más pequeñas.
El periodo de retención de los backups de nuestra base de datos son máximo 35 días.
Debemos tener en cuenta los tipos de migración (homogéneas y heterogéneas) cuando vamos a migrar nuestra base de datos.
AhororaDB es la base de datos más robusta y potente para grandes cargas de trabajo de AWS, también es la única con servicio de serverless y autoescalamiento.

- Conclusiones del servicio DynamoDB:

Es recomendado evitar las operaciones Scan para no afectar la capacidad aprovisionada, en cambio, las operaciones Query funcionan mucho mejor para el rendimiento de la base de datos.
La función de autoscaling se puede programar con lectura y escritura pero debemos tener en cuenta los costos.
Es clave elegir una llave principal adecuada para no afectar el performance de nuestra base de datos, entre más aleatoria sea este valor, mejor será el rendimiento.
Con DynamoDB Streams podemos crear arquitecturas en tiempo real para diferentes aplicaciones.
Cuando tenemos una tabla muy grande, configurar el particionamiento y los límites del mismo son fundamentales.
