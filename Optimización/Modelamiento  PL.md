## Ejemplo 1
En un taller de confecciones pueden procesarse un máximo de 500 productos (mochilas, carteras, billeteras, otros) por semana. Esta semana, el taller de confecciones ha recibido la solicitud de 3 clientes por el servicio de corte de productos, con las siguientes características:

| C   | Cm  | Dc  | U   |
| --- | --- | --- | --- |
| 1   | 300 | 8   | 2.0 |
| 2   | 250 | 7   | 2.5 |
| 3   | 150 | 6   | 3.0 |
Se busca maximizar la utilidad.

#### Desarrollo
Comenzaremos definiendo las variables del problema
- **Variables**
	- $x_i$ = cantidad de cortes que solicita el cliente
Luego, definiremos la función objetivo
- **Función objetivo**
	- $Max\,\,z = 2x_1+2.5x_2+3x_3$
Ahora analizaremos las restricciones del problema
- **Restricciones**
	- $x_1+x_2+x_3 \leq 500$
	- $\frac{(8x_1+7x_2+6x_3)}{x_1+x_2+x_3}\leq 6 \Rightarrow (8x_1+7x_2+6x_3)\leq6(x_1+x_2+x_3)$
	- $x_1\leq300$
	- $x_2\leq250$
	- $x_3\leq150$
	- $x_1,\,x_2,\,x_3\geq0$
## Ejemplo 2
En un taller de confecciones pueden procesarse un máximo de 1500 productos (mochilas, carteras, billeteras, otros) por semana. Esta semana, el taller de confecciones ha recibido la solicitud de 7 clientes por el servicio de corte de productos, con las siguientes características:

| C   | Cm  | Dc  | U   |
| --- | --- | --- | --- |
| 1   | 300 | 8   | 2.0 |
| 2   | 250 | 7   | 2.5 |
| 3   | 150 | 6   | 3.0 |
| 4   | 200 | 8   | 2.5 |
| 5   | 150 | 5   | 2.0 |
| 6   | 230 | 5   | 2.5 |
| 7   | 500 | 3   | 3.0 |
La dificultad promedio ponderada del total de productos por cortar no debe ser mayor a 5. El taller quiere conocer que cantidad de corte de productos genera la mayor utilidad.
#### Desarrollo
Comenzaremos definiendo las variables del problema
- **Variables**
	- $x_i$ = cantidad de cortes que solicita el cliente
Luego, definiremos la función objetivo
- **Función objetivo**
	- $Max\,\,z = 2x_1+2.5x_2+3x_3+2.5x_4+2x_5+2.5x_6+3x_7 \Rightarrow$
	  $Max\,\,z=\sum_{i=1}^{7}u_ix_i$
Ahora analizaremos las restricciones del problema
- **Restricciones**
	- $\sum_{i=1}^7 x_i \leq 1500$
	- $\sum_{i=1}^7 Dc_i x_i \leq 5\sum_{i=1}^7 x_i$
	- $x_i\leq Cm_i\,\,\forall i = 1,...,7$
	- $x_i\geq0\,\,\forall i = 1,...,7$