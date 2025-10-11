## Pregunta 1
Por un lado, notación asintótica $O ,\Omega, \Theta$ 
- $f(n) \in O(g(n)) \Rightarrow$ $g(n)$ crece de manera igual o menor que $f(n)$. Es decir, la notación $O$ indicará que dicha función crecerá **como mucho** $O(...)$. No confundir peor caso con notación $O$.
- $T(n) \in O(n³) \Rightarrow T(n)$ tiempo de ejecución será menor o igual a $n³$. Es decir, la notación $\Omega$ indicará que dicha función crecerá **al menos** $\Omega(...)$. 
- $E(n) \in \Omega (n\,\,log\,n) \Rightarrow$ El espacio utilizado será mayor o igual a $n\,\,log\,n$.
- Punto aparte: La notación $\Theta$ indicará que una función crecerá **como mínimo** $\Theta (...)$.
¿Qué analizamos?
- Pesimista (Peor caso): la entrada trata de sabotear el funcionamiento del algoritmo.
- Caso promedio: Análisis probabilístico que busca saber cuál es el consumo de recursos esperados.
- Caso amortizado: Análisis sobre una "secuencia de llamados".
## Pregunta 2
### Parte 1
$$log_{a}\,{n}\in\Omega(log_2\,{n}),\,\,\,\forall a>0$$
$$\exists c,n_{0}\,\,tal\,que\, \,log_{a}\,(n)\geq c\cdot log_2(n) $$
$$c \leq \frac{1}{log_{2}\,a}$$
Por lo que para que esto se cumpla $a > 1$.
### Parte 2
- Invariante: $idx\_max$ contiene la primera aparición del elemento más grande de A$[0:i]$
## Pregunta 3
```cpp title:generarFractal()
def generarFractal(m,x0,y0,n):
if (n <= 1):
	M[y0][x0] = calc...
for i in range(n):
	for j in range(n):
		M[y0+i][x0+j] = calc...
generarFractal(M,x0,y0,n/2)
```
- $a = 1$
- $b =2$
- $d = 2$
$T(n) \in a\cdot T(\frac{n}{b})+c(n^d)\Rightarrow T(n)\in O(n²)$
## Pregunta 4
```cpp title:algorithm
// Bloque A
for (int y : b) en_b.insert(y);

// Bloque B
for (int u : a){
	int v = x-u;
	if (en_b.find(v) != en_b.end()){
		pares_ordenados.insert(make_pair(u,v));
	}
}

// Bloque C
vector<pair<int, int>> resultado(pares_ordenados.begin(), pares_ordenados.end());
```
- Bloque A $\in O (m\,\,log\,m)$
- Bloque B $\in O(n\,\,log\,m + n\,\,log\,n)$
- Bloque C $\in O(n)$
- 