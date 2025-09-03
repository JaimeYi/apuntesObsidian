# Programación matemática
### Definición
La programación matemática es una rama de la investigación de operaciones que se encarga de **formular y resolver problemas de optimización**. El objetivo que se busca es **encontrar el valor óptimo (mínimo o máximo)** de una función (la cual llamaremos función objetivo), **sujeta a restricciones** que limitaran las posibles soluciones del problema.
### Ejemplo
Optimizar $f(x)$ sujeto a $g_i(x) \leq b_i,\,\,x\in X$
### Categorización
Dependiendo de la naturaleza de la función y las restricciones, el problema modelado podrá corresponder a:
- **Programación lineal (PL):** Función objetivo y restricciones lineales.
- **Programación entera (PE):** Alguna o todas las variables son enteras.
- **Programación no lineal (PNL):** Función objetivo o restricciones no lineales.
- **Programación dinámica:** Problemas secuenciales (decisiones en etapas).
### CSP (Constraint Satisfaction Problem)
Un problema de satisfacción de restricciones es un modelo matemático usado en inteligencia artificial y optimización. Un CSP se define por:
- **Conjunto de variables** $X = \{x_1,x_2,...,x_n\}$
- **Dominio de valores posibles** para cada variable.
- **Restricciones** que limitan las combinaciones permitidas.
El objetivo de este tipo de problemas no es necesariamente optimizar, sino que **encontrar una asignación de valores a las variables que satisfaga todas las restricciones**.
### Ejemplo
Un clásico ejemplo para este tipo de problemas es el **coloreo de grafos**, donde:
- Variables: Colores de cada país en un mapa.
- Dominios: {Rojo, Verde, Azul}.
- Restricciones: Nodos vecinos no pueden compartir color.
## CSOP (Constraint Satisfaction Optimization Problem)
Un CSOP es una extensión de los CSP. Mientras que para un CSP basta con **satisfacer las restricciones**, en un CSOP también **se busca optimizar una función objetivo**. De manera más resumida:
- **CSP** = Cumplir condiciones (¿hay solución factible?).
- **CSOP** = Cumplir condiciones y encontrar la mejor solución posible según un criterio.
### Ejemplo
Encontrar una ruta óptima para minimizar el costo total de transporte.
- Variables: Ruta de camiones.
- Restricciones: Cada cliente debe ser visitado una vez, no exceder la capacidad del camión.
- Función objetivo: Minimizar el costo total de transporte.
## Supuestos de programación lineal
Para que un problema pueda resolverse mediante programación lineal, deben cumplirse ciertos supuestos:
1. **Proporcionalidad:** La contribución de cada variable en la función objetivo y restricciones es proporcional a su valor (ej: 1 unidad produce el doble que 0.5 unidades).
2. **Aditividad:** No existen efectos de interacción entre variables; el efecto total es la suma de los parciales.
3. **Divisibilidad:** Las variables pueden tomar valores fraccionarios (ej: producir 2.5 toneladas).
4. **Certidumbre:** Los coeficientes de la función objetivo y las restricciones son conocidas con certeza y no cambian.
5. **Linealidad:** Tanto la función objetivo como las restricciones deben ser expresadas como funciones lineales de las variables.