# push_swap

**Ordenar una lista de números con dos pilas y el mínimo de movimientos posible.**

[English](README.md) · [Català](README.ca.md) · **Español**

`Parte del Common Core de 42 Barcelona` · `Rango 2` · `C` · `Algorithms`

---

## Descripción

El programa recibe una lista de enteros e imprime las operaciones necesarias para ordenarlos. Solo se pueden usar dos pilas (`a` y `b`) y 11 operaciones: swap (`sa`, `sb`, `ss`), push (`pa`, `pb`), rotate (`ra`, `rb`, `rr`) y reverse rotate (`rra`, `rrb`, `rrr`). El objetivo no es solo ordenar, sino hacerlo con el mínimo de movimientos.

## Qué enseña

- **Diseño de algoritmos** y complejidad: contar y reducir operaciones.
- Listas enlazadas para representar cada pila.
- Validación robusta de la entrada: valores no numéricos, desbordamiento de enteros y duplicados.
- Probar un algoritmo con entradas aleatorias y medir sus resultados.

## Cómo funciona

Las listas de 3, 4 y 5 números tienen soluciones propias escritas a mano. Para listas más grandes el programa usa un **algoritmo basado en costes** (a menudo llamado "algoritmo Turk"): los números pasan de `a` a `b`, y antes de cada movimiento calcula cuántas rotaciones necesitaría cada candidato y elige el más barato, combinando rotaciones de las dos pilas (`rr`, `rrr`) cuando se puede. Cuando solo quedan tres números en `a`, se ordenan, y los números de `b` vuelven a su posición correcta. Una rotación final pone el número más pequeño arriba del todo.

Medido con listas aleatorias (media de 5 ejecuciones): **unos 590 movimientos para 100 números** y **unos 5.100 movimientos para 500 números**. La evaluación de 42 da la nota máxima por debajo de 700 y 5.500 movimientos.

## Compilar y ejecutar

```bash
git clone https://github.com/acarranz-dev/push_swap.git
cd push_swap
make

./push_swap 3 2 5 1 4                 # prints the list of moves
./push_swap 3 2 5 1 4 | wc -l         # counts the moves

make bonus                            # builds the checker
ARG="3 2 5 1 4"; ./push_swap $ARG | ./checker_exec $ARG   # prints OK or KO
```

## Estructura del proyecto

```
push_swap/
├── src/
│   ├── parsing.c, check_list.c       # input validation: numbers, limits, duplicates
│   ├── swap.c, push.c, rotate.c, reverse_rotate.c   # the 11 allowed operations
│   ├── sort.c, sort_five.c           # small cases (3, 4 and 5 numbers)
│   ├── cost.c, move_to_a.c           # cost of each move and cheapest choice
│   └── list.c, put_node.c            # doubly linked list for each stack
├── checker/                          # bonus: verifies a list of moves
├── libft/
└── Makefile
```

---

[Más proyectos en mi perfil](https://github.com/acarranz-dev)
