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
```
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
```
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
```
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
# Cambiar parámetros de sorting en tarea...