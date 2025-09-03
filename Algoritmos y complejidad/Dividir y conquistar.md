### Multiplicación de enteros
$X = x_1,x_2,x_3,...,x_n$
$Y =y_1,y_2,y_3,...,y_n$
1. Simulación/definición $O(n*2^4)$
2. Campesino ruso $O(n^2)$
3. Algoritmo de 3ero básico $O(n^2)$
4. D&C_naive $\in O(n^2)$ 
### Dividir y conquistar
- Particionar la entrada (dividir).
- Resolver el problema para cada partición. **(recursivamente)**
- Juntar las soluciones de cada partición para crear una solución global. (conquistar)
##### Ejemplo dividir y conquistar
$4827\cdot 3341$
$x = a\cdot 10^{n/2} + b \Rightarrow a=48,\,b=27$
$y = c \cdot 10^{n/2}+d \Rightarrow c=33,\, d=41$
$p_1 = a\cdot c,\,p_2 = b\cdot d,\,p_3 = b\cdot c,\,p_4 = a\cdot d$
$x\cdot y = a\cdot c \cdot 10^n+(bc+ad)\cdot 10^{n/2}+bd$
```python
d_y_c_naive(x, y):
	//caso base
	x o y tienen un solo digito
	
	//dividir (O(n/2))
	a = mitad_izquierda(x)
	b = mitad_derecha(X)
	c = mitad_izquierda(y)
	d = mitad_derecha(y)
	
	//llamadas recursivas
	p1 = d_y_c_naive(a,c)
	p2 = d_y_c_naive(b,d)
	p3 = d_y_c_naive(a,d)
	p4 = d_y_c_naive(b,d)
	
	return (p1*10^n+(p3+p4)*10^(n/2)+p2) //conquistar (O(n))
```
##### Preguntas
1. Reducción de los subproblemas. 
   R: 2
2. Cuantas llamadas recursivas hacen.
   R: 4
3. Cuánto trabajo se realiza, a partir de las llamadas recursivas. 
   R: O(n)
```python
karatsuba(x,y):
	-> Fondo recursivo
	
	// dividir
	a = mitad_izq(x)
	b = mitad_der(x)
	c = mitad_izq(y)
	d = mitad_der(y)
	
	// llamadas recursivas
	p1 = karatsuba(a, c)
	p2 = karatsuba(b, d)
	p3 = karatsuba(a+b, c+d)
	
	// conquistar
	return (p1*10^n+(p3*p2*p1)*10^(n/2)+p2)
```
$x = a+b$
$y = c+d$
$xy = ac+(bc+ad)i-bd$
$(bc+ad) = (a+b)(c+d)-ac-bd$
##### Preguntas
1. Reducción de los subproblemas. 
   R: 2
2. Cuantas llamadas recursivas hacen.
   R: 3
3. Cuánto trabajo se realiza, a partir de las llamadas recursivas. 
   R: O(n)
```python
bbinaria(l, e, i, f):
	if (i > f):
		return -1
	m = (i+f)//2
	if (l[m] == e):
		return m
	elif (l[m] < e):
		return bbinaria(l, e, m+1, f) # Pasar l por referencia
	else:
		return bbinaria(l, e, i, m-1) # Pasar l por referencia
```
##### Preguntas
1. Reducción de los subproblemas. 
   R: $\frac{n}{2}$
2. Cuantas llamadas recursivas hacen.
   R: 1
3. Cuánto trabajo se realiza, a partir de las llamadas recursivas. 
   R: O(1), siempre y cuando se pase la lista por referencia y no por copia
$T_{bbinaria}(n)\in O(log\,n)$
##### Merge Sort (ejemplo de dividir y conquistar)
![[Pasted image 20250828115216.png]]
```python fold title:mergeSort
def mergeSort(v)
	if (len(v) == 1):
		return
	#----- Dividir -----#
	a = v[0:len(v)//2]
	b = v[(len(v)//2): len(v)]
	
	#----- Llamadas recursivas -----#
	mergeSort(a)
	mergeSort(b)
	
	#----- Conquistar -----#
	merge(v, a, b)
	return
```
- Taza de reducción del tamaño: 2
- \# de llamadas recursivas: 2
- Tiempo de ejecución en cada llamada: $O(n)$
- Tiempo de ejecución total: $T_{mergeSort}(n) \in O(n\,log\,n)$
- Espacio total que utiliza: $E_{mergeSort}(n) \in O(n)$
```python fold title:merge
def merge(v, a, b):
	posI = 0
	posD = 0
	for i in range(len(v)):
		if (posD == len(b) or a[posI] < b[posD]):
			v[i] = a[posI]
			posI += 1
		else:
			v[i] = b[posD]
			posD += 1
	return
```
##### Quick Sort 
![[Pasted image 20250828115259.png]]
```python fold title:quickSort
def quickSort(v, i, f):
	if (i == f):
		return
		
	#----- Pivotear -----#
	p = i
	for (j in range(i+1, f+1)):
		if (v[j] < v[p]):
			swap(v[j], v[p+1])
			swap(v[p], v[p+1])
			
	#----- Llamadas recursivas -----#
	quickSort(v, i, p-1)
	quickSort(v, p+1, f)
```
- Algoritmo **In-place** (se ejecuta sobre el vector inicial)
- Tiempo de ejecución: $T_{quickSort}(n) \in O(n^2)$
##### Naive
```python fold title:Naive
def mul(m1, m2):
	r = []
	for i in range(len(m1)):
		r.append([])
		sum=0
		for j in range(len(m2[0])):
			for k in range(len(m2)):
				sum += m1[i][k] * m2[k][j]
			r[i].append(sum)
	return (r)
```
##### dd_ingenuo
```python fold title:dd_ingenuo
def mul_dd(m1, m2):
	#*=

	#=== Dividir ===#
	a = m1[:]
	b = m1[:]
	c = m1[:]
	d = m1[:]
	e = m2[:]
	f = m2[:]
	g = m2[:]
	h = m2[:]
	
	#=== Recursividad ===#
	p1 = mul_dd(a,e)
	.
	.
	.
	py
	
	#=== Conquistar ===#
	r = (ae + bc)
```
$T_{mul\_dd} \in O(n^3)$
##### Strassen
``p1 = a(f-h)
``p2 = (a+b)h
``p3=(c+d)e
``p4=d(g-e)
``p5=(a+d)(e+h)
``p6=(b-d)(g+h)
``p7=(a-c)(e+f)

```python fold title:Strassen

```
\# llamadas = 7
tamaño de los subproblemas = $\frac{n}{2}$
trabajo en cada fracción $\in O(n^2)$
$$