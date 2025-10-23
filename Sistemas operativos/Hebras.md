## Definición
Los sistemas modernos permiten que un proceso tenga más de una hebra en ejecución. Esto afecta directamente el diseño de los sistemas, lo que ha provocado que la mayoría de los programas modernos estén construidos con hebras.

La idea es simple, intentar paralelizar las tareas que debe ejecutar un programa:
- Diferentes funcionalidades.
- Resolver recurrencias.
- Cálculos más rápidos.

Una hebra es una secuencia simple de ejecución que representa una tarea itinerante separada. Las Hebras están compuestas por un ID, contadores, registros y un stack.

Una Hebra comparte con otras hebras, que son parte del mismo proceso, código, datos y recursos. La creación de hebras es más eficiente que la de procesos. Más simple y menos recursos. La utilización de hebras en el código de un programa puede volverlo más sencillo.
![[Pasted image 20251022230901.png]]
Beneficios:
**Capacidad de respuesta:**
La ejecución de un programa puede continuar a pesar de que una parte de él esté bloqueada.
**Recursos compartidos:**
Ventajas sobre los IPC, es mucho más simple y se requieren menos recursos.
**Economía:** Creación y cambio de contexto son menos costosos.
**Escabilidad:** Explotar arquitectura de múltiples procesadores.
## Programación
El uso de hebras depende exclusivamente del programador. Presenta un mayor desafío por los siguientes puntos:
- **Dividir actividades**: No todas las tareas pueden paralelizarse. El programador debe identificar qué partes del programa pueden ejecutarse de forma independiente y cuáles deben ejecutarse de manera secuencial.
- **Balancear**: Una vez que se dividen las tareas, el programador tiene el trabajo de asegurarse de que el trabajo se reparta de manera equitativa entre las distintas hebras.
- **Separación de datos**: Esto hace referencia a como los datos se organizan en la memoria. Idealmente, cada hebra debería trabajar con su propio "trozo" de datos para no interferir con las demás. El programador debe decidir cómo partir y distribuir los datos entre las hebras.
- **Dependencia de datos**: Este es el problema central de la programación concurrente. Ocurre cuando dos o más hebras necesitan leer y/o escribir en la misma ubicación de memoria al mismo tiempo.
- **Pruebas y debug**: Depurar un programa con múltiples hebras es extremadamente difícil. Los errores son a menudo no deterministas. Esto hace que los errores sean muy difíciles de reproducir, encontrar y solucionar.
La idea es explotar una arquitectura de varios procesadores.![[Pasted image 20251022235217.png]]
Existen dos tipos de paralelismos:
- **Datos**: Se distribuyen las mismas operaciones sobre distintos sets de datos.
- **Operaciones**: Cada hebra ejecuta operaciones distintas.

Necesitaremos herramientas para programar con hebras. Las librerías más comunes:
- POSIX Threads.
- Windows Threads.
- Java Threads.
Nosotros revisaremos la API simple para hebras, basada en POSIX pero simplifica su uso omitiendo opciones y manejo de errores. Requiere `sthread.c` y `sthread.h`
## API Simple para Hebras
Las funciones principales son:

`{c++ icon} void sthread_create(thread, func, arg):`
Crea una nueva hebra almacenando la información en **thread**. Ejecuta la función **func** utilizando el argumento **arg**.

`{c++ icon} void sthread_yield():`
La hebra que invoca esta función libera voluntariamente el procesador. El itinerador de corto plazo es quién decide cuando continua con la hebra que liberó.

`{c++ icon}void sthread_join(thread):`
La hebra que invoque esta función debe esperar el término de la hebra **thread**. El término de la hebra se gatilla por la función sthread_exit().

`{c++ icon}void sthread_exit(ret):`
Termina la hebra que la invoca. Puede retornar el un valor en **ret**. Si una hebra está esperando con un join se despierta.
## Implementación
El sistema entrega la ilusión de que cada hebra usa su propio procesador, esto lo logra suspendiendo y despertando las hebras. Es necesario utilizar estados internos.

Se implementarán igual que los procesos, utilizando una estructura para el contexto. La estructura se denomina TCB y guarda:
- Estado de la computación.
- Metadata de la hebra.
![[Pasted image 20251023005858.png]]

Cada hebra contiene dos elementos de estado que la determinan:
- **Stack**: Información de procedimientos y funciones anidadas de la hebra que está en ejecución. Se almacenan variables temporales, parámetros y direcciones de retorno.
- **Metadata**: El tid, prioridades, uso de recursos, etc.

Las hebras también tienen un diagrama de estados:
![[Pasted image 20251023010100.png]]

El sistema debe contar con sus propias hebras para atender a las hebras de usuario. En su mayoria, el objetivo principal es ejecutar instrucciones privilegiadas.![[Pasted image 20251023010202.png]]

Las hebras de tipo kernel se pueden implementar de 3 formas:
- Muchas hebras de usuario a una hebra de kernel.
- Una hebra de usuario a una hebra de kernel.
- Muchas hebras de usuario a muchas hebras de kernel.

**Muchas hebras de usuario a una hebra de kernel**:
Una hebra puede bloquear el proceso completo. No existe el paralelismo real sobre arquitectura con múltiples procesadores. Pocos sistemas lo utilizan.![[Pasted image 20251023010558.png]]

**Una hebra de usuario a una hebra de kernel:**
Esta opción ofrece un mayor grado de concurrencia. Si una se bloquea, las otras pueden seguir. Esta opción si ofrece un paralelismo en arquitecturas que lo permitan, pero tener en cuenta que esta opción es más costosa. Windows y Linux siguen este modelo.![[Pasted image 20251023010743.png]]

**Muchas hebras a muchas hebras:**
Se define un total de hebras de tipo kernel, cantidad que variará dependiendo del sistema. Su uso no es muy común. Se multiplexan muchas hebras de usuario a kernel.

**Conclusiones generales:**
- Cada proceso tiene una hebra principal y puede dividirse en más.
- Un proceso es mucho más que una hebra. La PCB requiere más información que la TCB.
- Tanto la PCB y la TCB representan a una hebra. La cola ready contiene una mezcla de ambas.
- El cambio de contexto puede ocurrir en:
	- Solo hebras de kernel.
	- Hebras de kernel y hebras de procesos.
	- Hebras de diferentes procesos y de un mismo proceso.

**Aspectos adicionales:**
- ¿Qué pasa con fork()?
	- La semántica cambia en programas multi hebra.
	- Algunos sistemas tienen dos versiones de fork().
	- Si una hebra invoca exec() se cambia todo el programa.

- ¿Es posible cancelar una hebra?
	- Si, se denomina hebra objetivo.
	- La cancelación puede ser asíncrona (termina inmediatamente) o diferida (constantemente se verifica si se debe cancelar o no).