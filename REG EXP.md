Cadena de Caracteres: Es un carácter ASCII generalmente, seguido de otro carácter y de otro. No todos son visibles, el espacio por ejemplo. Cada carácter es un carácter.

El caracter (.): Encuentrame todo lo que sea un carácter


Dígitos:\d

Encuentra todos los dígitos de 0 a 9.
\d es equivalente a poner [0-9].
Si en vez de \d, usamos por ejemplo [0-2] nos encontrará solamente los dígitos de 0 a 2.
Podemos usar “\D” para encontrar justo lo contrario, todo lo que no son dígitos.
Palabras:\w

Encuentra todo lo que puede ser parte de una palabra, tanto letras (minúsculas o mayúsculas) como números.
\w es equivalente a poner [a-zA-Z0-9_].
Si en vez de \w, usamos por ejemplo [a-zA-Z] nos encontrará solamente las letras.
Podemos usar “\W” para encontrar justo lo contrario, todos los caracteres que no son parte de palabras.
Espacios:\s

Encuentra todos los espacios (los saltos de línea también son espacios).
Podemos usar “\S” para encontrar justo lo contrario, todo lo que no son espacios.

Delimitadores:

(*) : Cero o más veces
(?): Cero o una sola vez
(+): una o más veces.
Aplican al carácter o sentencia que preceden

[a-z]? : Esto es que puede estar una sola vez o no estar una letra minuscula de la (a) a la (z).
\d*: Esto es que puede estar muchas veces o no estar un digito.
\d+: Esto es que puede estar muchas veces o una sola vez un digito.

<img src="https://static.platzi.com/media/user_upload/Captura%20de%20pantalla%20de%202018-06-19%2023-08-30-118ac225-25ca-4823-8112-41cbf410fbc5.jpg">

Esto :

\d{2,2}[\-\.]?\d{2,2}[\-\.]?\d{2,2}[\-\.]?
Se pudo hacer así:

	(\d{2,2}[\-\.]?){3,3}