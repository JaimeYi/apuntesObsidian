## Definiciones
## Algoritmos de planificación
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