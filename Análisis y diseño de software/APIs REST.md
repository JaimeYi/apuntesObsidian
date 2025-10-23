Una API (**A**pplication **P**rogramming **I**nterface), como dice su nombre, es un conjunto de reglas y protocolos que permite que dos programas se comuniquen entre sí.
- Un punto donde dos sistemas, sujetos, organizaciones, etc. Se encuentran e interactúan.
- Son las interfaces que programas  (de software) presentan a otros programas o a humanos.
- Son diseñadas para interactuar con otros programas.
- No nos dice mucho sobre la lógica de negocio interna.
Si bien la definición es amplia, en el contexto del curso hablamos de API's Web: API remotas accedidas mediante el protocolo HTTP.

Los cuatro principios de REST son:
- **Identificación de los recursos en las solicitudes**: se identifican los recursos en las solicitudes y se separan de las representaciones que se envían al cliente (URIs).
- **Administración de los recursos en las solicitudes**: Los clientes reciben archivos que representan los recursos. Estas representaciones deben tener la información suficiente como para poder ser modificadas o eliminadas.
- **Mensajes autodescriptivos**: Cada mensaje que se envía al cliente contiene una descripción clara sobre la manera en la que debe procesar la información.
- **Hipermedios como el motor del estado de la aplicación** (Hypermedia As The Engine of Application State, HATEOAS): es necesario que después de que el cliente REST acceda a un recurso, pueda descubrir todas las otras acciones que están disponibles actualmente mediante hipervínculos.

Una sola API puede exponer muchas funciones. El backend puede, por ejemplo, exponer funciones como: AddFriend, ListFriends, or GetTimeLine.

Esto ofrece una buena manera de gestionar el rendimiento, escalamiento y su evolución.

Dos tipos de API:
- API públicas:
	- Propuestas por otros como servicio o producto.
- API privadas.
	- La API timeline solo la consumen las aplicaciones creadas por la empresa de la Red Social.

Aunque una API Web permiten su uso en variados sistemas, este no es su principal objetivo.
Las APIs también pueden ser categorizadas en:
- Locales
- Remotas: Servicios Web (SOAP, REST->RESTful)
## RESTful
No todas las APIs Web son RESTful (REpresentatinal State Transfer).
En REST, las acciones son implementadas con verbos (operaciones) HTTP.
- GET/ get_profesor \[mal] -> GET /Profesor \[bien]}
- Solicitamos cosas, no acciones.

| Task                          | Operation | URI                                                 |
| ----------------------------- | --------- | --------------------------------------------------- |
| Insert new item into the cart | POST      | http://api.shopping.com/cart/InsertionNewItem       |
| Delete item from the cart     | POST      | http://api.shopping.com/cart/cartName/item/itemName |
## Formato para representación
Al enviar información a través de una API existirán dos posibles representaciones para esta información, las cuales serían:
- JSON (JavaScript Object Notation)
- XML (e**X**tensible **M**arkup **L**anguage)
### Mapeo códigos de respuesta

| Verbo HTTP | Código de respuesta          |
| ---------- | ---------------------------- |
| GET        | 200, 400, 404, 401, 403      |
| POST       | 200, 201, 202, 400, 401, 403 |
| PUT        | 200, 400, 401, 403           |
| DELETE     | 200, 202, 204, 401, 404      |

| Código de respuesta | Condición o significado                                       |
| ------------------- | ------------------------------------------------------------- |
| 200                 | Solicitud exitosa                                             |
| 201                 | Recurso creado exitosamente                                   |
| 202                 | Solicitud exitosa, pero aún no completada                     |
| 204                 | Recurso eliminado exitosamente                                |
| 400                 | Parámetros entregados pero filtrado no válidos                |
| 401                 | No se entregaron credenciales para autenticación (rechazo)    |
| 403                 | Usuario no autorizado o el servidor ha rechazado la solicitud |
| 404                 | Recurso no encontrado                                         |

2XX: Exito
3XX: Redirección
4XX: No encontrado
5XX: Error
### HTTP  Request
Aspectos importantes
- Headers: Usados con objetivo informativo (e.g., indicar al servidor que el formato (lenguaje) esperado es Text/html o application/json)
- Method: Indica el verbo HTTP asociado a la solicitud.
- Content-Length: En una solicitud POST o PUT puede enviarse este parámetro para que el servidor chequee si hubo truncamiento o no.
- Content-Type: Indica al servidor el formato del contenido (cuerpo)(ej: application/json)
- Body: En el caso de las solicitudes GET, el cuerpo puede ir vacío.
### URI
Una URI (**U**niform **R**esource **I**dentifier) identifica un recurso en forma opaca (p. ej. como el RUT identifica a c/u de nosotros). (opaca: no podemos deducir nada de su lectura.)

Una URI consiste de:
- scheme (esquema): proporciona información sobre el protocolo utilizado (e.g, http, https...).
- authority (autoridad): identifica el dominio.
- port number (e.g. 80, 8080...)
- path(ruta): muestra la ruta exacta al recurso.
- query (consulta): representa la acción de consulta.