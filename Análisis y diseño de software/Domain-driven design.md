### Principios claves
- Concentrarse en el corazón del dominio.
- Aprender por medio de la colaboración.
- Modelamiento vía exploración y experimentación.
- Comunicación (Lenguaje Ubicuo).
- Entender la aplicabilidad del modelo (contexto).
- Evolución constante.
Es importante entender el contexto sobre el cual se trabajará.
### Pasos claves DDD
1. Capturar el [[Diagrama de contexto y modelo de dominio|MD]] en términos del dominio. (lenguaje ubicuo)
2. Embeber terminología dominio en el código. (cohesión)
3. Proteger el dominio de que sea corrompido por otros dominios.
![[apuntesObsidian/Análisis y diseño de software/Untitled Diagram.svg]]
Dentro de un dominio solo las entidades pueden ser `root`, las cuales serán las encargadas de comunicar el dominio con otros dominios mediante sus `roots`.
### Caso de estudio
Se tiene una aplicación la cual tiene funcionalidades en $n$ capas, procesos del sistema mediante las funcionalidades del sistema y una o más bases de datos las cuales son compartidas para todas las funcionalidades definidas.

Además:
- El sistema/negocios de tamaño acotados.
- Desarrollo rápido y más sencillo.
- Acceso a los datos único
Pero:
- ¿Y si el negocio crece?
- Mantención o cambios en el negocio.
- ¿Y si aumenta su uso en determinados periodos?

