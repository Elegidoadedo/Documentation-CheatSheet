<h1>JSON WEB TOKENS</h1>


USOS DE JWT:

- Propagar una identidad entre las partes interesadas
- Propagar un usurio completo entre las partes interesadas.
- Tranferir de forma segura datos en un canal inseguro-
- Comprobar una identidad para ofrecer confianza y validación.

Ejemplo de Token:

    eyJhbGciOiJSUzI1NiIsImtpZCI6Ijc4YjRjZjIzNjU2ZGMzOTUzNjRmMWI2YzAyOTA3NjkxZjJjZGZmZTEifQ.eyJpc3MiOiJhY2NvdW50cy5nb29nbGUuY29tIiwic3ViIjoiMTEwNTAyMjUxMTU4OTIwMTQ3NzMyIiwiYXpwIjoiODI1MjQ5ODM1NjU5LXRlOHFnbDcwMWtnb25ub21ucDRzcXY3ZXJodTEyMTFzLmFwcHMuZ29vZ2xldXNlcmNvbnRlbnQuY29tIiwiZW1haWwiOiJwcmFiYXRoQHdzbzIuY29tIiwiYXRfaGFzaCI6InpmODZ2TnVsc0xCOGdGYXFSd2R6WWciLCJlbWFpbF92ZXJpZmllZCI6dHJ1ZSwiYXVkIjoiODI1MjQ5ODM1NjU5LXRlOHFnbDcwMWtnb25ub21ucDRzcXY3ZXJodTEyMTFzLmFwcHMuZ29vZ2xldXNlcmNvbnRlbnQuY29tIiwiaGQiOiJ3c28yLmNvbSIsImlhdCI6MTQwMTkwODI3MSwiZXhwIjoxNDAxOTEyMTcxfQ.TVKv-pdyvk2gW8sGsCbsnkqsrS0T-H00xnY6ETkIfgIxfotvFn5IwKm3xyBMpy0FFe0Rb5Ht8AEJV6PdWyxz8rMgX2HROWqSo_RfEfUpBb4iOsq4W28KftW5H0IA44VmNZ6zU4YTqPSt4TPhyFC9fP2D_Hg7JQozpQRUfbWTJI

Vemos que está separado por "." . Si lo decofificamos con base64url-decode obtenemos que esta separado por " : " y podemos apreciar en la primera parte:

            {“alg”:”RS256",”kid”:”78b4cf23656dc395364f1b6c02907691f2cdffe1"}

A esta parte se le conoce como JOSE ( Javascript Object Signing and Encryption ).

<h2>un JWT no existe como tal, si está firmado se le conoce como JWS ( Json Web Signature), y si no JWE (Json Web Encrytion) </h2>

Estructura de JWE:
<img src="https://cdn-images-1.medium.com/max/1600/1*-qEUNh7EYxBbnnt0Xk997g.png">

En los JWT se especifica:

typ: determina el tipo de media del JWT
cty: content type


Unsecured JWT: son en los que en el JOSE header el "alg" tiene un valor de "none", se espera que el protocolo TSL/SSL se encarge de la seguridad.

<img src="https://cdn-images-1.medium.com/max/1200/1*o4A-GOhRYlqYwVET7Jzm8Q.png">
 Esto es la segunda aprte del Token una vez pasado el base64url-decode

 

 La tercer parte del token contiene la firma. Google usa RSASSA-PKCS1-V1_5 con el algoritmo de hasheo SHA-256.


