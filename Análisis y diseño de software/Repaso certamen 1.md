## Modelo de dominio
Este tipo de modelado será de gran ayuda cuando queramos modelar el contexto sobre el que se esta trabajando. En este tipo de diagrama se trabajará con notación UML (aunque sin implementar métodos) y será el encargado de mostrar las interacciones que existirán entre distintos actores entre sí.
### Puntos claves
- El esfuerzo debe centrarse en encontrar conceptos relevantes.
- Las asociaciones y atributos son elementos secundarios.
- Detallar solo la información relevante para el problema (abstracción).
- Describe el "universo" del problema, no clases de **software**.
## Historias de Usuario
Nos ayudarán a capturar el valor que el usuario final espera del producto. La estructura de las historias de usuario puede verse resumida en "Como \<Rol>, quiero \<Objetivo>, para \<Beneficio>". Conecta el rol, su intención y el valor que aporta.
- Rol: Nos obliga a pensar en quien es el que quiere la funcionalidad.
- Objetivo: Nos dice el para que se requiere la funcionalidad.
- Beneficio: Indicará el valor que agrega dicha funcionalidad al producto.
### INVEST
Para realizar una buena HU se debe seguir el criterio INVEST
- **I**ndependiente: Deben ser independientes entre sí.
- **N**egociable: No son un contrato, son una referencia para discutir.
- **V**aliosa: Deben proporcionar valor real al usuario.
- **E**stimable: Debe poder ser estimada con suficiente precisión.
- **S**mall: Su tamaño debe permitir su implementación en una iteración.
- **T**esteable: Deben ser comprobables mediante pruebas.
![[Pasted image 20250929234019.png]]
### Aclaraciones clave
- El criterio INVEST aplica a la historia de forma global.
- Se especifican desde la perspectiva del usuario, no del producto.
- Su objetivo es lograr consenso, no que el negocio domine.
## Diagramas de secuencia
Un diagrama de secuencia nos da una perspectiva dinámica. Ilustra las interacciones mediante mensajes entre objetos a través del tiempo.
## Patrón MVC
El Modelo-Vista-Controlador (MVC) es un patrón de arquitectura de software que se utiliza para separar las responsabilidades de una aplicación en tres elementos fundamentales: el **modelo**, la **vista** y el **controlador**.
### Componentes principales
El patrón MVC se compone de:
1. **Modelo (Model):** Se encarga de la lógica del dominio de la aplicación web. Contiene los métodos para realizar operaciones CRUD (Create, Read, Update, Delete) sobre una fuente de datos, como una base de datos o un repositorio. En una página web, puede existir más de un modelo.
2. **Vista (View):** Representa la interfaz gráfica de usuario (GUI) de la aplicación. Utiliza los datos proporcionados por el modelo para desplegarlos a través de la interfaz, implementada típicamente con HTML y CSS.
3. **Controlador (Controller):** Define el comportamiento de la aplicación web. Es el encargado de gestionar las peticiones HTTP (como GET, POST, PUT, DELETE). Actúa como intermediario entre la Vista y el Modelo, recuperando datos del Modelo para entregárselos a la Vista.
### Propósitos y beneficios
La razón principal para usar MVC es separar las responsabilidades, aislando la interfaz de usuario de la lógica de negocio para evitar que los cambios se vuelvan excesivamente complejos.

Al utilizar MVC, se obtienen las siguientes ventajas:
- Se favorece la mantenibilidad del código.
- Se permite la delegación de responsabilidades en el desarrollo.
- Ayuda a evitar introducir defectos en el software.
- Resuelve el problema recurrente de tener archivos con código mezclado (HTML, CSS, lógica de negocios y SQL), así como la mezcla de responsabilidades.
### Puntos claves
- El Controlador gestiona las peticiones HTTP.
- No todas las páginas necesitan los tres componentes.
- Separa responsabilidades, pero no especifica el cómo implementarlas.
## Patrones y Frameworks
### Patrón de Diseño
Una solución genérica y probada para un problema recurrente en un contexto específico.
### Patrón de Diseño v/s Framework
- **Patrón de Diseño:** Más abstracto. Reutiliza solo diseño. Es una solución conceptual.
- **Framework:** Más concreto. Reutiliza diseño y código. Puede ser una aplicación incompleta.
### Patrones de Persistencia
- Se encargan de la comunicación con la base de datos.
- Resuelven la complejidad de transferir datos.
## Guía para diseñar
### 1. Delimitar el problema
Antes de comenzar a escribir código es muy importante tener claro **que** es lo que se busca. Para este proceso contaremos con diversas herramientas las cuales serán mencionadas a continuación.
#### Diagrama de contexto
Este diagrama se utilizará para definir los límites entre el sistema y su ambiente, mostrando las entidades que interactúan con el.
##### Elementos claves
- Producto: El sistema a definir (círculo del centro).
- Entidades externas: Actores que interactúan (rectángulos).
- Líneas de Flujo: Las interacciones y datos intercambiados (flechas).
- Muy importante tener en cuenta que **LOS ACTORES NO INTERACTÚAN ENTRE ELLOS EN ESTE DIAGRAMA**.
#### Modelo de dominio
Es una representación de las clases conceptuales en el mundo real, no de componentes de software.
### 2. Capturar las necesidades
Una vez que ya entendemos el contexto del sistema surge una nueva pregunta, **¿Qué quieren los usuarios que haga el sistema?**
#### Historias de Usuario
Una HU es una descripción corta y concisa que describe una funcionalidad pero siempre desde la persona que la va a usar.
### 3. Modelar las interacciones
Ahora que ya definimos lo que el usuario quiere que haga el sistema estableceremos como van a colaborar los objetos del sistema para cubrir lo requerido mediante la HU.
#### Diagrama de secuencia
Para este propósito el diagrama de secuencia será de mucha ayuda, dado que este nos servirá para modelar las interacciones entre objetos de un sistema. En otras palabras, modelaremos que mensajes le envía que objeto a otro y en que orden.
### 4. Establecer cimientos sólidos
Centrándonos en la parte más técnica la orientación a objetos será de gran ayuda, pero para poder implementarla primero debemos tener claro ciertas diferencias.
#### Clase v/s Objeto
Mientras que una **clase** es un plano o plantilla la cual define atributos y métodos, un **Objeto** será una instancia creada a partir de dicho plano, es decir, será una entidad concreta.
#### Framework
Un framework puede verse como una aplicación a medio hacer, dado que es una abstracción con código genérico que puede ser especializado.
##### Ventajas y desventajas de un framework
**Ventajas**
- Acelera el desarrollo.
- Código más limpio.
- Soporte de la comunidad.
**Desventajas**
- Curva de aprendizaje.
- Poca flexibilidad.
- Dependencia externa.
### 5. Implementar patrones de diseño
Un patron de diseño describe un problema recurrente y entrega una propuesta de solución genérica y reutilizable.
#### Patrón: MVC
Su idea central es la separación de responsabilidades. Dichas responsabilidades serán abordadas por:
- Modelo: Manejara los datos y la lógica de negocio.
- Vista: Mostrará los datos al usuario.
- Controlador: Tomará el rol de coordinador entre Modelo y Vista.
![[Pasted image 20250930002504.png]]
