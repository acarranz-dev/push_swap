# push_swap

**Ordenar una llista de números amb dues piles i el mínim de moviments possible.**

[English](README.md) · **Català** · [Español](README.es.md)

`Part del Common Core de 42 Barcelona` · `Rang 2` · `C` · `Algorithms`

---

## Descripció

El programa rep una llista d'enters i imprimeix les operacions necessàries per ordenar-los. Només es poden fer servir dues piles (`a` i `b`) i 11 operacions: swap (`sa`, `sb`, `ss`), push (`pa`, `pb`), rotate (`ra`, `rb`, `rr`) i reverse rotate (`rra`, `rrb`, `rrr`). L'objectiu no és només ordenar, sinó fer-ho amb el mínim de moviments.

## Què ensenya

- **Disseny d'algorismes** i complexitat: comptar i reduir operacions.
- Llistes enllaçades per representar cada pila.
- Validació robusta de l'entrada: valors no numèrics, desbordament d'enters i duplicats.
- Provar un algorisme amb entrades aleatòries i mesurar-ne els resultats.

## Com funciona

Les llistes de 3, 4 i 5 números tenen solucions pròpies escrites a mà. Per a llistes més grans el programa fa servir un **algorisme basat en costos** (sovint anomenat "algorisme Turk"): els números passen de `a` a `b`, i abans de cada moviment calcula quantes rotacions necessitaria cada candidat i tria el més barat, combinant rotacions de les dues piles (`rr`, `rrr`) quan es pot. Quan només queden tres números a `a`, s'ordenen, i els números de `b` tornen a la seva posició correcta. Una rotació final posa el número més petit a dalt de tot.

Mesurat amb llistes aleatòries (mitjana de 5 execucions): **uns 590 moviments per a 100 números** i **uns 5.100 moviments per a 500 números**. L'avaluació de 42 dona la nota màxima per sota de 700 i 5.500 moviments.

## Compilar i executar

```bash
git clone https://github.com/acarranz-dev/push_swap.git
cd push_swap
make

./push_swap 3 2 5 1 4                 # prints the list of moves
./push_swap 3 2 5 1 4 | wc -l         # counts the moves

make bonus                            # builds the checker
ARG="3 2 5 1 4"; ./push_swap $ARG | ./checker_exec $ARG   # prints OK or KO
```

## Estructura del projecte

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

[Més projectes al meu perfil](https://github.com/acarranz-dev)
