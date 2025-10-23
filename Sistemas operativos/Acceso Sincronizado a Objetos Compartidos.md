## Conceptos básicos
## Un problema de Ejemplo
## Herramientas para sincronizar
### Semáforos
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
- El problema de los semáforos es que presentar espera ociosa. Al menos no producen cambios de contexto innecesarios.
- Se conocen como **spinlocks**.
- Para evitar la espera ociosa se puede modificar su definición.
- A cada semáforo se le asigna una cola de espera y se definen dos operaciones:
	- **Block**: Lleva al proceso a una cola de espera.
	- **WakeUp**: Lleva al proceso a la cola de listos.
- La idea es simple, en vez de utilizar el procesador se bloquean para esperar.