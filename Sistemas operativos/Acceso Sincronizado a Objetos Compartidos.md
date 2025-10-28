## Conceptos básicos
Consideremos un proceso con dos hebras.
![[Pasted image 20251026181049.png]]
¿Cuáles son los posibles valores para x? (*Houston, tenemos un problema...*). La itineración de hebras es no determinista.

Ahora consideremos otro proceso con dos hebras. Inicialmente $x=0$.
![[Pasted image 20251026181211.png]]
¿Cuáles son los posibles valores para x?, (OJO: Es necesario descomponer el código anterior). La idea es analizar las operaciones atómicas que lo componen. Algunos posibles escenarios para el ejemplo anterior:
![[Pasted image 20251026181421.png]]

**Problema**: Acceso concurrente a objetos compartidos.
- Comportamiento del programa indefinido.
- El resultado puede variar en cada ejecución.
- Incoherencia de datos.

**Condición de carrera**: Se produce cuando el comportamiento del programa **depende** de la forma en que se intercalan las operaciones que se deben ejecutar.

Este problema ocurre entre hebras, entre procesos e incluso a nivel del sistema operativo.
![[Pasted image 20251026182739.png]]

Resolver estos problemas de sincronización es pega del desarrollador, esto puede llevar a errores y otros problemas. Los sistemas operativos modernos nos entregan las herramientas para sincronizar.

¡No es parte de las funciones de un sistema resolver estos problemas!

El objetivo de este capítulo es entender el problema y revisar algunas formas y herramientas para resolver clásicos problemas de sincronización.

**Sección crítica**: Código en donde se accede al objeto compartido.

Toda solución a un problema de sincronización debe cumplir con:
- **Exclusión mutua**: Solo 1 instancia entra a la sección crítica por vez.
- **Progreso**: Las solicitudes de acceso deben avanzar.
- **Espera acotada**: Si se solicita entrar a la sección, el tiempo de espera es acotado.

Exclusión mutua es la propiedad de **seguridad**, progreso y espera acotada son la propiedad de **vivacidad**.
## Un problema de Ejemplo
Dos hebras deben comprar ron:
![[Pasted image 20251026183911.png]]

Primera solución:
- Cada hebra deja una nota (flag) en el Bar.
- **Seguridad**: Nunca se puede comprar de más.
- **Vivacidad**: Si se requieren ron, alguien debe comprar.
```cpp title:primeraSolucion
if (ron == 0){
	if (nota == 0){
		nota = 1;
		ron++;
		nota = 0;
	}
}
```
Para esta solución el criterio de seguridad no se cumple como se puede ver a continuación:
![[Pasted image 20251026184421.png]]

Segunda solución:
- Se dejan dos notas. Se crean antes de validar.
- La idea es dejar una nota: "Voy a comprar".
![[Pasted image 20251026184634.png]]
Para este caso la seguridad OK, el problema es que ambas hebras podrían dejar las notas y decidir no comprar, por lo que falla la vivacidad.

Tercera solución:
-  Al menos una hebra se asegura si se ha comprado o no.
![[Pasted image 20251026191624.png]]
- Funciona correctamente.
- La solución cumple con vivacidad y seguridad pero es:
	- Compleja y muy particular.
	- Asimétrica: Códigos para hebras distintos.
	- Ineficiente: Produce espera ociosa.
	- Falla ante un reordenamiento de las instrucciones.
## Herramientas para sincronizar
Cada lenguaje de programación puede proveerlas, la interfaz es limpia y simple, se ocultan detalles de la sincronización. Incluye variables de sincronización que se asocian a objetos específicos. Se acceden a través de métodos específicos.

Estudiaremos:
- Locks y variables de condición -> Hebras de un mismo proceso.
- Semáforos -> Procesos cooperativos.

**Locks (Candados)**
Es un tipo de variable de sincronización. Si una hebra retiene un lock, ninguna más lo toma, permitiendo asegurar la exclusión mutua. Tiene dos métodos:
- `acquire()`
	- Espera hasta que el lock esté FREE.
	- Cambia automáticamente a BUSY.
	- Si hay varias hebras esperando, una tiene éxito.
- `release()`
	- El lock queda en estado FREE.
	- Si hay hebras esperando, una tiene éxito.
Tiene dos estados: BUSY y FREE.
Ejemplo: Para solucionar el problema del ron definimos la variable `Lock lock;`, la idea es proteger la sección crítica:
![[Pasted image 20251026192635.png]]
Esta solución cumple con:
- Exclusión mutua: A lo más una hebra retiene el candado.
- Progreso: Si nadie lo retiene y se solicita, se obtiene.
- Espera acotada: El tiempo de espera queda acotado.
Importante: No existe orden de asignación del lock.

**Variables de condición**
Permiten a las hebras esperar eficientemente que ocurra un cambio en un estado compartido. **Siempre** están asociadas a un candado. Tienen tres métodos:
- `wait(Lock *lock)`
	- Automáticamente libera el candado.
	- Suspende la ejecución de la hebra que lo invoca.
	- La hebra queda en una cola de espera asociada a la variable.
	- Cuando despierta, adquiere el candado antes del retorno del wait.
- `signal()`
	- Despierta solo a una hebra.
- `broadcast()`
	- Despierta a todas las hebras.

Consideraciones adicionales:
Una variable de condición no tiene memoria. Solo tiene una cola asociada. Tantas variables de condición como condiciones existan en el problema. Ojo con los candados!

wait() siempre se ejecuta:
- Reteniendo un candado.
- Desde el interior de un loop.

Una hebra despertada no se ejecuta inmediatamente, solo queda en la cola ready.

**Semáforos**
- Utilizados para sincronizar procesos.
- Corresponden a una variable entera que se accede mediante dos métodos.
- p()/wait(): 
  ```
  wait(S){
	  while (S <= 0)
	  ; // busy wait
	  S--;
  }
  ```
  - v()/signal():
    ```
    signal(S){
	    S++;
    }
    ```
- Sistemas modernos usualmente diferencias en dos tipos:
	- **Contadores:** Definidos en un dominio no restringido (usualmente para las condiciones)
	- **Binarios:** Valor 0 a 1. Conocidos como Mutex.
- Mutex generalmente protege la sección crítica.
- El problema de los semáforos es que presentan espera ociosa. Al menos no producen cambios de contexto innecesarios.
- Se conocen como **spinlocks**.
- Para evitar la espera ociosa se puede modificar su definición.
- A cada semáforo se le asigna una cola de espera y se definen dos operaciones:
	- **Block**: Lleva al proceso a una cola de espera.
	- **WakeUp**: Lleva al proceso a la cola de listos.
- La idea es simple, en vez de utilizar el procesador se bloquean para esperar.

Semáforos en C:
Implementados en la librería `semaphore.h`. Permiten sincronización entre procesos y hebras de un mismo proceso. Funciones clave:
- `sem_t sem1;` -> `sem_init(&sem1,0,1)`
	- Segundo parámetro: 0 para hebras, 1 para procesos.
	- Tercer parámetro: Valor de inicio.
- `sem_wait(&sem1)`
- `sem_post(&sem1)`