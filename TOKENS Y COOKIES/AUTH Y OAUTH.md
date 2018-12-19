<h1>AUTH </h1>

* Se pueden hacer por cookies (lo más común) o por Tokens

Beneficios de Tokens:
* Cookies y CORS no se llevan bien entre dominios.

<img src= "https://juanda.gitbooks.io/webapps/content/api/cookie-token-auth.png"/>
<h2> OAUTH </H2>

* Standard en APIs REST abiertos a terceros
* Se basan en el uso de Tokens
* sirven para acceder a servicios de terceros sin que el usuario tenga que dar sus credeenciales a esta app.

En el proceso intervienen tres "actores":

* Consumer:
    * -> El servicio al que se quiere acceder.
* Service Provider:
    * -> Se le llama al servicio de auth externo.
* Final User.

WORKFLOW:

CONSUMER pide un token a SERVICE PROVIDER.

COSUMER  redirige a USER a una página segura con el token como parámetro.

USER se autentifica en la página del SERVICE PROVIDER validando el Token.

SERVICE PROVIDER reenvia al USER  a la página solicitada en 'oauth_callback'.

COSUMER recoje al USER en el callback con el Token.


