# Fuzzy CA — Cellular Automaton with Fuzzy Logic

A cellular automaton where cells don't just vote yes or no — they're allowed to be uncertain about it. Combines fuzzy logic with grid-based simulation to model opinion dynamics and consensus-building.

## What it does

Creates an interactive grid where each cell holds a position: **Yes** (+1), **No** (-1), or **Abstain** (0). Inner cells compute their position using fuzzy membership functions based on their neighbors' values — meaning they can partially belong to multiple categories before committing to a final decision.

Each iteration:
1. Inner cells calculate fuzzy membership values from their Moore neighborhood (8 surrounding cells)
2. Three membership functions (yes, abstain, no) assign degrees of belonging
3. Visualization shows proportional membership as stacked colored bars
4. On click: defuzzification converts fuzzy values to crisp decisions (highest membership wins)
5. New crisp values feed into the next iteration

It's a model for how consensus (or polarization) can emerge from local interactions under uncertainty.

## Running it

```bash
pip install graphics.py
python main.py
```

A window opens with the grid. Click to advance through simulation steps. The UI is in German (it was a German university project, after all).

**Note:** Uses `ctypes.windll` for dialog boxes — Windows only as written.

## Visualization

- **Green** — Yes (+1)
- **Gold** — Abstain (0)
- **Orange-Red** — No (-1)
- **Fuzzy cells** show three stacked rectangles proportional to membership degrees
- **Crisp cells** show a single color with value label

## How the fuzzy logic works

Three membership functions map neighbor averages to category degrees:

- **yes_function:** Linear ramp from 0 to 1 (positive values)
- **abst_function:** Triangular peak centered at 0 (neutral values)
- **no_function:** Triangular membership for negative values

The grid uses toroidal wrapping — edges connect to opposite edges — so there are no boundary effects.

## Project structure

```
main.py           — Simulation loop and user interaction
Cell.py           — Cell class (fuzzy and crisp variants)
Grid.py           — Grid management and fuzzy logic processing
Inference.py      — Fuzzy membership function definitions
GraphicsUnit.py   — Rendering with Zelle's graphics library
config.py         — Grid dimensions, cell proportions, window settings
```

## Dependencies

- Python 3.x
- [graphics.py](https://mcsp.wartburg.edu/zelle/python/) (Zelle's graphics library)
- Windows OS (for dialog boxes)

## Context

Graduate coursework project (University of Bamberg) exploring the intersection of fuzzy logic and cellular automata. Classic CA models force binary states — this project explores what happens when you let cells express uncertainty before making decisions.
