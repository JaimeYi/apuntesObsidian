#### ¿Qué es un sistema operativo?
Un sistema operativo es el conjunto entre programas y kernel, donde se gestionan los recursos del computador para poder ejecutar dichos programas. Es importante tener en cuenta que el sistema operativo también es un programa, por lo que este también consumirá recursos (ram, uso del procesador, etc.)
![[Pasted image 20250812172920.png]]
Los programas al ejecutarse generan un proceso, los cuales se almacenan en memoria RAM. Con lo recién mencionado se puede inferir que no en todos los casos un aumento de memoria RAM implica un mejor rendimiento.

Su diseño y construcción conlleva varios desafíos. Éste debe ser:
- **Portable**.
- **Eficiente**.
##### Confiable
- ¿El sistema **hace** lo que debe hacer?
- ¿Hace lo que debe **sin** errores?
- ¿Está **siempre** disponible?
##### Seguro
- ¿El sistema puede verse comprometido?
- Protección interna y externa.
- ¿Usarías un sistema inseguro?
##### Portable
- Programas: No importa el SO ni el hardware. ¡Me debo ejecutar!
- SO: No importa el hardware. ¡Me debo instalar y funcionar!
##### Eficiente
- ¿Cómo medimos la eficiencia? Debemos definirlo.
	- ¿Cuánto demora un programa en ejecutarse?
	- ¿Cuántos programas puedo ejecutar?
	- ¿Se mantiene en el tiempo el desempeño?
#### Objetivo principal
El sistema operativo provee un **entorno de ejecución** de programas de usuario utilizando de forma **conveniente** y asignando de forma **justa** el hardware del computador.

Se deben prevenir errores y gestionar las operaciones E/S (entrada/salida).
#### Entorno de ejecución
El entorno de ejecución estará basado:
- **Respecto al hardware**:
  - Asignación equitativa.
  - Ilusión en la asignación (compartir).
- **Protección**
  - Aislar la ejecución de programas entre sí.
  - Aislar a diferentes usuarios.
#### Ejecución secuencial
- Para que un programa se ejecute el SO debe asignarle el procesador.
- Para poder competir por el procesador debe estar en memoria principal.
- El camino que recorre se basa en la pirámide de jerarquía de hardware de un computador.
- La  ejecución de un programa usualmente se divide en: uso de procesador y tareas de E/S.
- Cuando se realizan tareas de E/S el procesador queda libre.
#### Multiprogramación
- Intercala la asignación del procesador entre distintos programas.
- La intercalación se produce solo cuando los programas realizan tareas de E/S.
- Para lograrlo, debe existir un grupo de programas disponibles.
- La idea es que siempre haya uno para ejecutar.
- Esto genera un aumento en el uso del procesador. 

| CPU  | P0  | P1  | P2  | P0  | P0  |     | P0  | P1  | P2  | P2  |
| ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| E/S0 |     | P0  | P0  |     |     | P0  |     |     |     |     |
| E/S1 |     |     | P1  | P1  | P1  | P1  | P1  |     |     |     |
| E/S2 |     |     |     | P2  | P2  | P2  | P2  |     |     |     |

#### Tiempo compartido
- Intercala la asignación de uno o más procesadores entre distintos programas.
- La intercalación se produce por distintos eventos de interrupción.
- La intercalación debe ser lo más rápida posible.  
#### Definiciones
- **Concurrencia**: Ilusión que genera el SO al ejecutar dos o  más programas al "mismo tiempo" con un solo procesador.
- **Paralelismo**: Ejecución de dos o más programas al mismo tiempo en dos o más procesadores.
### Rendimiento
- Uno de los objetivos principales de la evolución de los SO's fue optimizar el tiempo de usuario.
- El rendimiento de un sistema computacional es inversamente proporcional al tiempo de ejecución de uno o varios programas.
- **Tiempo de ejecución**: Tiempo que transcurre entre que se ordena la ejecución de un programa hasta que finaliza. Existen dos grandes factores:
	- Sistema Operativo.
	- Hardware.
- Si bien existen varios tiempos asociados, por el momento consideramos la siguiente forma de calcularlo.
$$T_{EJ} = T_{CPU}+T_{RESP}+T_{ECR*}+T_{E/S}+T_{HW}$$
	- $T_{CPU}$ : Tiempo utilizado en ejecutar operaciones en el procesador.
	- $T_{RESP}$ : Tiempo que transcurre desde que se ordena la ejecución de un programa hasta que se le asigna por primera vez el procesador.
	- $T_{ECR*}$ : Tiempo espera en la cola ready sin contar el tiempo de respuesta.
	- $T_{E/S}$ : Tiempo utilizado en ejecutar operaciones E/S.
	- $T_{HW}$ : Tiempo asociado a lectura y escritura en los distintos componentes de hardware.
- El CPI es un buen indicador que refleja la organización del procesador y la arquitectura del conjunto de instruccciones.
- Se define como el número promedio de ciclos por instrucción para un programa.
- No olvidar que cada arquitectura puede tener varios tipos de instrucciones. Ejemplo:
	- Aritméticas y lógicas.
	- Acceso a memoria principal.
	- Direccionamiento.
### Tópicos modernos
Los sistemas operativos actuales
- Foco en el usuario: Facilidad de uso y rendimiento.
- Gestión de distintos tipos de dispositivos.
- Gestión de servidores y data center de gran escala.
- Servicios Cloud y Virtualización:
	- IaaS
	- PaaS
	- SaaS
- Redes de computadores.
- Sistemas distribuidos.
- Gestión de capacidad de hardware y funcionalidades extras. Ejemplo Procesador Intel.
	- Turbo boost.
	- Hyper Threading.
	- Memoria caché.
##### Tendencias
- Inteligencia artificial y aprendizaje automático.
- Computación cuántica.
- IoT y Edge Computing.
- Entre otras cosas interesantes.