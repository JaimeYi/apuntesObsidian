Al analizar algoritmos un aspecto muy importante a tener en cuenta será la **complejidad temporal** de este algoritmo. La complejidad temporal hace referencia a una función a la cual se ajuste el tiempo que demore en ejecutarse un algoritmo.
### Notaciones
Para expresar complejidad temporal tendremos distintas notaciones, las cuales serán:
- $O(g(n))$ : Conjunto  de funciones acotadas superiormente por $g(n)$.
- $\Omega (g(n))$ : Conjunto de funciones acotadas inferiormente por $g(n)$.
- $\Theta (g(n))$ : Conjunto de funciones acotadas superiormente e inferiormente por $g(n)$.
##### $O(g(n))$
La función $f(n)$ debe cumplir lo siguiente para pertenecer a $O(g(n))$: $$f(n) \in O(g(n)) \,\,ssi\,\,\exists\,c,\,n_0 > 0\,/\,\forall n>n_0\,\,f(n)\leq c\cdot g(n) $$.
##### $\Omega (g(n))$
La función $f(n)$ debe cumplir lo siguiente para pertenecer a $\Omega (g(n))$.$$f(n)\in\Omega(g(n))\,\,ssi\,\,\exists\,c,\,n_0 > 0\,/\,\forall n>n_0\,\,f(n)\geq c\cdot g(n)$$
.
##### $\Theta (g(n))$
La función $f(n)$ debe cumplir lo siguiente para pertenecer a $\Theta (g(n))$. $$f(n)\in\Theta(g(n))\,\,ssi\,\,\exists\,c_1,\,c_2,\,n_0 > 0\,/\,\forall n>n_0\,\,\,\,c_1\cdot g(n)\leq f(n)\leq c_2\cdot g(n)$$
$$O(1)<O(log\,n)<O(n)<O(n\,\,log\,n)<O(n^2)<O(n^3)<O(2^n)<O(n!)<O(n^n)$$