De momento se han estudiado dos paradigmas de diseño, los cuales son:
- **Dividir y conquistar** (Búsqueda binaria, Merge Sort, Quick Sort, Strassen, etc.).
- **Backtracking** (A*/Branch and Bound)

Pero ahora empezaremos a estudiar el paradigma de diseño **Greedy**. Los algoritmos **Greedy** son algoritmos que toman decisiones miopes a cada paso y esperan lo mejor al final. Suelen ser fácil de implementar y suelen ser intuitivos. El análisis de estos algoritmos suele ser fácil. Su mayor problema es que estos algoritmos suelen ser **incorrectos**.

**Greedy famosos:**
- Dijkstra.
- Códigos de Huffman.
- Prim.
- Kruskal.
- Simplex.

#### Ejemplo
##### Programación de tareas
Se tiene la siguiente lista de tareas: $$t_1,t_2,...,t_n$$donde cada una de estas tareas tendrá su propia prioridad: $$c_1,c_2,...,c_n$$y su propia duración: $$l_1,l_2,...,l_n$$donde nuestro objetivo será establecer un orden de tareas tal que: $$min \sum_{i=1}^{n}c_iT_i$$donde $T_i$ es el tiempo total hasta completar $i$
###### Instanciación de ejemplo

| Ej    | $c_i$ | $l_i$ |
| ----- | ----- | ----- |
| $t_1$ | 3     | 2     |
| $t_2$ | 2     | 1     |
| $t_3$ | 1     | 1     |

$\sigma = t_1,t_2,t_3$
$c(\sigma) = 3\cdot 2 + 2\cdot 3 + 1\cdot4 = 16$
$\sigma_1 = t_3,t_2,t_1$
$c(\sigma_1) = 1\cdot 1 + 2\cdot 2 + 3\cdot4 = 17$
$\sigma_2 = t_2,t_3,t_1$
$c(\sigma_2) = 2\cdot 1 + 1\cdot 2 + 3\cdot4 = 16$
$\sigma_3 = t_2,t_1,t_3$
$c(\sigma_3) = 2\cdot 1 + 3\cdot 3 + 1\cdot4 = 15$
#### Teorema: Algoritmo greedy para prog. tareas es correcto
Sea $\sigma \neq p_!,p_2,...,p_n$ la solución del algoritmo greedy: $$\frac{c_1}l_{1}\geq\frac{c_2}{l_{2}}\geq \frac{c_1}{l_{1}} ...\geq\frac{c_n}{l_n}$$$$\frac{c_i}{l_{i}}\geq \frac{c_j}{l_j}$$$\sigma$ es la mejor del mundo mundial $\Rightarrow$ No existe un $\sigma^{*}\neq\sigma$ que sea mejor.

Sea $\sigma^{*}$ **cualquier** solución distinta a $\sigma$. Yo voy a proponer un mecanismo que mejore o iguale la realidad de $\sigma^{*}$.
$\sigma^{*}= X,p_j,p_i,Y$ con $j > i$ .
$\sigma^{**} = X,p_i,p_j,Y$
.
.
.
$c(\sigma^{**}) = c(x)+c_i\cdot(T_x+l_i)+c_j\cdot(T_x+l_i+l_j)+C(y)$
$c(\sigma^{*}) = c(x)+c_i\cdot(T_x+l_i)+c_j\cdot(T_x+l_i+l_j)+C(y)$
Los restamos:
$c(\sigma{**})-c(\sigma{*}) = c_jl_i-c_il_j$ y $\frac{c_i}{l_i}\geq\frac{c_j}{l_{j}}\Rightarrow c_il_j-c_jl_i\leq0$



























































































































