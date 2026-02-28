# Dynamic Pathfinding Agent

A grid-based pathfinding visualizer built with **Python + Tkinter** (no external dependencies required).

---

## Features

| Feature | Details |
|---|---|
| Algorithms | A\* Search, Greedy Best-First Search (GBFS) |
| Heuristics | Manhattan Distance, Euclidean Distance |
| Visualization | Animated frontier (yellow), visited (blue), path (green), agent (purple) |
| Grid Sizing | User-defined rows × columns (5–50 rows, 5–70 cols) |
| Map Editor | Click/drag to place walls, set Start/Goal, erase |
| Maze Generator | Random maze with adjustable obstacle density |
| Dynamic Mode | Random obstacles spawn mid-traversal; agent re-plans automatically |
| Metrics | Nodes Visited, Path Cost, Execution Time (ms), Replans |

---

## Requirements

- Python 3.7 or higher
- **No external libraries needed** — uses only Python's built-in `tkinter`

---

## How to Run

```bash
python pathfinding_agent.py
```

---

## GUI Controls

### Row 0 — Grid Size
| Control | Description |
|---|---|
| Rows spinbox | Set number of rows (5–50) |
| Cols spinbox | Set number of columns (5–70) |
| Apply Grid Size | Resize the grid (clears current map) |

### Row 1 — Algorithm & Tools
| Control | Description |
|---|---|
| A\* / GBFS | Select search algorithm |
| Manhattan / Euclidean | Select heuristic function |
| Wall / Start / Goal / Erase | Select the editing tool for clicking on the grid |

### Row 2 — Actions
| Control | Description |
|---|---|
| Generate Maze | Randomly fill the grid with walls at the set density |
| Clear Grid | Remove all walls, reset start/goal |
| RUN | Run the selected algorithm and animate the result |
| STOP | Stop any running animation |
| Density slider | Control the % of cells that become walls during maze generation |
| Dynamic Obstacles | Enable random wall spawning while agent walks the path |
| Spawn % slider | Probability per step that a new obstacle will spawn |

---

## Color Legend

| Color | Meaning |
|---|---|
| 🟢 Green (bright) | Start node |
| 🔴 Red | Goal node |
| ⬛ Dark gray | Wall |
| 🟡 Yellow | Frontier — nodes currently in the open/priority queue |
| 🔵 Blue | Visited — nodes that have been expanded |
| 🟢 Green (medium) | Final path from Start to Goal |
| 🟣 Purple | Agent moving along the path |

---

## Algorithm Details

### A\* Search
- **Evaluation function:** `f(n) = g(n) + h(n)`
- `g(n)` = actual cost from start to node n (number of steps)
- `h(n)` = heuristic estimate from n to goal
- Guarantees the **shortest path** when the heuristic is admissible
- Explores fewer nodes than GBFS in most cases with a good heuristic

### Greedy Best-First Search (GBFS)
- **Evaluation function:** `f(n) = h(n)` (heuristic only, no path cost)
- Always expands the node that *looks* closest to the goal
- **Not guaranteed to find the shortest path**
- Typically faster than A\* but may explore suboptimal routes

### Heuristics
| Heuristic | Formula | Best for |
|---|---|---|
| Manhattan | `\|r1 - r2\| + \|c1 - c2\|` | 4-directional grids (used here) |
| Euclidean | `sqrt((r1-r2)^2 + (c1-c2)^2)` | Diagonal/free movement |

---

## Dynamic Mode

When **Dynamic Obstacles** is checked:
1. As the agent walks the path step-by-step, new walls may randomly spawn
2. If a new wall lands on the **remaining path**, the agent immediately re-plans from its current position
3. If no new path is found, the agent stops and reports "No path after obstacle"
4. The **Replans** counter tracks how many times re-planning was triggered

---


## Metrics Dashboard

| Metric | Description |
|---|---|
| Nodes Visited | Total number of nodes expanded during search |
| Path Cost | Number of steps in the final path (start to goal) |
| Exec Time (ms) | Time taken by the search algorithm in milliseconds |
| Replans | Number of times the agent re-planned due to dynamic obstacles |

---

## Tips

- For a **best case** with GBFS: use a clear open grid with Start and Goal in a straight line
- For a **worst case** with GBFS: place a U-shaped wall trap near the goal — GBFS may get stuck exploring the wrong side
- A\* always finds the optimal path but may be slightly slower in dense mazes
- Use **Density 20–30%** for interesting mazes that still have a valid path
- Use **Density 50–60%** for hard/worst-case scenarios

---

## Author

Eshal Hussain  
