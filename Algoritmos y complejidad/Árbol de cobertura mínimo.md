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

```{c++ icon} title:Prim_Janick
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