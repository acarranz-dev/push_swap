# push_swap

**Sorting a list of numbers with two stacks and the smallest possible number of moves.**

**English** · [Català](README.ca.md) · [Español](README.es.md)

`Part of the 42 Barcelona Common Core` · `Rank 2` · `C` · `Algorithms`

---

## Description

The program receives a list of integers and prints the operations needed to sort them. Only two stacks (`a` and `b`) and 11 operations are allowed: swap (`sa`, `sb`, `ss`), push (`pa`, `pb`), rotate (`ra`, `rb`, `rr`) and reverse rotate (`rra`, `rrb`, `rrr`). The goal is not only to sort, but to do it with as few moves as possible.

## What it teaches

- **Algorithm design** and complexity: counting and minimising operations.
- Linked lists to represent each stack.
- Robust input parsing: non-numeric values, integer overflow and duplicates.
- Testing an algorithm with random inputs and measuring its results.

## How it works

Lists of 3, 4 and 5 numbers have their own hand-written solutions. For bigger lists the program uses a **cost-based algorithm** (often called the "Turk algorithm"): numbers are pushed from `a` to `b`, and before each push it calculates how many rotations each candidate would need and picks the cheapest one, combining rotations of both stacks (`rr`, `rrr`) when possible. When only three numbers remain in `a`, they are sorted, and the numbers in `b` are pushed back to their correct position. A final rotation puts the smallest number on top.

Measured on random lists (average of 5 runs): **about 590 moves for 100 numbers** and **about 5,100 moves for 500 numbers**. The 42 evaluation gives the maximum score below 700 and 5,500 moves.

## Build and run

```bash
git clone https://github.com/acarranz-dev/push_swap.git
cd push_swap
make

./push_swap 3 2 5 1 4                 # prints the list of moves
./push_swap 3 2 5 1 4 | wc -l         # counts the moves

make bonus                            # builds the checker
ARG="3 2 5 1 4"; ./push_swap $ARG | ./checker_exec $ARG   # prints OK or KO
```

## Project structure

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

[More projects on my profile](https://github.com/acarranz-dev)
