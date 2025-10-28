3# Árbol de cobertura/expansión mínimo (MST)
Entrada: $G=(V,E),\,\,w:E\Rightarrow\mathbb{R}$, $G$ es conexo.
Salida: $T\leq E \rightarrow$ No tiene ciclos, $T$ cubre $V$, $|T|=|V|-1$
$min\,\,\sum\limits_{e\in T}w(e)$.
## Prim-Janick
```python title:Prim-Janick
Prim-Janick(G=(v,e),w):
	C = {v1}
	T = {}
	mientras |c| < |V|:
		(v,w) = e = min(aristas que cruzan de C a V\C con v perteneciente a c y w perteneciente a v\c)
		T = T union {e}
		C = C union {w}
	retornar T
```
$T_{prim\_janick\_ingenuo}(n,m)\in O(n\cdot m)$
### Maneras de implementar grafos
1. Listas de adyacencia
   `vector<vector<pair<int,double>>> g`
2. Matriz de adyacencia
   ![[Pasted image 20251021102245.png]]
3. Lista de aristas
   `vector<pair<pair<int,int>,double>>`

```c++ title:Prim_Janick
vector<pair<int,int>> prim_janick(vector<vector<pair<int,double>>>& g){
	vector<bool> c(g.size(),false);
	priority_queue<pair<double,pair<int,int>>> pq;
	vector<pair<int,int>> T;
	
	C[0] = true;
	for (auto e : g[0]){
		pq.push(make_pair(e.second,make_pair(0,e.first)))
	}
	
	while (T.size() < g.size()-1){
		auto e = pq.top();
		pq.pop();
		double w = e.first;
		double a = e.second;
		
		if (c[a.first] and (c[a.second])){
			T.push_back(a);
			c[a.second] = true;
			for (auto e : g[a.second]){
				pq.push(make_pair(e.second,make_pair(a.second,e.first)));
			}
		} else if (c[a.second] and (c[a.first])){
			T.push_back(a);
			c[a.first] = true;
			for (auto e : g[a.first]){
				pq.push(make_pair(e.second,make_pair(a.first,e.first)))
			}
		}
	}
	return (T);
}
```

```python title:prim_janick v2
prim_janick(G=(V,E), w):
	cubiertos = {v0}
	T = {}
	pq = min_heap_vacio
	
	for e in vecinos(vo):
		pq.push(e)
		
	while |cubiertos| < |V|:
		e = pq.pop()
		if (e = (v,t) / v in cubiertos and t not in cubiertos):
			cubiertos = cubiertos union {t}
			T = T union {e}
			for e in vecinos(t):
				pq.push(e)
	return (T)
```

$T(n,m) \in O (m\,\,log\,m) \in O(m\,\,log\,n)$

```python title:Kruskal
Ordenar 
T = {}
for e in |E|:
	if e no hace ciclo en T:
		T = T union {e}
utilizar union_find
```

El usar `prim_janick` o `kruskal` dependerá de la densidad del grafo, para grafos muy densos utilizar `prim_janick`, caso contrario utilizar `kruskal`
### Teorema: propiedad del corte del MST:
Si $e$ es una arista en algún corte de $G$, $e$ pertenece a algún MST.
#### Demostración del teorema por contradicción
Asumo que $e$ es la arista de menor costo del corte $C(s,\overline{s})$ pero existe un árbol de cobertura mínimo $T^*$ en el que no está $e$.