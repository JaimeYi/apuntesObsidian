Un problema computacional esta definido si uno es capaz de definir la entrada del problema, la salida del problema y cuando la salida del problema corresponde correctamente a la entrada del problema. Ej: Encontrar el camino más corto entre dos nodos dentro de un grafo. 

Se debe definir formalmente la entrada y la salida del problema, a la entrada del problema se le conocerá como **precondición**, mientras que a la salida del problema se le conocerá como **postcondición**.

Para los problemas computacionales tendremos que hacer uso de **algoritmos**, los cuales deberán ser capaces de solucionar el problema. Un algoritmo diremos que es una especie de receta que toma el input del problema y mediante una secuencia de instrucciones se calculará el output del problema.![[Pasted image 20250807112420.png]]
Salidas posibles:
- Si/No → Decisionales.
- Numérico → Optimización.
- Secuencia de valores (lista) → Asignación.
### Instancia
Una instancia será una entrada cualquiera de un problema, dado que existen muchas posibles instancias para un problema definiremos la **cardinalidad de una instancia** como la cantidad de posibles instancias de un problema. Ej: Encontrar el menor de dos números (instancia: \[2, 3], cardinalidad: $2^{64}\cdot 2^{64}$ (en computadores actuales)).
### Propiedades de los algoritmos
- Correctitud: Resuelve el problema computacional para el cual fue diseñado.
- Terminación: Punto donde el algoritmo deja de ejecutarse y produce un resultado.
- Eficientes: Se busca que se minimice el consumo de recursos (tiempo y espacio).
	- Para medir el tiempo dependeremos del hardware donde se ejecute el algoritmo como en la instancia utilizada, donde esta podrá variar en tamaño (\#bits que ocupa la entrada) y en la distribución de los datos (mejor caso, caso promedio, peor caso).
- Precisos
- Elegantes
```
def mis(a, b):
	x=a, y=b
	z=0
	while (x > 0):
		asset(x > 0)
		z += y
		x -= 1
	return z	
```
$a, b, z \in \mathbb{N}$

- Teorema: al terminar el algoritmo $z = a \cdot b$.
- Técnica: Invariante de ciclo → predicado que relaciona variables del código → expresión que se evalúa a T/F.
---
$V^{\ell,t}$ : Valor de la variable v, en la línea $\ell$, en la iteración t.
##### Inicialización
Invariante se cumple al ingresar al ciclo. Siguiendo el algoritmo visto anteriormente:
- $y^{\,4,\,0} = b$
- $x^{\,4,\,0} = a$
- $z^{\,4,\,0} = 0$
→ $ab = 0 + a \cdot b$
##### Mantenimiento
invariante se cumple de una iteración t, a una iteración t+1. Siguiendo el algoritmo visto anteriormente:

Por inducción en t asumo que se cumple $$ab = z^{\,4,\,t} + x^{\,4,\,t}\cdot y^{\,4,\,t}$$Demuestro que $$1)\,\,\,\,ab=z^{\,4,\,t+1} +x^{\,4,\,t+1}\cdot y^{\,4,\,t+1}$$$$\begin{aligned}
z^{\,4,\,t+1} = z^{\,4,\,t} + y^{\,4,\,t} \Rightarrow z^{\,4,\,t} = z^{\,4,\,t+1}-y^{\,4,\,t} \\ \\
y^{\,4,\,t+1} = y^{\,4,\,t} \Rightarrow y^{\,4,\,t} = y^{\,4,\,t+1} \\ \\
x^{\,4,\,t+1} = x^{\,4,\,t} -1 \Rightarrow x^{\,4,\,t} = x^{\,4,\,t+1} +1 
\end{aligned}$$Reemplazando en 1) $$\begin{align}
ab = (z^{\,4,\,t+1} - y^{\,4,\,t})+(x^{\,4,\,t+1}+1)\cdot y^{\,4,\,t+1} \\ \\
ab = z^{\,4,\,t+1} - y^{\,4,\,t+1}+x^{\,4,\,t+1}\cdot y^{\,4,\,t+1}+y^{\,4,\,t+1} \\ \\
ab = z^{\,4,\,t+1}+x^{\,4,\,t+1}\cdot y^{\,4,\,t+1}
\end{align}$$Queda por demostrado mediante inducción.
##### Terminación
 Invariante se cumple al salir del ciclo. Siguiendo el algoritmo visto anteriormente: $$\begin{align}
 ab = z^{\,7,-} + x^{\,7,-} \cdot y^{\,7,-} \\ \\
 z^7 = z^{4,\,u} + y^{4,\,u} \Rightarrow z^{4,\,u} = z^{7} - y \\ \\
 x^7 = 0 = x^{4,\, u} \\ \\
y^{7,-} = y^{4,u} = y = b \\ \\

\Rightarrow z^7=ab
\end{align}$$
### Sección 3: Costo computacional
$$T(n) = 4 + 5\cdot a \Rightarrow T(n) = 4 + 5\cdot 2^{\frac{n}{2}}$$Donde $n$ corresponde al número de bits que ocupa la entrada.
$a$ ocupa $\frac{n}{2}$ bits de la entrada. $$\begin{align}E(n) = n + \frac{n}{2} +  \frac{n}{2} + n\\ E(n)=3n\,\,(si\,consideramos\,la\,entrada) \\ E(n)=2n\,\, (si\,no\,consideramos\,la\,entrada) \end{align}$$.
### Demostración de correctitud
Teniendo el siguiente algoritmo:
```
def russian(a, b):
	x = a, y = b, z = 0
	while (x > 0):
		if (x % 2 == 1):
			z += y
		x = x >> 1
		y = y << 1
	return z
```
**Invariante:**
$ab = z^{3,\,t}+x^{3,\,t}\cdot y^{3,\,t}$
**Mantenimiento:**
Por inducción: demostramos para t+1
##### $x^{3,\,t}$ es impar
$z^{3,\,t+1} = z^{3,\,t} + y^{3,\,t}$
$z^{3,\,t}=z^{3,\,t+1}-y^{3,\,t}$
### Selection sort
```
void sel(vector<int>& v) {
	for (int i=0; i < v.size()-1; ++i) {
		if (v[j] < v[m]) {
			m = j;
		}
	}
	swap(&v[i], &v[m]);
}
```
**Invariante:**
$m = index(min(v[i:j^{\,4,\,t}]))$
**Mantenimiento:**
asumo $m^{\,4,\,t} = index(min(v[i:j^{\,4,\,t}]))$
intento demostrar que se cumple: $m^{\,4,\,t+1} = index(min(v[i:j^{\,4,\,t+1}]))$.
##### $v[j^{\,4\,,t}] < v[m^{\,4\,,t}]$
$m^{\,4\,,t+1} = j^{\,4\,,t} \Rightarrow$ por transitividad $\Rightarrow m^{\,4\,,t+1} = index(min(v[i:j^{\,4,\,t+1}]))$ 