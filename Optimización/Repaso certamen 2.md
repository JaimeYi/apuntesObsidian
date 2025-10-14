### ¿Cómo se toma la mejor decisión posible con límites?
La optimización matemática es una forma estructurada de encontrar el mejor resultado en un mundo de restricciones.
### Decisiones óptimas
#### Los 3 componentes básicos
- **Variables**: Lo que podemos cambiar.
- **Restricciones**: Los límites y reglas que debemos seguir.
- **Función objetivo**: La meta a maximizar o minimizar.
### Mapeando posibilidades
![[Pasted image 20251013011316.png]]
#### Método gráfico
Para encontrar las soluciones de un problema de optimización podemos utilizar el método gráfico, el cual seguirá los siguientes pasos:![[Pasted image 20251013011425.png]]
Lo bueno de este método es que **la mejor solución SIEMPRE se encuentra en los vértices de dicha región**.
##### Ejemplo
Nuestro objetivo es maximizar la función $z = 11x_1+14x_2$. $z$ representa nuestro beneficio total. Además tendremos las siguientes restricciones:
- $1x_1+1x_{2}\leq17$
- $3x_{1}+ 7x_{2}\leq63$
- $3x_{1}+ 5x_{2}\leq48$
- $3x_{1}+ 1x_{2}\leq30$
- $x_{1},x_{2}\geq0$
El **primer paso** será dibujar nuestras restricciones:
![[Pasted image 20251013014829.png]]
El **segundo paso** es fijarse en la región donde se cumplen todas las restricciones (el área pintada).
El **tercer paso** es encontrar el mejor punto para nuestra optimización, esto lo lograremos siguiendo la expresión **"Si existe una solución óptima, tiene que ser una solución factible en un vértice"**. Por lo tanto, evaluamos la función objetivo en cada vértice para obtener el valor máximo (en este caso) que podamos obtener.
![[Pasted image 20251013015706.png]]
Por lo que para $x_{1}=8.5$ y $x_2=4.5$ nuestra función objetivo $z$ se maximiza.
###### Resumen de la resolución
![[Pasted image 20251013015820.png]]

### Método simplex
Si bien el método gráfico nos facilita mucho la tarea de encontrar la mejor solución para un problema de dos variables, ¿Qué pasa si tenemos miles de variables?. Lógicamente realizar un gráfico para miles de variables no es una opción viable, por este motivo es que se buscó un mejor método para encontrar la mejor solución para un problema de optimización, este mejor método es el **método Simplex**. El método simplex se basa en la premisa de que **"Si existe una solución óptima, tiene que ser una solución factible en un vértice"**. El algoritmo del método Simplex puede describirse como:![[Pasted image 20251013011934.png]]
#### ¿Cómo maximizar el beneficio de una tienda con su mezcla?
##### El problema de Appamundi
- **Objetivo:** Maximizar el beneficio de la venta de frutos secos.
- **Productos:** Nueces ($x_1$), Almendras ($x_2$), Pistachos ($x_3$).
- **Beneficios:** 5.00\$/kg Nueces, 6.00\$/kg (Almendras), 5.50\$/kg (Pistachos).
- **Restricciones:**
	- Paquete total $\leq 100$ kg.
	- $x_2\leq2\cdot (x_{1}+x_3)+2$.
	- Pistachos disponibles $\leq 30$ kg.
![[Pasted image 20251013225103.png]]
Como $x_2$ (Almendras)es la variable con mayor coeficiente de mejora (cj-zj) realizamos las operaciones elementales necesarias para que el único elemento de la columna $x_2$ se encuentre en la fila $x_2$.
![[Pasted image 20251013225808.png]]
Como ahora $x_3$ es la variable con mayor coeficiente de mejora repetiremos el proceso realizado anteriormente pero esta vez con $x_3$.![[Pasted image 20251013225945.png]]
Por último, realizamos el mismo proceso con $x_1$.![[Pasted image 20251013230322.png]]
Por lo que con el método simplex fuimos capaces de obtener que el beneficio máximo de la tienda será de 582.33$. Donde $x_1$ debe ser $2.67$, $x_2$ debe ser $67.33$ y $x_3$ debe ser $30$.
##### Consideraciones
- Para saber si un ejercicio de metodo simplex tiene optimos alternativos nos debemos fijar en si las variables no basicas (las variables $s_n$ que se obtienen al estandarizar el problema) son menores a 0 en el cj-zj en su totalidad o no. Si todas las variables no basicas son menores a 0 en la fila cj-zj significa que no existen optimos alternativos.
- Para determinar que el tableau obtenido es el tableau final se debe cumplir que $c_j-z_j\leq0$.
### Análisis de sensibilidad
Si bien podemos obtener una solución que nos maximice nuestra función objetivo nos quedan las interrogantes **¿Es robusta la solución?¿Qué pasa si los precios cambian?**. Para resolver estas interrogantes entra el juego el análisis de sensibilidad.

El análisis de sensibilidad determina los rangos en los que los parámetros de un modelo pueden variar manteniendo la base óptima.![[Pasted image 20251013231023.png]]

### De la teoría al código
Para ejemplificar como se lleva la teoría a lo práctico utilizaremos el **problema de asignación**, el cual se plantea con la pregunta ¿Cómo asignar trabajadores a tareas para minimizar el coste total, si cada trabajador hace una tarea?
#### Modelo matemático
$Min\,z = \sum c_{ij}x_{ij}$ con restricciones de suma igual a 1.
#### Código MiniZinc
`solve minimize sum...` y `constraint forall...` Traducción directa.
### Optimización en el mundo
**¿Dónde está la optimización?**
- Transporte y logística (rutas, horarios).
- Fabricación (mezclas, producción).
- Finanzas (carteras de inversión).
- Asignación de recursos (personal, inventario).
- Planificación industrial.
Estos problemas resuelven problemas con cientos o miles de variables para encontrar el mejor resultado.
### Análisis de sensibilidad
El análisis de sensibilidad es una herramienta fundamental utilizada en la optimización, especialmente en la programación lineal, cuyo objetivo principal es determinar los rangos dentro de los cuales pueden variar los parámetros de un modelo manteniendo la base óptima y la solución posible.
### Branch & Bound
#### El problema de los enteros
En el mundo de la optimización al encontrar una solución que optimice nuestra entrada nos encontramos con un problema, **la mayoria de las veces esta solución esta compuesto por números decimales**, debido a este problema surge la pregunta ¿Qué pasa si las soluciones deben ser números enteros?. Para dar solución a este problema se invento el algoritmo **Branch & Bound**.
#### Branch & Bound
El **Branch & Bound** es un algoritmo de optimización entera. Su funcionamiento se basa en explorar un árbol de subproblemas para hallar la mejor solución.
- **Branch (Ramificar)**: Dividir el problema en partes más pequeñas.
- **Bound (Acotar)**: Calcular límites para descartar ramas enteras.
##### ¿Cómo funciona?
![[Pasted image 20251013222118.png]]
Una analogía para el proceso de acotar seria *"Si encuentras un vuelo por 300\$, ignoras las rutas de 350\$. Has puesto una 'cota'"*. Para realizar la poda de posibles soluciones nos guiaremos por las siguientes tres razones:
- **Por cota**: Su mejor solución es peor que una entera ya encontrada.
- **Por optimalidad**: La rama ya dio una solución entera válida.
- **Por infactibilidad**: Las restricciones de la rama la hacen imposible.
##### Ejemplo
Se tiene el siguiente problema de optimización: $$Max\,\,z = 11x_1+14x_2$$Donde $x_1$ y $x_2$ deben ser enteros.
- **Resolvemos ignorando la regla de los enteros:**![[Pasted image 20251013222730.png]]
De este paso podemos obtener que nuestra cota superior será $156.5$ lo que indicará que ninguna solución entera podrá obtener un valor para $z$ mayor al ya obtenido.
- **Ramificamos**![[Pasted image 20251013222958.png]]
Tomamos la variable $x_1$ y establecemos que debe ser moverse entre los dos valores enteros mas cercanos. De esta manera obtenemos que la cota inferior del problema será $141$ (en el caso de que $x_1=9$). Ahora exploraremos la rama más prometedora, la cual es P1, porque su $z$ potencial ($155.2$) es mayor que $141$.![[Pasted image 20251013223602.png]]
##### La solución óptima
El algoritmo se detiene cuando no quedan nodos prometedores. El árbol nos ha guiado a la respuesta. Donde la mejor solución óptima encontrada es $x_{1}= 6$, $x_2=6$, lo cual nos da un valor $z$ máximo de $150$.
##### ¿Por qué es importante?
El poder de Branch & Bound puede verse evidenciado en:
- **Eficiencia:** Convierte problemas enormes en una búsqueda manejable.
- **Base**: Técnica clave en logística, planificación, finanzas y redes.
- **Optimalidad garantizada:** Asegura encontrar la mejor solución entera.
- **Forma de pensar:** Un modelo de exploración y eliminación inteligente.
