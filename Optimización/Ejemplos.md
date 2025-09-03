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
$y_{4c} + 5y_{5c} = 80$
$y_{10c} = 4$
$0.1y_{7c} + 0.2y_{8c} + y_{9c} \geq 0.5$

**Relación de variables**
$\sum_{j=a}^c \, y_{ij}=x_i$, $\forall i = 1,...,10$

**Naturaleza de las variables**
$x_i \geq 0$, $\forall i =1,...,10$
$y_{ij} \geq 0$, $\forall i =1,...,10 \land \forall j = a,\,b,\,c$

### Certamen 1 2024-2
#### Pregunta 1
##### Variables de decisión
- $S$: Cantidad de sillas.
- $M$: Cantidad de mesas.
- $E$: Cantidad de estanterias.
- $H$: Horas extras.
- $X$: Madera extra.
##### Función objetivo
$$Max\,\,Z = S\cdot50+M\cdot80+E\cdot60-X\cdot7-H\cdot20$$
##### Restricciones
- $H \leq 40$ // Restricción de horas extras
- $M \geq 10 \land E\geq8$ // Demanda mínima de mesas y estantes
- $10\cdot S+20\cdot M + 15 \cdot E \leq 500$ // Disponibilidad de clavos
- $3 \cdot S + 5 \cdot M + 4 \cdot E \leq 150+X$ // Disponibilidad de madera
- $4 \cdot S + 6 \cdot M + 5 \cdot E \leq 200+H$ // Disponibilidad de horas de trabajo
- $10\cdot S + 20\cdot M \leq 300$ // Restricción de almacenamiento
- $S,\,M,\,E,\,H,\,X \geq 0$ // No negatividad de las variables
#### Pregunta 2
##### Variables de decisión
- $C_{EP}$ : Costo de asignación por equipo y proyecto.
- $T_{EP}$ : Tiempo estimado de finalización por equipo y proyecto.
- $X_E$ : Cantidad de proyectos asignados.
- $A_{EP}$ : Proyecto asignado.
- $E\in \{1,2,3,4\}\land P\in\{A,B,C\}$
##### Función objetivo
$$Min\,\,Z = C_{EA}+C_{2B}+C_{KC}$$
Donde $E\neq K\land E,K \in \{1,3,4\}$
##### Restricciones
- $X_E \leq 1$, $E\in \{1,2,3,4\}$
- $T_{iA} + T_{2B} + T_{jC} \leq 20$, $i \neq j \land i,j \in \{1,3,4\}$
- $T_{1P} \leq 7$, $P \in {A,B,C}$
- $A_{4C} \Rightarrow A_{3i} \neq A_{3A}$, $i \in \{A,B,C\}$ 
### Certamen 1 2024-1
#### Pregunta 1
##### Variables de decisión
- $x_{ij}$ : Cantidad de flores de tipo i de color j
- $y_{ij}$ : Precio de flor de tipo i de color j
Donde $i\in$ {Rosa = 0, Lirio = 1, Gardenia = 2, Hortensia = 3, Tulipán = 4, Caléndula = 5} $\land$ $j\in$ {Rojo = 0, Blanco = 1, Amarillo = 2, Rosado = 3}
##### Función objetivo
$$Min\,\,Z = \sum_{i=0}^5 \sum_{j=0}^3\,\,x_{ij}\cdot y_{ij}$$
##### Restricciones
- $\sum_j x_{0j} \leq 20,\sum_j x_{1j} \leq 10,\sum_j x_{2j} \leq 8,\sum_j x_{3j} \leq 5,\sum_j x_{4j} \leq 20,\sum_j x_{5j} \leq 6$
- $\sum_i x_{i0} = 15,\sum_i x_{i1} = 10, \sum_i x_{i2} = 8,\sum_i x_{i3} = 7$
- $x_{00} \geq 5$
- $\sum_j 2x_{3j} \leq \sum_j x_{1j}$
- $x_{42} = 0$
- $\sum_i 0.3x_{i1} \leq x_{21}$
- $x_{ij} \geq 0, \forall i,j$
#### Pregunta 2
##### Variables de decisión 
- $X_{ij}$ : {1 si se escoge la ruta $i$ para la ciudad $j$, 0 $eoc$}
##### Parámetros 
- $P_{ij}$ : Costo de la ruta $i$ para la ciudad $j$
- $T_{ij}$ : Tiempo empleado al tomar la ruta $i$ hacia la ciudad $j$
Con $i \in \{1,2,3,4\}$ y $j \in \{chillan = 1, temuco = 2, valdivia = 3, pto. montt = 4, chiloe = 5\}$
##### Función objetivo
$$Min\,\,Z = \sum_i \sum_j P_{ij}\cdot X_{ij}$$
##### Restricciones
- $\sum_i \sum_j T_{ij}\cdot X_{ij} \leq 24$
- $\sum_i\sum_j X_{ij} = 5$
- $X_{21} \leq 1-X_{23}$
- $X_{44} \leq X_{15}$
- $\sum_{i} \sum_{j=1}^4 ( T_{ij}\cdot X_{ij} + T_{(i+1)j}\cdot X_{(i+1)j}) \leq 10$
- $X_{ij}\in{0,1};\forall i \in \{1,2,3,4\}; \forall j \in \{1,2,3,4,5\}$
#### Pregunta 3
##### Variables de decisión
- $X_{i}$ : Cantidad de menús $i$ preparados
- $Y_i$ : {1 si se preparará el menu $i$ en el día, 0 $eoc$}
##### Parámetros 
- $T_i$ : Tiempo de preparación del menú $i$
- $P_i$ : Precio del menú $i$
##### Función objetivo
$$Max\,\,Z = (\sum_i X_i\cdot P_i)+40000+100\cdot60\cdot8$$
##### Restricciones
- $X_5 \geq 7$
- $X_4\geq2$
- $X_1+X_3 \geq 10$
- $Y_2 - Y_4 \geq 1$
- $Y_5 + Y_1 \neq 1$
- $2Y_3-Y_2-Y_5\geq 0$
- $\sum_i X_i\cdot T_i \leq 8\cdot60$
### Ayudantía pre-certamen
#### Pregunta 2
Don Dimmadone planea construir nuevos estudios en 6 posibles ciudades. Para este gran proyecto, debe considerar el costo de construcción por estadio y cómo distribuir a sus ejecutivos para que supervisen los avances, tomando en cuenta sus tiempos de viaje, por los cuales cobran 15 dólares la hora, y que no pueden visitar más de dos construcciones de cada uno. La tabla a continuación muestra el tiempo (en horas) de viaje de cada ejecutivo a cada ciudad.

| Tiempo de Viaje | Ejecutivo A | Ejecutivo B | Ejecutivo C |
| --------------- | ----------- | ----------- | ----------- |
| Ciudad 1        | 2           | 3           | 2.5         |
| Ciudad 2        | 1.2         | 2           | 0.8         |
| Ciudad 3        | 0.3         | 0.5         | 1           |
| Ciudad 4        | 1           | 2.3         | 3           |
| Ciudad 5        | 4           | 3           | 2.5         |
| Ciudad 6        | 0.5         | 1           | 1           |
Además, quiere cubrir el mayor público posible, por lo que fijó las siguientes restricciones:
- No puede construir más de un estadio por ciudad.
- Debe construir al menos 3 estadios para no perder presencia en el negocio.
- Debe haber al menos un estadio entre las ciudades 3 y 4.
- Si construye en la ciudad 5, no se construirá en la ciudad 2.
- Puede haber a lo más dos estadios entre las ciudades 1, 3 y 6.
- Se puede construir en la ciudad 1 sólo si se construye también en la ciudad 4.
##### Variables
- $x_i$ : 1, si se construye el estadio en la ciudad $i$. 0 $eoc$
- $y_{ij}$ : 1, si a la ciudad i se le asigna el ejecutivo $i$. 0 $eoc$
$i = 1,...,6$ y $j = A, B, C$
##### Parámetro
- $C_{ij}$ : Costo de asignar el ejecutivo $j$ a la ciudad $i$.
##### Función objetivo
$$min\,\,Z = 500\sum_{i=1}^6 x_i\cdot 10^6 + 15(\sum_{i=1}^6 \sum_{j=A}^C y_{ij}\cdot c_{ij})$$
##### Restricciones
- $x_i = \sum_{j=A}^C y_{ij}$, $\forall i \in \{1,2,...,6\}$
- $\sum_{i=1}^6 y_{ij} \leq 2$, $\forall j = A,B,C$
- $\sum_{i=1}^6 x_i \geq 3$
- $x_3+x_4 \geq 1$
- $x_2+x_5\leq1$
- $x_1+x_3+x_6 \leq 2$
- $x_1\leq x_4$
- Naturaleza de variables : $x_i \in \{0,1\}$, $y_{ij} \in \{0,1\}$, $\forall i \in \{1,...,6\}$, $\forall j \in \{A,B,C\}$
