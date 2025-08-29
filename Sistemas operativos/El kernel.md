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
Los servicios clásicos y necesarios de un sistema:
![[Pasted image 20250828173452.png]]
Los sistemas, además, incorporan programas de sistema, los cuales permiten, entre otras cosas:
- Manipulación de archivos.
- Obtención de información del sistema.
- Soporte a diferentes lenguajes de programación.
- Carga y ejecución de programas.
- Ejecución de servicios en *background*.
Además, los sistemas operativos modernos se pueden estructurar según:
**Monolíticos**
- Todos los grupos de servicios son parte del núcleo (*kernel*).
**Micro**
- Grupo esenciales son parte del núcleo. El resto en modo usuario.
**Híbrido**
- Mezcla de lo mejor de ambas estructuras anteriores.
##### Monolíticos
- La portabilidad exclusivamente de HAL y Gestión de Drivers.
- Las interfaces de comunicación entre distintos componentes del sistema son complejas.
- Lo anterior genera que sea propenso a error. Un error es fatal.
- Si falla un servicio, afecta a todo el núcleo. Es necesario reiniciar el sistema para resolver.
- Ejemplo:![[Pasted image 20250828174550.png]]
###### Monolíticos - HAL
- Capa de abstracción de hardware.
- Contiene configuraciones y operaciones específicas de diferentes arquitecturas del procesador.
- Una capa bien definida permite al sistema ser independiente del procesador.
- Portar un sistema significa modificar rutinas de bajo nivel en HAL.
- La idea es simple, no importa el hardware, el sistema se debe instalar.
###### Monolíticos - Gestión de Drivers
- Es necesario instalar una gran cantidad de controladores de E/S.
- Un 70% del núcleo de Unix es para gestionar E/S.
- Lo ideal es que un sistema sea capaz de cargar dinámicamente los drivers.
- Si el sistema no encuentra el controlador debería conectarse a internet, buscarlo e instalarlo.
##### Micro
- La mayoría de los servicios se mueven a espacio usuario. No requieren privilegios.
- Se debe implementar un mecanismo de comunicación entre los servicios.
- Mach es un buen ejemplo. Mac OS X Kernel está basado en Mach.
- Existe un problema de sobre trabajo para realizar la comunicación.
- Beneficios: Fácil de extender, portable y más seguro.
- ![[Pasted image 20250828180045.png]]
##### Híbridos
- Linux y Solaris se estructuran monolíticos junto a carga dinámica de módulos.
- Windows en su mayoría monolítico, pero con micro kernel para personalización del sistema.
- Mac OS X, por capas, Aqua UI junto al ambiente de desarrollo Cocoa.
	- Basado en Mach micro.
	- Componentes de BSD Unix.
	- Gestión de E/S y carga dinámica de módulos.
- ![[Pasted image 20250828180709.png]]
##### Implementación
- La forma de estructurar los servicios persigue dos objetivos:
	- Usuario: Seguridad, confiabilidad, desempeño y usabilidad.
	- Sistema: Simple, flexible, portable y libre de errores.
- Es importante separar los mecanismos de las políticas, ya que estas cambian durante el tiempo.
	- Política: ¿Qué se debe hacer? Ejemplo -> Interrumpir el procesador cada 10s.
	- Mecanismo: ¿Cómo se debe hacer? Ejemplo -> Utilizando el timer.
### Virtualización
La idea es poder ejecutar más de un sistema operativo de forma concurrente.
- Componentes:
	- Host: SO nativo.
	- VMM: Gestionador.
	- Guest: SO instalado en la VMM.
¿Cómo lograrlo? Se debe simular:
- Inicio del sistema.
- Gestión de interrupciones.
- Modo dual de ejecución.
- Llamadas al sistema.
- Gestión del procesador y memoria principal.
- Gestión de E/S.
##### Inicio del sistema
- El host carga el bootloader de la visita desde el disco virtual.
- El bootloader carga el kernel de la visita y comienza la ejecución.
- La visita inicia su vector de interrupciones.
- La visita carga un proceso desde el disco virtual a la memoria virtual.
##### Para el modo dual:
- CPU virtual para representar el estado de las visitas.
- El núcleo de la visita no debe ejecutarse en modo privilegiado del host.
- Se implementan dos modos virtuales (Usuario y Núcleo).
- Ambos modos se ejecutan en modo usuario del host.
##### Para gestionar interrupciones
- La máquina virtual gestiona, resuelve y retorna los resultados.
- Las instrucciones privilegiadas suelen ser más lentas.
- Más aún cuando se virtualiza más de un sistema sobre un computador.
##### Beneficios
- Múltiples sistemas corriendo sobre el mismo hardware.
- Ejecución de programas de forma concurrente en distintas plataformas.
- Ahorro en recursos de hardware.
- Gestión de estados: Congelar, suspender, ejecutar y clonar.
- Templates: SO + Aplicaciones.
- Migración en línea.