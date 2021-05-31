# `µSolver`: Heuristic cluster editing solver 

[PACE Challenge 2021](https://pacechallenge.org/2021/) submission for the Heuristic Track, by Gabriel Bathie, Ulysse Prieto, Valentin Bartier, Nicolas Bousquet, Marc Heinrich, and Théo Pierron.

## Dependencies, compilation and usage

This program requires `c++17`, `g++ 9.0` or higher and a not too old version of `make`. 
The only library that is uses is the STL.

To compile `mu_solver`, simply type `make`. The resulting executable is named `main`.
You can then use it as follows:

```bash
./main < graph_file.gr
```

Here, `graph_file.gr` contains the description of a graph, given in the [DIMACS-like `.gr` format](https://pacechallenge.org/2021/tracks/#input-format).  
The program then runs until it receives a `SIGTERM` or `SIGKILL` (CTRL+C) signal. When it terminates, it prints within a few seconds on the standard output the best cluster editing that it found.

## Description of the algorithm

First, our program uses four different kernelization rules that are rather efficient on sparse instances: they delete more that 1 million edges on the last two instances.

Then local search using bfs moves.

We also implemented in `fast_rng.h` a custom (pseudo) random number generator based on [Xorshift](https://en.wikipedia.org/wiki/Xorshift), which is around twice as fast as `std::minstd_rand`, and much faster than `std::mt19937`. As our application does not depend crucially on the quality of the generated numbers, this yields a performance improvement.