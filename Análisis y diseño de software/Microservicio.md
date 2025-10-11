Un microservicio, como su nombre lo indica, es un servicio pequeño y autónomo que trabaja de manera independiente. Estos microservicios son ideales para modularizar una aplicación.

Es un estilo de arquitectura que permite desarrollar una aplicación basado en varios servicios "pequeños" débilmente acoplados, con un alcance bien definido, los cuales utilizan medios de comunicación livianos (ej: HTTP).

Como ya se mencionó, a diferencia de las aplicaciones clásicas, los microservicios tienen como unidad granular servicios los cuales se comunican por medios de comunicación livianos.
### Ventajas
- Mejora mantenibilidad.
### Desventajas
- Latencia en la red.

Los microservicios que se organizan en torno a las capacidades de negocio, igual que los equipos que son responsable de ellos. Esto permite flexibilidad en la organización de trabajo de los equipos.
### Gateway
Expone un conjunto de microservicios internos a aplicaciones externas de manera controlada y segura.
### Más ventajas y desventajas
#### Ventajas
- Tienen poco código.
- Son simples. Tienen un solo propósito.
- Son desplegables de manera independiente.
- Son escalables de manera independiente.
- Son independientes de las tecnológica entre sí.
#### Desventaja
- Las arquitecturas distribuidas tienen otras consideraciones. (**Teorema CAP**)
- Información del negocio se encuentra distribuida en distintos contextos. Requiere considerar medidas adicionales.
- Pueden resultar difíciles de administrar (pero existen herramientas).
### Que pasa con...?
#### Datos
- **Enfoque tradicional**: Se vuelve complejo manejar datos para todos los contextos.
- **Recomendación**: Modelos orientados al objetivo.
- **¡Pero!*** Replicación de datos (puede ocurrir).
- Se tiene discrepancia de datos en algunos momentos (al realizar cambios locales).
##### SAGA
Es una forma de administrar la consistencia de los datos entre los microservicios en escenarios de transacciones distribuidas.
###### Eventos
- AMQP (Advanced Message Queuing Protocol).