<h1>Características de RDS</h1>
RDS (Relational Database Service) es un servicio de AWS enfocado a bases de datos relacionales con compatibilidad a 6 motores de bases de datos: Amazon Aurora, MySQL, MariaDB, PostgreSQL, Oracle y Microsoft SQL Server, cada uno con sus características, integraciones y limitaciones.

Entre sus características principales podemos destacar los backups automáticos con un tiempo de retención de hasta 35 días, es decir, si encontramos algún problema con nuestras bases de datos podemos restablecerlas a la hora, minuto y segundo que necesitemos dentro del periodo de retención. Recuerda que por defecto este periodo es de 7 días. También tenemos la opción de hacer backups manuales, podemos tomar snapshots manuales en cualquier momento si nuestra aplicación lo necesita. Además, AWS por defecto tomará un snapshot final de nuestras bases de datos antes de eliminarlas, así podremos restablecerla si tenemos algún inconveniente.

Todas las bases de datos relacionales utilizan un sistema de almacenamiento, si la carga de lectura y escritura son constantes, el sistema General Purpose funciona muy bien, sin embargo, podemos utilizar el sistema Provisioned Storage cuando requerimos de altas cantidades de consumo y operaciones de disco.

RDS es un sistema completamente administrado, esto quiere decir que AWS reduce nuestra carga operativa automatizando muchas tareas de nuestra base de datos, por ejemplo, las actualizaciones. A nivel de seguridad contamos con muchas opciones, una de ellas es la posibilidad de encriptar nuestra base de datos para que solo nosotros y las personas o roles que especifiquemos tengan acceso.

También tenemos integración con otros servicios de AWS, por ejemplo, IAM para administrar a los usuarios, roles, grupos y políticas de conexión a la base de datos por medio de tokens con máximo 20 conexiones por segundo (recomendado para escenarios de prueba), o la integración de Enhanced monitoring para hacer monitoreo en tiempo real nuestras bases de datos (recuerda que además de subir el precio, no está disponible para instancias small).

**El Compromiso Empieza con las Personas**

La seguridad empresarial es un compromiso de las personas. La mayoría de los ataques vienen desde dentro de la organización.

Se deben de evitar contraseñas que contengan información personal y sea muy facil de adquirir.

Existen muchos programas que ayudan a gestionar las contraseñas.

Cada vez que llegue un correo que te pide que te autentiques, primero fijarse si el texto es de uno corporativo. De igual manera, hay que verificar si el dominio es el correcto.

Para poder generar una contraseña fuerte, se puede usar How Secure Is My Password.

Los usuarios generalmente tienen un aspecto legal. Todo lo que haga con mi usuario va a tener un afecto con la información que trabaje.

**Diferencia entre Datos Personales y Empresariales**

Los datos personales son aquellos que solo me interesan a mi. Tiene que ver con mis amigos, mi familia, mi círculo social más cercano.

Ejemplos de datos personales:

Mis redes sociales
Cuentas bancarias
Recibios de teléfono, agua, luz, etc.
Información familiar
Los datos empresariales son aquellos que le importa a la empresa u organización.

Ejemeplo de información organizacional:

Redes sociales de la empresa
Datos del cliente
Estructura interna
Información financiera
Información tributaria
Algunas empresas tienen regulaciones que prohíben cualquier tipo de comunicación con algunos países.


**tipos de encriptado**
Dos tipos de encriptación
- Algoritmos Simétricos: proteger el algoritmo.

    ○ 3DES (DES triple)

    ○ IDEA

    ○ AES

    ○ Skipjack

    ○ Blowfish
    
    ○ Twofish

- Algoritmos Asimétrios. Proteger las claves.

    ○ RSA (Rivest-Shamir-Adleman). Los navegadores utilizan RSA para establecer una conexión segura.

    ○ Diffie-Hellman. Lo usan SSL, SSH, IPsec (las VPN utilizan IPsec).

    ○ ElGamal

    ○ Criptografía de curva elíptica (ECC)