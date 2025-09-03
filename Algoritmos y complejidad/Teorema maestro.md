$$T(n) = a\cdot T(\frac{n}{b}) + c\cdot n^d$$
$a$ : número de llamadas recursivas.
$b$ : en cuantas partes se separa la entrada inicial.
$d$ : grado del polinomio del trabajo realizado (trabajo realizado antes de la recursividad).
$n$ : tamaño de la entrada inicial.

Este teorema funcionará cuando el tamaño de subproblemas siempre son iguales y si siempre hago la misma cantidad de llamadas recursivas.

$$T_{total} = T_1 + T_2 +...+T_{log_b(n)} = \sum_{j=0}^{log_b(n)} c (\frac{n}{b^j})^d\cdot a^j$$
$log_b (n)\,\,T = c\cdot n^d \sum_{j=0}^{log_b(n)} (\frac{a}{b^d})^j$
- $a$ : tasa de proliferación de problemas.
- $b^d$ : tasa de reducción del trabajo.
**Caso 1:** $a=b^d$
$$T_n = O(n^d\cdot log (n))$$
**Caso 2:** $a < b^d$
$$r(S) = (1+r+r^2+...+r^k)r$$ $$rS = r+r^2+r^3+...+r^k+r^{k+1}$$ $$rS = S-1+r^{k+1}$$ $$rS-S = r^{k+1} - 1$$
$$S(r-1) = r^{k+1}-1$$ $$S = \frac{r^{k+1}-1}{r-1}$$
Si $r<1 \rightarrow s = c++e$
Si $r > 1 \rightarrow s = c\cdot r^k$
$$T(n) \in O(n^d)$$dominado por la raíz.
**Caso 3:** $a>b^d$
$$T(n)\in O(a^{log_b(n)}) = O(n^{log_b(a)})$$