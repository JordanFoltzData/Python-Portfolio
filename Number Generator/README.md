# Number Guessing Game

A terminal-based number guessing game built in Python. The computer picks a random number between 1 and 100, and the player tries to guess it within a limited number of attempts based on the difficulty they choose.

---

## Table of Contents

- [Overview](#overview)
- [How to Play](#how-to-play)
- [Features](#features)
- [How It Works](#how-it-works)
- [A Note on Scope](#a-note-on-scope)
- [Skills Demonstrated](#skills-demonstrated)

---

## Overview

This is a classic number guessing game where the player competes against the computer. At the start of each round, the computer randomly selects a number between 1 and 100. The player chooses a difficulty level that determines how many guesses they get, then tries to find the number using high and low hints after each attempt.

The project was built with a strong focus on clean variable scope. Game state is kept local to each round rather than relying on global variables, which keeps the code easy to follow and free of side effects.

---

## How to Play

1. Run the program in your terminal:
    ```bash
    python main.py
    ```
2. Choose a difficulty when prompted:
    - **Easy** gives you 10 guesses
    - **Hard** gives you 5 guesses
3. Enter a number between 1 and 100.
4. After each guess, the game tells you whether your guess was too high or too low.
5. Keep guessing until you find the number or run out of attempts.
6. When the round ends, choose whether to play again.

### Example
```
Welcome to the Number Guessing Game!
I'm thinking of a number between 1 and 100.
Choose a difficulty. Type 'easy' or 'hard': easy

You have 10 guesses remaining.
Make a guess: 50
Too high. Guess again.

You have 9 guesses remaining.
Make a guess: 25
Too low. Guess again.

You have 8 guesses remaining.
Make a guess: 37
You got it! The answer was 37.

Play again? Type 'y' or anything else to quit:
```

---

## Features

- Random number selection between 1 and 100 every round
- Two difficulty levels that control the number of allowed guesses
- High and low hints after each incorrect guess
- Clear win and loss messages
- Play again option that resets the game cleanly between rounds
- Difficulty constants defined at the top for easy adjustment

---

## How It Works

### Difficulty Constants
```python
EASY_LEVEL_TURNS = 10
HARD_LEVEL_TURNS = 5
```
The number of guesses for each difficulty is stored in uppercase constants at the top of the file. This follows the Python convention for values that never change and makes the difficulty easy to adjust in one place.

### Setting Difficulty
```python
def set_difficulty():
    level = input("Choose a difficulty. Type 'easy' or 'hard': ").lower()
```
The function reads the player choice and returns the matching number of turns. If the input is not recognized, it defaults to easy rather than crashing.

### Checking the Guess
```python
def check_answer(user_guess, actual_answer, turns):
    if user_guess > actual_answer:
        return turns - 1
```
This function compares the guess to the answer, prints a hint, and returns the updated number of turns. It does not modify any shared state. The caller receives the returned value and decides what to do next.

### The Game Loop
```python
def game():
    answer = random.randint(1, 100)
    turns = set_difficulty()
    guess = None

    while guess != answer:
        ...
```
All round variables live inside `game()`. The loop keeps running until the guess matches the answer or the player runs out of turns.

### Play Again
```python
def main():
    while True:
        game()
        again = input("Play again? ").lower()
        if again != "y":
            break
```
The `main()` function wraps the whole game in a loop. Each call to `game()` starts a brand new round with fresh variables.

---

## A Note on Scope

This project was designed to demonstrate good variable scope practices.

Rather than using global variables that functions reach into and modify, every value a function needs is passed in as a parameter, and every result it produces is returned. This pattern keeps each function self-contained and predictable.

All of the variables that matter to a single round live inside the `game()` function:

```python
def game():
    answer = random.randint(1, 100)   
    turns = set_difficulty()          
    guess = None                      
```

Because these are local, they are automatically destroyed when the function ends and recreated when a new round begins. This means the play again feature requires no manual resetting of game state. The local scope handles it.

The only values kept in the global scope are the difficulty constants, which are read-only and never modified. This is the appropriate use of global scope.

---

## Skills Demonstrated

| Python Concept | How It's Used |
|---|---|
| Defining functions | Logic split into `set_difficulty`, `check_answer`, `game`, `main` |
| Parameters and return values | Values passed in and returned instead of using globals |
| Local scope | Round variables kept local inside `game()` |
| Global constants | `EASY_LEVEL_TURNS` and `HARD_LEVEL_TURNS` defined once at the top |
| `while` loops | Game loop and play again loop |
| `if / elif / else` | Difficulty selection and guess comparison |
| `random.randint()` | Selecting the number to guess |
| f-strings | Formatting dynamic output messages |

---

*Built as part of a Python learning curriculum, with a focus on clean function design and proper variable scope.*
