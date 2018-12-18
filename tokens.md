<h1>TOKENS & COOKIES</h1>

* Los tokens de han de guardar, ya sea en local, en la sesión o en las cookies.

Se pueden usar las cookies no como método de auth si no como mecanismo de almacenamiento del token. Así evitamos ataques XSRF.

* Los tokens caducan como las cookies, pero tienes más control sobre ellos.

Deben caducar ya que sinó cualquier usuario podría acceder para siempre a la API si alguna vez se conectó.

DIFERENCIAS ENTRE TOKENS Y COOKIES

* COOKIES

    Workflow

        Las cookies se pueden destruir al cerrar el browser.

                            | |
                             V
        Puedes crear un control de vida (life cycle control) en el servidor y manipular su ciclo de vida.

                            | |
                             V
        Las cookies , de esta forma, sobreviven al cierre del browser, hasta el fin de su expiración.


* TOKENS  ( Si el token caduca, simplemente generas uno nuevo)

        Validar el antiguo Token
        
                | |
                 V
        Verificar que el usuario existe y que no tiene restrinción (no esté borrado, esté activo, etc)
                | |
                 V
        Asignarle el nuevo Token al usuario con una fecha de expiración.


Las COOKIES LOCALES no puede pasarse a través del dominio.

Por ejemplo, no puede pasarle una cookie de dominio.com a app.dominio.com

Para solucionar esto, podemos crear una COOKIE DE DOMINIO mediante un token.

WORKFLOW:

    $.post('/authenticate', function() {
    // store token on local/session storage or cookie
    ....

    // create a cookie signaling that user is logged in
    $.cookie('loggedin', profile.name, '.yourdomain.com');
    }); 



Logeamos en app.dominio.com => Generamos un token y klo asginamos en una cookie en dominio.com => Volvemos a app.dominio devolviendo el token


Evitar que cada request contenga en el Auth la información en el header, mediantes las propiedades de "OPTIONS".

Para hacer Streams hacerlo con una request firmada con token

Con als cookies puedes descargar archivos son problemas pero si se hace mediante XHR no puedes. La solución es crear una request ( Como hace AWS) se puede hacer con el Framework de Haws (github => huniverse/hawk ) que ayuda a crearlo.

Creas un ticket con caducidad compuesto por => host + path + query + headers + timestamp + HMAC

WORKFLOW:

Creas un ticket (5 min de caducidad) => redirect ala página de descarga => Verifica que el token no ha caducado o tiene permiso => comienza la descarga o carga error.


ATAQUES *XSS* VS *XSRF*

Los ataques XSS son más fáciles de lidiar. XSS inyección de código en formularios. XSRF ataque de robo de cookies de sesión y credenciales.

* Las cookies están configuradas como "HTTPOnly", por lo cual solo se puede acceder desde el servidor y no por JavaScript, de esta forma no suf5re el ataque XSS.

* Los Tokens guardados en el local-Cookies sí que pueden sufrir ataques XSS, por este motivo es ideal hacer caducidades muy bajas.


TOKEN EN REQUESTS CON "PESO"

La cookies tienen una ID => connect.sid o PHPSESSID => Pero el contenido se almacena en el servidor.

también se puede implementar esta opción con los tokens, es más controlable ya que has de crearlo.

Si contiene información confidencial el token, es mejor encriptar el token. TLS/SSL previene los ataques Man-in-the-middle.


    app.post('/authenticate', function (req, res) {
    // validate user

    // encrypt profile
    var encrypted = { token: encryptAesSha256('shhhh', JSON.stringify(profile)) };

    // sing the token
    var token = jwt.sign(encrypted, secret, { expiresInMinutes: 60*5 });

    res.json({ token: token });
    }

    function encryptAesSha256 (password, textToEncrypt) {
    var cipher = crypto.createCipher('aes-256-cbc', password);
    var crypted = cipher.update(textToEncrypt, 'utf8', 'hex');
    crypted += cipher.final('hex');
    return crypted;
    }

    //En el código se hace encrypt-then-MAC, ya que si se realiza al revés, MAC-then-encrypt es vulnerable a los atauqes Vaudenay-Style.

OAUTH Y TOKENS

OAUTH es un protocolo de autorización que devuelve un access_token y puede hacer llamadas a APIs en su nombre.

Estos Tokens se les llama BEARERS TOKENS (Tokens de portador) y se componen de Strings randoms que se almacen en una Tabla Hash en el servidor junto a su caducidad, Scope y usuario asignado. Al llamar a la API se comprueba el token en el servidor ( que no haya caducado, etc.).

La diferencia entre los BEARER TOKENS y los JWT ( Json Web Tokens) es que los JWT son stateless y no necesitan ser guardados en una Tabla Hash.

En OAUTH2 no especifica el formato de access_token así que se puede usar JWT.


Evitar usar sistema de tokens para todas las ocasiones, si hay un gran volumen de información puede ser muy complicado y tedioso el mantenimiento y la implementación en el sistema.











