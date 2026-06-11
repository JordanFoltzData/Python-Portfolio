# Trivia Quiz

A command-line True/False trivia game built in Python. The player works through a bank of computer science trivia questions one at a time, gets instant feedback after each answer, and receives a final score at the end.

I built this project to practice object-oriented programming. Instead of writing one long script, the program is split into separate classes and modules that each handle one job — the same way larger, real-world applications are structured.

## How It Works

The program is organized into four files, each with a single responsibility:

| File | Responsibility |
|------|----------------|
| `data.py` | Stores the raw question data as a list of dictionaries |
| `question_model.py` | Defines the `Question` class — a simple model holding the question text and its correct answer |
| `quiz_brain.py` | Defines the `QuizBrain` class — the engine that asks questions, checks answers, and tracks the score |
| `main.py` | Ties everything together: builds the question bank, creates the quiz, and runs the game loop |

When the program runs, `main.py` loops through the raw data and converts each dictionary into a `Question` object. Those objects are passed into a `QuizBrain`, which manages the entire quiz: it presents each question, takes the user's input, compares it against the correct answer (case-insensitive), updates the score, and reports progress after every question. A `while` loop in `main.py` keeps the quiz going until the question bank runs out.

## What I Learned

- **Classes and objects** — modeling real concepts (a question, a quiz) as classes with attributes and methods
- **Separation of concerns** — keeping data, models, and logic in separate files so each piece can change without breaking the others
- **Object state** — using attributes like `score` and `question_number` to track progress across method calls
- **Constructors** — using `__init__` to set up each object with the data it needs
- **Imports across modules** — connecting multiple files into one working program

## How to Run

1. Make sure Python 3 is installed
2. Download all four files into the same folder
3. Run the program from a terminal:

```
python main.py
```

4. Answer each question by typing `True` or `False` and pressing Enter

## Example

```
Q.1: The HTML5 standard was published in 2014. (True/False): True
You got it right!
The correct answer was: True
Your score is 1/1
```

## Possible Improvements

- Pull live questions from the Open Trivia Database API instead of a static list
- Clean up HTML entities in question text (such as `&quot;`) using Python's built-in `html` module
- Add difficulty selection and category filtering
- Validate user input so anything other than True/False prompts a retry
