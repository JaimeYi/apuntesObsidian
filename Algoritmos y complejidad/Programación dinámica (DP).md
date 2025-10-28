La programación dinámica es una técnica de optimización que divide un problema complejo en subproblemas más simples, almacena sus soluciones y las utiliza para construir la solución óptima del problema original.
## Principios DP
- Inspeccionar si puedo construir la solución del problema original a partir de la solución o subproblemas más pequeños.
- Etiquetar los subproblemas de tal manera de usar las etiquetas como claves de un diccionario (tabla) de soluciones parciales (memoizing).
## Implementaciones posibles
### Top-Down
Esta implemetación de programación dinámica consiste en resolver un problema dividiéndolo en subproblemas más pequeños y usando la recursión para abordarlos. Es caracterizado por utilizar llamadas recursivas con memoization.
#### Ejemplo
**Fibonacci**
```python title:fibonacciTopDown
def fib(n):
	tabla = [0]*(n+1)
	tabla[1] = 1
	tabla[2] = 1
	for i in range(3,n+1):
		tabla[i] = tabla[i-1]+tabla[i-2]
	return (tabla[n])
```

**Weighted Maximum Independent Set**
Como ejemplo se utilizará el problema *Weighted Maximum Independent Set (WMIS)*.

Entrada: $G=(V,E)$   $w:V\rightarrow\mathbb{R}$
Salida: $V_0<V$ con $\{v_1,v_{2}\}\leq\rightarrow V_{0}(v_1,v_2)\notin E$
       $max\,\,\sum\limits_{i\in v_{0}} w_{i}$
```python title:wmisTopDown
global dp=[0]*1000001
def wmis(W,n):
	if n == 1:
		dp[n] = w[1]
	elif n == 2:
		dp[n] = max(w[1],w[2])
	else:
		if dp[n-1] == 0:
			wmis(w,n-1)
		if dp[n-2] == 0:
			wmis(w,n-2)
		dp[n] = max(dp[n-1],dp[n-2]+w[n])
	return dp[n]
```
### Bottom-up
Esta segunda implemetación de programación dinámica consiste en resolver subproblemas más pequeños de un problema general primero, y luego utiliza esas soluciones para resolver subproblemas más grandes, hasta llegar a la solución final. Es caracterizado por computaciones iterativas y llenado de tabla.
#### Ejemplo
**Weighted Maximum Independent Set**
```python title:wmisBottomUp
def wmis(W,n):
	dp=[-inf]*(n+1)
	dp[1] = W[1]
	dp[2] = max(w[1],w[2])
	for i in range(3,n+1):
		dp[i] = max(dp[i-1], dp[i-2]+w[i])
	return (dp[n])
```