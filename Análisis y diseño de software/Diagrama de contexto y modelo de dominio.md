### Diagrama de contexto
Es un diagrama que define los límites entre el sistema, o parte del sistema, y su ambiente, mostrando las entidades que interactúan con él.

Un diagrama de contexto comprende tres características claves.
- **Producto**: El proyecto, sistema o entidad a definir, se simboliza con un círculo que contiene en su interior todo lo que está bajo su control.
- **Entidades externas o agentes**: Las personas, los sistemas y las organizaciones que funcionan fuera pero que interactúan de alguna manera con el producto.
- **Líneas de flujo**: Se representan mediante flechas y simbolizan los datos que fluyen entre los agentes o las formas específicas en que las entidades externas interactúan con el producto.
##### Ejemplo
![[Pasted image 20250812112241.png]]
### Modelo de dominio
##### Motivación
- La escritura de las **historias de usuario** es sencilla cuando nos enfrentamos a **dominios de trabajo conocidos**.
- Incluso cuando estamos ante dominios conocidos, la existencia de una **cultura organizacional** distinta en cada dominio fomenta la existencia de **distintos conceptos** para (muchas veces) similares significados.

La esencia del análisis orientado a objetos es la descomposición del problema en conceptos individuales.
###
Un **modelo de dominio** contiene principalmente los **conceptos** y sus **relaciones** que sean significativos en el **dominio del problema**.
- Está enfocado en conceptos del dominio y **no en entidades de software**.
- Se centra en las abstracciones relevantes, vocabulario del dominio e información del dominio.
- **Objetivo:** Visualizar y comprender la relación de los conceptos que se manejan en el dominio del problema.

Un modelo de dominio es una representación de las clases conceptuales del mundo real, no de componentes de software. No se trata de un conjunto de diagramas que describen clases de software, u objetos de software con responsabilidades.
- UML ofrece notación de diagrama de clases para modelos de dominios.
- A diferencia de los modelos de clases de software, los modelos de dominio no incluyen operaciones (métodos).
  ![[Pasted image 20250812115214.png]]
##### Guía para hacer un modelo de dominio
- Listar las clases conceptuales candidatas relacionadas con los requisitos actuales en estudio.
 