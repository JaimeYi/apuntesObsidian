Una estructura de datos es el cómo están dispuestos los datos en memoria y cómo se almacenan/representan las relaciones de los datos.
##### Dequeue
- Consecutivos en memoria
- Implícita
##### Vector dinámico
- Acceso directo a todos los elementos por posición.
##### Listas enlazadas
- Dispersos
- Explícitos -> punteros
# Tipos abstractos de datos
Colecciones de datos con comportamiento bien definido.
- Filas/Colas -> push(), pop(), front(), size() / utiliza dequeue

|         | List(Dequeue) |
| ------- | ------------- |
| push()  | O(1)          |
| pop()   | O(1)          |
| front() | O(1)          |
| size()  | O(1)          |

- Pila (Stack) -> top(), push(), pop(), size() / utiliza vector o dequeue

|        | Vector |
| ------ | ------ |
| top()  | O(1)   |
| push() | O(1)   |
| pop()  | O(1)   |
| size() | O(1)   |

- Cola de prioridad (Heap) -> front(), pop(), push(), size() / utiliza heap

|         | Vector                 | Heap     |
| ------- | ---------------------- | -------- |
| front() | O(n)                   | O(1)     |
| pop()   | O(n)                   | O(log n) |
| push()  | O(n) / O(1) amortizado | O(log n) |
| size()  | O(1)                   | O(1 )    |

Análisis amortizado: Si se sabe con anterioridad que el peor caso posible es muy raro, podemos decir que este caso puede ser **amortizado**.
- Diccionarios -> insert(), find(), delete(), modify(), size() / se implementa con tablas hash, BST rojo/negro

|          | T. Hash | Rojo/Negro |
| -------- | ------- | ---------- |
| insert() | O(1)    | O(log n)   |
| find()   | O(1)    | O(log n)   |
| delete() | O(1)    | O(log n)   |
| modify() | O(1)    | O(log n)   |
| size()   | O(1)    | O(1)       |
- Conjuntos 

|     | Unordered_map | Map |
| --- | ------------- | --- |
|     |               |     |
