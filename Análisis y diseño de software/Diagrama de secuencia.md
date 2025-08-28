### Definiciones
El diagrama de secuencia es un tipo de diagrama usado para modelar interacciones entre objetos de un sistema. Se modela para cada historia de usuario (caso de uso). A menudo, es útil para complementar un diagrama de clases.

Considera el comportamiento de las *entidades* del sistema como *cajas negras*, nos interesa *lo que hacen y no el cómo lo hacen* internamente.

El diagrama de secuencia está construido a partir de dos dimensiones:
- Horizontal: Representa los objetos que participan en la secuencia.
- Vertical: Representa la línea de tiempo sobre la que los elementos actúan.
Además, estos estarán compuestos por:
- Actores (Siempre estarán los usuarios)
	- Objetos.
- Eventos
	- Mensajes con parámetros.
	- Respuestas.
#### Utilidad
Los diagramas de secuencia ilustran, para un escenario en particular de una historia de usuario, los eventos del sistema.

Los diagramas de secuencia son generados después de analizar e inspeccionar las historias de usuario.

Corresponden a una perspectiva dinámica de análisis y descripción de sistemas.
### Notación
![[Pasted image 20250827164120.png]]
#### Estereotipos
![[Pasted image 20250827164153.png]]
#### Mensajes
Una flecha desde el Llamador de Mensajes hasta el Receptor de Mensajes especifica un mensaje en un diagrama de secuencia. Un mensaje puede fluir en cualquier dirección. (Formato sugerido: nombre_de_mensaje(argumentos): tipo_retorno)
- **Mensaje síncrono:** La entidad que envía el mensaje espera mientras la entidad que recibe el mensaje termine el procesamiento y envíe su respuesta al emisor.
- **Mensaje de retorno:** Se utiliza para indicar que el receptor del mensaje ha terminado de procesar el mensaje y está devolviendo el control a la persona que llama el mensaje.
- **Mensaje asíncrono:** La entidad que envía el mensaje, continua su ejecución sin esperar respuesta.
- **Mensaje encontrado:** Este tipo  de mensaje no muestra quién lo envía, esto podría significar que no se conoce el remitente o no es importante para el entendimiento de la interacción que se está describiendo.
- **Mensaje auto enviado:** El origen y destinatario del mensaje es la misma entidad. Puede representar una llamada recursiva o la llamada a otro método perteneciente al mismo objeto.
- **Mensaje condicional:** El mensaje sólo se envía si se cumple la condición indicada.
##### Ejemplo
![[Pasted image 20250827164850.png]]
#### Bloques
- **Alternativa (alt):** elección (mediante una guarda) de una interacción. Múltiples fragmentos, sólo se ejecuta el que cumpla la guarda.
- **Opción (opt):** Equivale a un operador alt con un solo fragmento. Se ejecuta si la guarda se cumple.
- **Bucle (loop):** El fragmento se ejecuta múltiples veces. La guarda indica cómo realizar la iteración.
- **Negativa (neg):** Define una interacción inválida.
- **Paralelo (par):** Cada fragmento se ejecuta en paralelo.
- **Región crítica (critical):** Sólo puede haber un proceso ejecutando simultáneamente el fragmento.
- **Diagrama de secuencia (sd):** rodea un diagrama de secuencia.
- **Referencia (ref):** El marco hace referencia a una interacción definida en otro diagrama. El marco dibujado cubre las líneas involucradas en la interacción. Puede incluir parámetros y un valor de retorno.
##### Ejemplo
![[Pasted image 20250827165310.png]]