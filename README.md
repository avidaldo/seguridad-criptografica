# Breve introducción a las técnicas de seguridad informática basadas en criptografía clásica

## Objetivos de los servicios de seguridad

Los servicios de seguridad son aquellos que buscan garantizar los siguientes objetivos:

- Disponibilidad: garantía de que la información va a estar disponible. Puede verse comprometida, por ejemplo, por el fallo físico de un dispositivo de almacenamiento o de una línea de comunicación.

- Integridad: ausencia de modificación o destrucción de la información. Se compromete p. ej. cuando parte de la información se corrompe y se pierde en un documento almacenado o en una transferencia de información no confiable.

- Confidencialidad: garantía de que la información solo es accesible por los destinatarios. Se suele garantizar mediante el cifrado de los datos o garantizando un canal seguro.

- No repudio, vinculación o irrenunciabilidad: garantía que las participación de las partes en una comunicación. Se pude garantizar que el emisor realizó una transferencia de información (no repudio en origen) y también que el receptor la recibió (no repudio en destino).

Cabe señalar que esta lista varía según el autor y es habitual que se añada la autenticación como un objetivo más. Sin embargo, también es habitual considerarla no como un objetivo sino como un método que puede garantizar confidencialidad (solo recibe la información quien se autentica) o no repudio (la persona que accedió es aquella que se autenticó).

## Criptografía de clave simétrica o de clave privada

Es aquella en la que la misma clave se usa para cifrar y descifrar los mensajes. El texto en claro se transforma en un criptograma ininteligible mediante cifrado, y este criptograma puede ser descifrado usando la misma clave.

El gran problema que presenta es el del intercambio de claves, ya que para poder enviar información, los participantes tienen requieren estar en posesión de la clave, que deberá haberse transmitido previamente.

Algoritmos relevantes son DES (ya roto) y AES (el estándar actual).

## Criptografía de clave asimétrica o de clave pública

La criptografía asimétrica soluciona el problema de la distribución de la clave privada entre los participantes en la comunicación. En estos sistemas cada participante cuenta con un par de claves propias, clave pública y clave privada: siendo cada una la que permite descifrar mensajes cifrados por la otra.

Para conseguir Confidencialidad e Integridad, un mensaje es cifrado con la clave pública del receptor, que es el único que conoce su clave privada y por tanto el único que puede descifrar el mensaje.

Si lo que se quiere es conseguir autenticación y no repudio el proceso sería el inverso. El emisor utiliza su clave privada para cifrar el mensaje. Dado que esta clave es solo conocida por él, cuando el receptor lo descifra con la clave pública del emisor, sabe que el mensaje está vinculado necesariamente a éste.

Algunos de los algoritmos más relevantes son RSA y DSA.

## Criptografía híbrida

Dado que los sistemas de cifrado asimétricos son computacionalmente más costosos que los simétricos y que éstos tienen el problema del intercambio de claves, existen sistemas híbridos donde se usa un sistema de clave asimétrica para intercambiar de forma segura una clave privada de sesión que se usará para cifrar el resto de la comunicación de forma más eficiente. Ejemplos de este sistema son los protocolos SSH y SSL/TLS (capa de seguridad que utiliza HTTPS).

## Función Hash y huella digital

Una función hash convierte un conjunto de datos de cualquier tamaño en otro de longitud fija. El valor devuelto se llama resumen, suma hash o hash o huella digital y debe cumplir:

- que no se pueda calcular los datos originales a partir del resumen
- que no se pueda encontrar fácilmente otro documento diferente del original y con sentido con el mismo resumen.

Estas características permiten utilizarlos para:

- comprobar la integridad de un fichero: el receptor calcula el resumen del fichero recibido y comprueba que coincide con el hash facilitado por el emisor.
- identificación de ficheros, comparar los hashes de dos ficheros permite saber si se trata del mismo más rápido que comparando el original.
- almacenamiento de contraseñas: en lugar de almacenar la contraseña, se almacena su hash, de modo que aunque se tenga acceso al almacén (el administrador del sistema o un atacante), no se conozca la contraseña del usuario.

Los algoritmos más usados son MD5 (actualmente no seguro) y SHA (considerado seguro en sus versiones SHA-2 y SHA-3)

## Firma digital

Una firma digital es un bloque de caracteres que acompaña a un documento. Su funcionamiento es el segundo de los explicados para los cifrados de clave pública, pero para no cifrar todo el documento, lo que resultaría bastante lento en caso de documentos grandes, se firma un resumen hash del documento original. De este modo, la firma digital permite garantizar la autenticidad del documento, su integridad y el no repudio por parte del emisor.

## Certificados de clave pública y PKI

Para la distribución de claves públicas, se suele acudir a una autoridad de certificación (CA), que emite un documento digital firmado que certifica la vinculación de una clave con una identidad real. Estos documentos se conocen como certificados de clave pública y contienen datos del usuario, clave pública y el algoritmo usado en su generación, datos de la entidad que emite la certificación.

Una infraestructura de clave pública (PKI) está constituida por las CA y otras entidades que mantienen una infraestructura para recibir solicitudes, verificar identidades y emitir documentos digitales que certifiquen el registro de la clave pública con la identidad del solicitante. El principal estándar de define el funcionamiento de una PKI es X.509 de la UIT (Unión Internacional de Telecomunicaciones).
