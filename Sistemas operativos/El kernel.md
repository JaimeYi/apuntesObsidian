### Inicio, interrupciones y privilegios
- El inicio del sistema comienza con la ejecución de la BIOS.
- Ésta se encuentra en una memoria no volátil de la placa madre.
- Luego de validar el hardware, carga el boot loader, el cual busca y carga el SO en memoria.
- El sistema operativo queda operativo esperando que suceda algo.
- Ejemplo: El más común, GRUB, permite seleccionar y ejecutar distintos SO's.
- La ocurrencia de un evento se indica a través de una interrupción.
- Estos eventos cambian el flujo normal de la ejecución de un programa.
- Cuando se producen, el procesador deja de hacer lo que está haciendo.
- El SO revisa que pasó, lo resuelve y reanuda la ejecución del programa.
- Pueden ser producidas por software o hardware.
**Los sistemas operativos modernos son conducidos por interrupciones (OS interrupt driven)**
##### Interrupciones por software
- También son denominadas *traps*, son síncronas respecto a la ejecución de instrucciones.
- Se producen por ejecutar una instrucción de un programa.
- Ejemplo:
	- División por cero.
	- Overflow aritmético.
	- Referencia de memoria inválida.
##### Interrupciones por hardware
- Son asíncronas respecto a la ejecución de instrucciones.
- Ejemplo:
	- Oprimir teclas.
	- Término de la transferencia de datos.
	- Timer: Dispositivo de hardware que constantemente interrumpe al procesador. La frecuencia con que lo hace es definida dentro del sistema operativo.![[Pasted image 20250819182036.png]]
- El código que resuelve un evento se denomina *interrupt handler*.
- Mientras se ejecuta:
	- Se deshabilitan temporalmente las interrupciones.
	- No se puede bloquear. Se ejecuta hasta finalizar.
- Enmascaramiento de interrupciones: El sistema operativo es capaz de deshabilitar las interrupciones ante otros eventos.
- Es necesario implementar la solución a todas las interrupciones.
- Se agruparán en el vector de interrupciones.
- Éste agrupa las direcciones de todos los interrupt handler.
- Usualmente se encuentra en la región de memoria asignada al sistema.
  ![[Pasted image 20250821175437.png]]
- Es necesario poder guardar el estado de un programa en ejecución, pero no solo los datos internos, sino que también el contexto.
- Al ejecutar un programa se guarda la información en los registros de apoyo del procesador. Un ejemplo de esto podría ser la dirección de la siguiente instrucción a ejecutar.
- El sistema utiliza una región denominada stack para guardar estos datos en la memoria principal.
##### Flujo normal ante un evento de interrupción
El flujo normal será el siguiente:
- Guardar los datos que están en los registros de apoyo en el stack.
- Direccionar al vector de interrupciones.
- Ejecutar el interrupt handler correspondiente.
- Restaurar los datos a los registros de apoyo del procesador.
- Reanudar la ejecución del programa.
![[Pasted image 20250821182319.png]]
##### Instrucciones en un SO
- Las instrucciones que son del sistema operativo requieren permisos. La idea de esto es proteger al sistema de mal intencionados.
- Se incorporan privilegios a la ejecución de instrucciones.
- Dos modos: Usuario y SO (kernel).
- Requiere soporte de hardware: Bit de modo (0 para kernel).
![[Pasted image 20250821182854.png]]
### Llamada al sistema
Son una interfaz de programación que permite acceder a los servicios de un sistema. Usualmente son escritas en C o C++. Para acceder a ellas a través de una API.
- Tienen un ID único para ser identificadas. Su implementación varía en cada sistema.
- Quien invoca el servicio no necesita saber como está implementado.

Los sistemas pueden incorporar un gestionador específico. Las funciones más comunes:
- Localizar argumentos y copiarlos a una región accesible por el sistema.
- Validar los valores para evitar errores o uso mal intencionado.
- Copiar los resultados en una región de memoria para el usuario.

El paso de parámetros puede ser implementado de 3 formas:
- Utilizando registros de apoyo.
- En memoria y entregando la dirección en un registro de apoyo.
- En una región de memoria compartida. El programa guarda y el sistema lee.
![[Pasted image 20250821184008.png]]
Se pueden clasificar según el servicio del sistema que invocan, por ejemplo:
- Gestión de procesos.
- Gestión de archivos.
- Gestión de E/S.
- Contabilidad.
- Comunicación.
![[Pasted image 20250821184126.png]]
### Servicios estructurados
### Virtualización