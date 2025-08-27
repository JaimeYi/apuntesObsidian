Un problema de optimización con satisfacción de restricciones (CSOP) estará compuesto por **Parámetros**, **Variables**, **Restricciones** y **Función objetivo**. Con lo dicho anteriormente podemos decir que: $$CSOP = CSP+función\,\,objetivo$$.
#### Ejemplos
##### El problema de la mochila
![[Pasted image 20250812222321.png]]
Este problema consiste en ordenar de la mejor manera objetos en una mochila, con tal de ocupar el mayor espacio posible.
##### El problema de transporte
![[Pasted image 20250812222505.png]]
Este problema consiste en encontrar la mejor ruta basándose en el costo de tal manera que se satisfaga la demanda de los clientes.
##### El problema del vendedor viajero
![[Pasted image 20250812222606.png]]
Este problema consiste en, dado un conjunto de destinos, visitar todos los destinos pasando una vez por cada destino y finalizando el recorrido en el punto inicial.
#### CSOP
Dado un CSOP se define:
- Solución óptima: solución factible mejor o igual que todas las otras soluciones factibles con respecto a la función objetivo.
Dependiendo del conjunto de restricciones, un CSP puede ser:
- Factible: si por lo menos existe una solución factible.
- Infactible: si no existe ninguna solución factible.
Dependiendo del conjunto de restricciones y de la función objetivo, un CSOP factible puede tener:
- Solución óptima única: sólo una solución óptima.
- Solución óptimas múltiples: dos o más soluciones óptimas.
- Soluciones factibles no acotadas: el valor de la función objetivo puede ser mejorado indefinidamente.
Resolver un CSOP consiste en buscar la(s) solución(es) óptima(s) o probar que el CSOP es infactible.