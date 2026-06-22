# Knight-Exchange-Puzzle

This is the reduction from a grid graph Hamiltonian path problem to the knight's tour puzzle on a chessboard with holes. The solver uses heuristic search and pruning to find Hamiltonian paths on the tranformed graph modeling the knight's moves on the chessboard.

## Overview

- `reduction.py` builds a randomized grid graph and maps each grid-cell to a 9x9 knight-board tile.
- `hamiltonian_path_tester.py` attempts to find a Hamiltonian path through a knight adjacency graph using randomized Warnsdorff-style heuristics and depth-first search with strong pruning.
- `board_to_graph.py` contains the chessboard tile patterns and utilities for converting a binary board layout to a knight-move graph.
- `build_grid_graph.py` generates randomized grid graphs with optional holes.
- `print_board.py` and `print_path.py` provide matplotlib-based visualization helpers.
- `generate_tikz_graphs.py` can convert a static adjacency list into LaTeX TikZ drawing code.

## What this project does

The code is centered on a reduction for an NP-hard problem:

1. A grid graph is generated or specified.
2. Each grid vertex is replaced by a specially designed 9x9 knight-board tile.
3. Tiles are glued together to form a larger chessboard configuration.
4. Solving the knight Hamiltonian path on that board corresponds to solving the original graph problem.

## Key scripts

### `reduction.py`

- Creates a random grid graph using `build_grid_graph.randomized_grid_graph`.
- Converts the grid graph to tile indices and maps each cell to a 9x9 chessboard pattern.
- Assembles the full board and displays it using `print_board.display_board`.

### `hamiltonian_path_tester.py`

- Contains a hard-coded knight adjacency graph for testing.
- Runs a randomized greedy Warnsdorff search over many trials.
- If the greedy phase fails, it runs a deeper DFS search with pruning:
  - isolated vertex detection
  - connectivity checks for unvisited vertices
  - neighbor ordering by onward degree
- Displays the best found path with `print_path.display_path`.

### `board_to_graph.py`

- Defines board tile patterns such as `Corner4`, `Corner3V1`, `Corner2V1`, etc.
- Converts a 2D binary board representation into a knight adjacency list.

### `build_grid_graph.py`

- Generates a grid graph with a given number of rows and columns.
- Includes edge probability and optional holes support.

### `generate_tikz_graphs.py`

- Converts an adjacency list to LaTeX TikZ code for graph visualization.

## Installation

This project requires:

- Python 3
- `matplotlib`

Install dependencies with pip:

```bash
pip install matplotlib
```

> Note: Several scripts import from `Utils.utlities`. Ensure the required utility module is available in your Python path or repository layout.

## Usage

Run the reduction step:

```bash
python3 reduction.py
```

Run the Hamiltonian path solver:

```bash
python3 hamiltonian_path_tester.py
```

Customize the solver by editing the adjacency graph, start/end nodes, or the search parameters at the top of `hamiltonian_path_tester.py`.

## Notes

- This is research/prototype code.
- The current solver is designed for a specific knight adjacency graph and may require adjustment for other boards.
- The reduction demonstrates how a graph Hamiltonian path instance can be embedded into a knight-move puzzle.

## Repository structure

- `reduction.py` — reduction from grid graphs to knight-board tilings.
- `hamiltonian_path_tester.py` — heuristic solver for knight Hamiltonian paths.
- `board_to_graph.py` — knight adjacency graph generation and tile definitions.
- `build_grid_graph.py` — randomized grid graph generator.
- `print_board.py` — board visualizer using matplotlib.
- `print_path.py` — path visualizer using matplotlib.
- `generate_tikz_graphs.py` — exports graph drawings to TikZ.
