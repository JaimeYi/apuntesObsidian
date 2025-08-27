### Certamen 1 xxxx-x
##### Variables
$x_i$ : Cantidad de Kg de oro comprado al inicio del mes i
$y_i$ : Cantidad de Kg de oro vendido al final del mes i
##### Parámetros
$PC_i$ : Precio de compra de oro en el mes i
$PV_i$ : Precio de venta  de oro en el mes i
##### Función objetivo
$Max\,\,z =\sum_{i=1}^{4} PV_i\,y_i - \sum_{i=1}^4 PC_i\,x_i$
##### Restricciones
Enero: $(50 +x_i-y_0 \leq 100\,\,\,\, con\,\,y_0 = 0 )\land (300x_1 \leq 1000)$

Febrero: $(50 + x_1 +x_2-y_1 \leq 100) \land (300x_1+350x_2 \leq 1000 + 250y_1)$

Marzo: $(50 + x_1 +x_2+x_3-y_1-y_2 \leq 100)\land (300x_1+350x_2+400x_3 \leq 1000 + 250y_1+400x_2)$

Abril: $(50 + x_1 +x_2+x_3+x_4-y_1-y_2-y_3 \leq 100)\land (300x_1+350x_2+400x_3+500x_4 \leq 1000 + 250y_1+400x_2+350x_3)$

Forma compacta: $(50 + \sum_{j=1}^i x_j - \sum_{k=1}^{i-1}y_{j-1}\,\,\,\,\forall k = 0,...,3) \land (\sum_{j=1}^i Pc_j\,x_j \leq 1000 + \sum_{k=1}^{i-1} Pv_k\,y_k\,\,\,\,\forall j=1,...,4.\,\,\forall k=1,...,3)$
### Certamen 1 2025-1
#### Pregunta 1
Una distribuidora dispone de 100 kilogramos de azúcar, 150 kilogramos de harina y 10 kilogramos de
polvos de hornear. Con esto, deben envasar el azúcar en paquetes de 1, 2 y 5 kilogramos; la harina
en envases de 1, 5 y 10 kilos; y los polvos de hornear en 100, 200 y 500 gramos. Además, también
ofrecen paquetes de 1 kilogramo de harina con 20 gramos de polvos de hornear. Ellos distribuyen a tres minimarkets de barrio: Don Pimentón, El Gran Bodegón y Mercado al Día. Cada minimarket tiene sus propios precios de compra de los productos y especificaciones del pedido:
(a) **Don Pimentón:**
- Al menos 20 kilogramos de harina, independiente del tipo de paquetes.
-  Exactamente 15 kilos de azúcar, en envases de 1 y 2 kilogramos.
-  Al menos 1 kilogramo de polvos de hornear en paquetes de 100 gramos.
(b) **El Gran Bodegón:**
- Al menos 5 kilogramos de harina con polvos de hornear.
- 3 paquetes de 2 kilos de azúcar y 4 de 1 kilo.
(c) **Mercado del día:**
- Exactamente 20 kilogramos de harina en paquetes de 1 y 5 kilogramos.
- 4 paquetes de harina con polvos de hornear.
- Al menos 0,5 kilogramos de polvos de hornear.

A continuación, una tabla con los precios:
![[Pasted image 20250827101459.png]]

Genere un modelo de programación lineal para que la distribuidora decida cuántos paquetes hacer y cómo venderlos, con el objetivo de maximizar ventas.
##### Desarrollo
**Variables**:
$X_i:$ Cantidad de paquetes del producto $i$
$Y_{ij}:$ Cantidad de paquetes del producto $i$ vendidos al minimarket $j$, $\forall j=a,\,b,\,c$

**Parámetro**
$P_{ij}$ Precio del paquete de producto $i$ para el minimarket $j$

**Función Objetivo**
$Max\,Z = \sum_{j=a}^c \sum_{i=1}^{10}\, P_{ij}\,Y_{ij}$

**Restricciones**
*Disponibilidad material*
$x_1+2x_2+5x_3 \leq 100$
$x_4+5x_5+10x_6+x_10 \leq 150$
$0.1x_7+$

*Don Pimentón*
$y_{4a}+5y_{5a}+10y_{6a} \geq 20$
$y_{1a}+2y_{2a} = 15$
$0.1y_{7a}+0.2x_8+0.5x_9+0.02x_{10} \leq 10$

*El Gran Bodegón*
$y_{10b} \geq 5$
$y_{1b} = 4$
$y_{2b} = 3$ \# Paquetes

*Mercado al día*

