# Damien Hirst Dot Artwork Replica

A generative art program that recreates the look of Damien Hirst's iconic spot paintings using Python's `turtle` graphics module, with a color palette pulled directly from a real Hirst artwork using Colorgram.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Requirements](#requirements)
- [How to Run](#how-to-run)
- [How It Works](#how-it-works)
- [Extracting Colors with Colorgram](#extracting-colors-with-colorgram)
- [Example Output](#example-output)
- [Code Breakdown](#code-breakdown)
- [Skills Demonstrated](#skills-demonstrated)

---

## Overview

Damien Hirst's spot paintings are made up of evenly spaced, randomly colored circles arranged in a precise grid. This program recreates that style programmatically: a turtle "draws" a 10x10 grid of dots, picking a random color for each one from a palette sampled from an actual Hirst painting.

---

## Features

- Grid layout of 100 dots (10 rows × 10 columns), evenly spaced
- Color palette of 27 RGB values extracted from a real Damien Hirst spot painting
- Randomized color selection for every dot using `random.choice()`
- Fast, clean rendering — no visible turtle cursor or connecting lines between dots

---

## Requirements

- Python 3.x
- Built-in `turtle` and `random` modules (no installation needed)
- `colorgram.py` — only needed if you want to extract your own color palette from an image instead of using the one already in the script:
  ```bash
  pip install colorgram.py
  ```

---

## How to Run

1. Make sure Python 3 is installed on your machine.
2. Save the script as `dot_artwork.py`.
3. Open a terminal and navigate to the file location.
4. Run the program:
   ```bash
   python dot_artwork.py
   ```
5. A turtle graphics window will open and draw the 10x10 dot grid automatically. Click anywhere in the window to close it.

---

## How It Works

1. `turtle_module.colormode(255)` switches turtle's color system from 0–1 floats to standard 0–255 RGB values, so the colors pulled from Colorgram can be used as-is.
2. The turtle (`tim`) is set to hide its cursor, lift its pen, and move at the fastest speed, since only dots need to be drawn — not lines.
3. `setheading(225)` and `forward(300)` move `tim` diagonally to the bottom-left starting corner of the grid without drawing anything, since the pen is up.
4. A `for` loop runs 100 times. On each pass, it:
   - Draws one dot, sized 18, in a random color chosen from `color_list` with `random.choice()`.
   - Moves forward 50 pixels to line up the next dot in the row.
5. Every 10th dot — checked with `dot_count % 10 == 0` — the row is finished, so the turtle repositions for the next row: turn up and move 50 pixels down (row spacing), turn around and travel back 500 pixels (return to the left edge), then reset heading to face right again.
6. The result is a 10×10 grid of randomly colored, evenly spaced dots that mimics the structure of a Damien Hirst spot painting.

---

## Extracting Colors with Colorgram

Instead of picking colors manually, the RGB values in `color_list` were sampled directly from a photo of a real Damien Hirst spot painting using the `colorgram.py` library:

```python
import colorgram

colors = colorgram.extract('hirst_artwork.jpg', 30)

for color in colors:
    print(color.rgb)
```

`colorgram.extract()` analyzes an image and returns its most dominant colors as RGB tuples, ranked by how much of the image each one covers. Those RGB values were then copied into `color_list`, so the replica's palette matches the original artwork.

---

## Example Output

Running the script opens a turtle graphics window and draws a 10×10 grid of colored dots, each 18px wide and spaced 50px apart — a close visual match to Damien Hirst's spot painting style, using colors sampled from the real artwork rather than arbitrary ones.

---


## Skills Demonstrated

| Concept | Usage |
|---|---|
| `import random` / `import turtle` | Importing and aliasing built-in Python modules |
| `turtle.colormode(255)` | Configuring RGB color mode for accurate, real-world colors |
| `random.choice()` | Selecting a random color for each dot from a list |
| `for` loops with `range()` | Repeating dot-drawing a fixed number of times |
| Modulo operator (`%`) | Detecting every 10th dot to trigger a new row |
| `tim.setheading()` / `tim.forward()` | Directional movement and coordinate positioning with turtle graphics |
| Conditional logic (`if`) | Row-wrapping logic nested inside a loop |
| `colorgram.py` (external library) | Extracting a real-world color palette from an image file |
| Turtle graphics (`.dot()`, `.penup()`, `.hideturtle()`) | Rendering shapes without visible cursor or connecting lines |

---

## Note

This project is a generative art piece rather than a task-based script — it focuses on translating a real artwork's grid structure and color palette into code using loops, conditionals, and the `turtle` graphics library.

---
