El **Backtracking** es una técnica algorítmica para resolver problemas probando todas las soluciones posibles de forma sistemática. Dentro del backtracking tendremos las siguientes posibles soluciones:
- Generar todas las combinaciones de $k$ elementos de $n$ con/sin repetición. (con repetición = $n^k$, sin repetición = $\binom{n}{k}$)
- Generar todas las permutaciones de $n$ elementos. ($n!$)
- Generar todos los subconjuntos de $n$ elementos. ($2^n$)
```cpp title:ejemplo1
bool cumple_propiedad(vector<int>& comb){
	vector<int> global;
	bool generar_combinaciones(vector<int>& elems){
		global.clear();
		for (int  i = 0; i <  elem.size()-1; ++i){
			global.push_back(elems[i]);
			for (int j = i*1; j < elems.size(); ++j){
				global.push_back(elems[j]);
				if (propiedad(global)) return true;
				global.pop_back();
			}
			global.pop_back();
		}
	return (false);	
	}
}
```

```cpp title:generacionDeTodasLasCombinaciones
vector<int> perm;
bool generar_permutaciones(vector<bool>& usados, vector<int>& elems){
	if (perm.size() == usados.size()){
		return propiedad(perm);
	}
	for (int i = 0; i < usados.size(); ++i){
		if (not usados[i]){
			usados[i]=true;
			perm.push_back(elems[i]);
			if (generar_permutaciones(usados, elems)) return true;
			perm.pop_back();
			usados[i] = false;
		}
	}
	return false;
}
```

![[apuntesObsidian/Algoritmos y complejidad/Untitled Diagram.svg]]
