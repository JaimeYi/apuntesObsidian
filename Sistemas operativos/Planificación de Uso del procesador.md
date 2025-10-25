## Definiciones
El estudio de este capítulo comienza con el uso del procesador, luego escalamos a más. Cuando hay muchos procesos por ejecutar, ¿A cuál le asignamos el procesador?, toda política de asignación del procesador presenta un complejo conjunto de decisiones. 

Se dice que el criterio de asignación define la naturaleza de un sistema operativo. La idea es simple: Si la ejecución de un proceso se interrumpe, sin importar la razón, otro debe tomar su lugar y utilizar el procesador.

El itinerador de corto plazo debe elegir un proceso desde la cola listos y asignarle el procesador. Las decisiones de asignación se producen en los siguientes cambios de estado de un proceso:
- Desde "en ejecución" a "espera".
- Desde "en ejecución" a "listo".
- Desde "espera" a "listo".
- Fin de un proceso.

Las decisiones de asignación pueden ser apropiativas o cooperativas. Windows, Linux y MacOS toman decisiones apropiativas para asignar el procesador.

El despachador entrega el control del procesador al proceso seleccionado por el itinerador de corto plazo. Esta asignación produce:
- Cambio de contexto.
- Cambio a modo usuario.
- Saltar a la dirección correcta dentro del proceso y reanudar su ejecución.

El despachador debe ser lo más rápido posible. El tiempo utilizado en detener un proceso e iniciar la ejecución de otro se conoce como latencia del despachador.

Los criterios claves que se deb considerar:
- **Uso del procesador**: Mantenerlo siempre ocupado.
- **Tasa de procesamiento**: Tareas realizadas por unidad de tiempo.
- **Tiempo de ejecución**: Desde que se ordena la ejecución hasta que termina.
- **Tiempo de espera**: Sumatoria del tiempo global que el proceso debe esperar.
- **Tiempo de respuesta**: Desde que se ordena su ejecución hasta que se le asigna por primera vez el uso del procesador.

Objetivo principal:
- **Maximizar el uso del procesador.**
- **Maximizar la tasa de procesamiento.**
- **Minimizar los tiempos de ejecución, espera y respuesta.**

Recordemos la fórmula vista en el capítulo 1: $$T_{EJ}=T_{CPU}+T_{ECR*}+T_{RESP}+T_{E/S}+T_{HW}$$
## Algoritmos de planificación
**FCFS - First Come, First Service**
Es el algoritmo más sencillo de implementar. Su funcionamiento consiste en que el procesador se asigna al primer proceso en solicitarlo. Se gestiona a través de una cola FIFO (First In, First Out). El tiempo promedio de espera suele ser alto. Esto se debe a que no busca optimizarlo.

**FCFS - First Come, First Service - Ejemplo**
- Consideremos la siguiente carga de trabajo:      ![[Pasted image 20251025002408.png]]
- Gantt de asignación:![[Pasted image 20251025002828.png]]
- Tiempo de espera: $P1 = 0$, $P2 = 24$, $P3 = 27$. ¿Qué pasa con el tiempo de respuesta?
- Tiempo de ejecución promedio $=27$
- Tiempo de espera promedio $= 17$.
- $T_{ECR} = T_{RESP}+T_{ECR*}$
**FCFS - First Come, First Service - Ejemplo 2**
- Consideremos que el orden de llegada es $P2$, $P3$, y $P1$:![[Pasted image 20251025012107.png]]
- Gantt de asignación:![[Pasted image 20251025012140.png]]
- Tiempo de espera: $P1=6$, $P2=0$ y $P3 = 3$. ¿Qué pasa con el tiempo de respuesta?
- Tiempo de espera promedio $=3$.
- FCFS sufre el efecto convoy.

**SJF - Short Job First**
Es un algoritmo de tipo prioridad. Su funcionamiento se basa en asignar mayor prioridad al proceso de menor tiempo de uso de procesador. Si existe empate se resuelve por FCFS.

SJF es un algoritmo óptimo, ya que entrega el mínimo tiempo de espera. La dificultad de este algoritmo está en calcular los tiempos de uso del procesador de cada proceso.
**SJF - Short Job First - Ejemplo**
- Consideremos la siguiente carga de trabajo:     ![[Pasted image 20251025012733.png]]
- Si todos llegan al mismo tiempo, Gantt:![[Pasted image 20251025012818.png]]

Sufre de inanición. Las tareas cortas se ven favorecidas, aunque la ráfaga de uso del procesador se debe estimar. Lo cuál es costoso. Puede ser:
- Cooperativo: Permite que las tareas terminen.
- Apropiativo: Interrumpe la ejecución del proceso.
**SJF - Short Job First - Otro ejemplo**
Consideremos la siguiente carga de trabajo:![[Pasted image 20251025013041.png]]
Determine los tiempos de ejecución, espera, y respuesta promedio para el algoritmo apropiativo y luego para el cooperativo. ¿Existen diferencias? Ojo con el tiempo de llegada.
## Multiprocesamiento
- Computadores modernos cuentan con más de un procesador para asignar procesos. La planificación de la asignación se vuelve una tarea más compleja.
- Desafíos:
	- ¿Cómo utilizar múltiples procesadores?
	- ¿Cómo utilizar los algoritmos de planificación de asignación?

- Algunos tipos de arquitecturas:
	- Varios procesadores.
	- Un procesador con varios núcleos.
	- Núcleos para multi hebras.

Algunos posibles escenarios:
![[Pasted image 20251014173945.png]]

- Tendencias tecnológicas han incorporado múltiples núcleos por procesador. Esto permite ser más rápidos y consumir menos energía.
- Múltiples hebras por núcleo: Conocido como *Hyperthreading* en procesadores Intel.
- Un procesador *quad-core* con dos hardware threads por núcleo permite ver 8  procesadores lógicos.
![[Pasted image 20251014174332.png]]

- En este escenario tenemos dos niveles de planificación:
1. El sistema decidiendo a qué hebra asigna un procesador lógico.
2. Luego se decide qué hardware thread se asigna para correr en el núcleo.
![[Pasted image 20251014174502.png]]

Aspectos adicionales:
- El sistema operativo debe estar preocupado de mantener todos los procesadores ocupados.
- Carga balanceada:
	- **Push**: Constantemente buscar procesadores sobrecargados y migrar a otros desocupados.
	- **Pull**: Los procesadores libres notifican para que les asignen tareas.
- Si una hebra se ejecuta, sus datos quedan en la caché.
- **Afinidad**: Que las hebras vuelvan al mismo procesador.
	- **Suave**: El sistema se preocupa de lograrlo, pero no lo garantiza.
	- **Dura**: Los procesos se ejecutan en ciertos procesadores.
- La afinidad mejora el desempeño, pero hay que tener cuidado con no afectar la carga balanceada.2