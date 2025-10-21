### Codificación Huffman
#### Problema
Dado un alfabeto $\Sigma$ y una función de ocurrencia $o:\Sigma \rightarrow \mathbb{R}$ 
#### Salida
Calcular el árbol binario libre de prefijos que: $min\,\Sigma_{i=1}^{|\Sigma|}o(i)\cdot h(i)$, donde $o(i)$ es la ocurrencia de $i$ y $h(i)$ representa la altura en la que se encuentra $i$ en el árbol binario.
#### Ejemplo
$\Sigma =$ {A, B, C, D, E, F}
$o =$  {3, 6,  4, 6, 9, 12}
![[apuntesObsidian/Algoritmos y complejidad/Untitled Diagram 1.svg]]
**Proceso utilizado para crear el árbol:**
{A:3, B:6, C:4, D:6, E:9, F:12} $\rightarrow$ {B:6, D:6, E:9, F:12, AB: 7} $\rightarrow$ {E:9, F:12, AC:7, BD:12} $\rightarrow$ {F:12, BD:12, ACE:16} $\rightarrow$ {ACE:16, FBD:24} $\rightarrow$ {ACEFBD: 30}
$= \frac{3\cdot3+6\cdot3+3\cdot4+3\cdot6+2\cdot9+2\cdot12}{40} = \frac{99}{40} = 2,475$ b/s.
#### Pseudocódigo
```cpp title:Huffman_ingenuo
Huffman(sigma, o):
if (|sigma|) == 2:
	T_prima = sigma1 union sigma2
	o(T_prima) = o(sigma1) + o(sigma2)
else:
	a = min_0(sigma)
	sigma = sigma - a
	b = min_0(sigma)
	sigma = sigma - b
	T = a union b
	o(T) = o(a) + o(b)
	sigma = sigma + T
	Huffman(sigma, o)
```
$T_{Huffman\_{ingenuo}}(n)\in O(n²)$ 
```cpp title:Huffman
string huffman(priority_queue<pair<int,string>> pq){
	while (pq.size() > 1){
		auto a = pq.top();
		pq.pop();
		auto b = pq.top();
		pq.pop();
		auto ab = make_pair(a.first + b.first, string("(") + a.second + string(",") + b.second + string(")"));
		pq.push(ab);
	}
	return pq.top().second;
}
```

```python title:treeHuffman
Tree Huffman(sigma, f):
	if |sigma| == 2:
		a = sigma_1
		b = sigma_2
		return arbol con a y b como hijos de un nodo intermedio
	else:
		sigma_aux = sigma
		a = min_f(sigma_aux)
		sigma_aux -= a
		b = min_f(sigma_aux)
		sigma_aux -= b
		crear metasimbolo 'ab' con f(a,b) = f(a) + f(b)
		sigma_aux += ab
		T_aux = Huffman(sigma_aux,f)
		T = T_aux con ab expandido
		return (T) 
```
Demostración por inducción:
- **P(R):** Huffman calcula el árbol óptimo para un alfabeto $\Sigma$ y una función de frecuencia f, tal que $|\Sigma| = k$.
- **Caso base:** p(2) $\rightarrow$ $L(t) = f(a) + f(b)$
- **Hipótesis inductiva:** Si $P(k-1)$ se cumple, entonces $P(k)$ se cumple.
	- Por hipótesis de inducción, sabemos que $T'$ es óptimo para la entrada $\Sigma ' = \Sigma$
	- Si $T'$ es el mejor $x_{ab}'$, será que $T$ es el mejor de $x_{ab}$.