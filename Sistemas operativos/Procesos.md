### Definición
- El objetivo principal de un sistema es proveer un entorno de ejecución de programas.
- Un programa es una entidad pasiva. Está instalado y almacenado en el disco duro.
- Un **proceso** es una abstracción generada por el sistema para ejecutar un programa.
- La ejecución (carga en memoria principal) comienza a través de una GUI, CLI, etc.
- Existen de tipo usuario y de sistema operativo.

Todo proceso está compuesto por:
- **Código (sección de texto):** Instrucciones que son parte del programa y que se deben ejecutar.
- **Datos:** Espacio para variables globales.
- **Stack:** Valores temporales: Variables locales, direcciones de retorno, parámetros, etc.
- **Heap:** Se asigna en tiempo de ejecución. Normalmente para arreglos.
![[Pasted image 20250902173829.png]]

Todo proceso cambia de estado mientras se ejecuta:
- Nuevo.
- En ejecución.
- En espera.
- Listo.
- Finalizado.
![[Pasted image 20250902174108.png]]
La información de cada proceso se almacena en el `Process Control Block`:
- **Estado:** Los diferentes estados.
- **PC:** Dirección de la siguiente instrucción a ejecutar.
- **Registros:** Datos almacenados en los registros de apoyo.
- **Itineración:** Prioridad, punteros a colas, etc.
- **Contabilidad:** Uso de CPU, ciclos, límites de tiempo, etc.
- **E/S:** Recursos asignados, estados de uso, etc.
Esta información es requerida por el sistema para hacer gestión sobre los procesos.
### Itineración
El objetivo es elegir uno de los tantos procesos disponibles y asignarlos al procesador.
- El cambio debe ser lo más rápido posible.
- Se busca maximizar el uso de procesador, evitando tiempos muertos. ¿Por qué?
- Para lograrlo, el sistema dispone de dos tipos de colas para los procesos:
	- **Cola ready:** Acá están todos los procesos listos para usar el procesador.
	- **Colas de espera:** Existen distintas, dependiendo de los eventos de espera. Se tendrán tantas colas como eventos del sistema operativo existan.
- Los procesos, a lo largo de su vida, se van moviendo entre las distintas colas.

La implementación de las distintas colas es la siguiente:
![[Pasted image 20250902175317.png]]

- Cuando a un proceso se le asigna el procesador, se dice que es despachado.
- Mientras se está ejecutando pueden ocurrir distintos eventos:
	- Solicitar E/S y ser asignado a la cola de espera correspondiente.
	- Crear un nuevo proceso y esperar la finalización de éste.
	- Ser desalojado como resultado de una interrupción.
	- Invocar al sistema a través de una llamada al sistema.
Ejemplos de eventos que pueden interrumpir la ejecución de un proceso.
![[Pasted image 20250902180706.png]]

El sistema puede implementar dos tipos de itineradores:
**Largo plazo:**
- Cuando se cargan en memoria principal los procesos por primera vez.
**Corto plazo:**
- Aquel que asigna el procesador constantemente a los procesos que están en la cola listos.
¿Cuál de los dos controla el grado de multiprogramación?

El sistema debe ser cuidadoso con los procesos que lleva a memoria principal:
- Podemos clasificar a los procesos según:
	- **E/S:** Aquellos que ocupan la mayor parte del tiempo realizando operaciones E/S.
	- **CPU:** Aquellos que ocupan la mayor parte del tiempo en el procesador.
- Se debe elegir una combinación de procesos que permitan mantener el equilibrio
- Los casos bordes de asignación pueden reducir el rendimiento del sistema.

El sistema puede implementar dos tipos de itineradores:
**Caso borde 1 - Todos los procesos E/S**
- Procesador ocioso.
- Alta demanda de E/S.
- Cola listos vacía, itinerador de corto plazo con poco trabajo.
**Caso borde 2 - Todos los procesos de CPU**
- E/S con baja demanda. Colas vacías.
- Aumenta el trabajo de asignación del procesador entre muchos procesos.

Cuando el itinerador de corto plazo cambia la asignación el procesador:
**Cambio de contexto**
- Se guarda el contexto del proceso saliente y se carga el del entrante.
- El contexto de un proceso es representado por la PCB.
- El tiempo utilizado en realizar el cambio es desperdiciado.
- El tiempo dependerá exclusivamente del hardware de la máquina.
![[Pasted image 20250902182719.png]]
### Operaciones
Los sistemas deben proveer acciones para trabajar con procesos:
- Al menos debemos poder crearlos y finalizarlos.
- Existen 3 tipos de eventos que gatillan la creación:
	- Arranque del sistema.
	- Petición del usuario.
	- **Proceso en ejecución crea uno o varios**.

- Mientras se ejecuta, un proceso puede crear varios procesos.
- Para lograrlo, debe utilizar llamadas al sistema.
- El proceso que crea es el padre, los procesos creados son los hijos.
- Cada hijo a su vez puede crear otros procesos. Esto generará una jerarquía.
- Será necesario poder identificar de forma inequívoca a cada uno.
- Unix y Windows asignan un pid a cada uno.
![[Pasted image 20250902183423.png]]

Respecto a la creación, se pueden definir algunas opciones en cada sistema:
**Recursos compartidos**
- Define cómo y cuántos recursos se pueden compartir entre padre e hijos.
**Ejecución**
- Define como se ejecutan los procesos. Pueden ejecutarse de forma concurrente o esperar.
**Espacio de direcciones**
- Los hijos pueden ser duplicados del padre o cargar un nuevo programa.

Estudiaremos las llamadas al sistema de Unix:
**fork();**
- Permite crear un proceso.
**exec();**
- Permite cambiar el contenido del espacio de direcciones de un proceso.
- Tiene varias variantes.
**wait();**
- El proceso que lo invoca debe esperar el término de un proceso hijo.
**Ejemplo de fork**![[Pasted image 20250902183936.png]]

### Comunicación