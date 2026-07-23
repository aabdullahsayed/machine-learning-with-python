

## 2. Loops & Control Flow

### While Loops

**What it is:** A loop that keeps running *as long as* a condition is `True`.

**Why we need it:** Sometimes you don't know in advance how many times you need to repeat something — you just know the *condition* under which you should stop. For example, "keep asking the user for input until they type 'quit'." A `while` loop handles this open-ended repetition; without it you'd have to guess a fixed number of repetitions, which doesn't work when the count is unknown ahead of time.

**Example:**
```python
count = 0
while count < 5:
    print("Count is:", count)
    count += 1
print("Done!")
```

**Exercises:**
1. Write a `while` loop that prints numbers from 10 down to 1.
2. Write a program that keeps asking the user to enter a password until they type the correct one ("open123").
3. Use a `while` loop to sum numbers entered by the user until they enter `0`.

---

### For Loops

**What it is:** A loop that iterates over a sequence (list, string, range, etc.) a known/finite number of times, once per item.

**Why we need it:** When you already know what you're iterating over (a list of names, a range of numbers), a `for` loop is cleaner and less error-prone than a `while` loop — you don't need to manually manage a counter or worry about forgetting to increment it (which can cause infinite loops).

**Example:**
```python
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print("I like", fruit)

for i in range(5):
    print("Number:", i)
```

**Exercises:**
1. Loop through a list of 5 cities and print each one with its index (e.g., "1: Dhaka").
2. Use a `for` loop with `range()` to print all even numbers between 1 and 20.
3. Given a string, use a `for` loop to count how many vowels it contains.

---

### Nested Loops

**What it is:** A loop placed inside another loop. The inner loop runs completely for every single iteration of the outer loop.

**Why we need it:** Many real problems are naturally two-dimensional — grids, tables, matrices, pairs of items to compare. A single loop can only move through one dimension at a time; nesting loops lets you move through rows *and* columns, or generate every combination of two lists.

**Example:**
```python
for i in range(1, 4):
    for j in range(1, 4):
        print(f"{i} x {j} = {i*j}")
```

**Exercises:**
1. Print a multiplication table (1 to 5) using nested loops.
2. Print a triangle pattern of stars:
   ```
   *
   **
   ***
   ****
   ```
3. Given two lists `colors = ["red", "blue"]` and `sizes = ["S", "M", "L"]`, print every color-size combination.

---

### Match-Case Statements

**What it is:** Python's version of a `switch` statement (introduced in Python 3.10). It compares a value against several possible patterns and runs the code for the first match.

**Why we need it:** When you have many `if/elif/elif/...` checks against the *same* variable, the code becomes long and repetitive. `match-case` makes this kind of multi-way branching more readable, and it can also match patterns (like structure of data), not just plain values.

**Example:**
```python
def get_day_type(day):
    match day:
        case "Saturday" | "Sunday":
            return "Weekend"
        case "Monday" | "Tuesday" | "Wednesday" | "Thursday" | "Friday":
            return "Weekday"
        case _:
            return "Not a valid day"

print(get_day_type("Sunday"))
```

**Exercises:**
1. Write a `match-case` that takes a number (1, 2, or 3) and returns "One", "Two", "Three", or "Unknown".
2. Write a simple calculator using `match-case` that takes an operator (`+`, `-`, `*`, `/`) and two numbers, and returns the result.
3. Write a `match-case` that takes an HTTP status code (200, 404, 500) and prints a matching message like "OK", "Not Found", or "Server Error".

---

## 3. Collections & Data Structures

### Lists, Sets, and Tuples

**What they are:**
- **List** `[]` — ordered, changeable (mutable), allows duplicates.
- **Tuple** `()` — ordered, unchangeable (immutable), allows duplicates.
- **Set** `{}` — unordered, unique items only (no duplicates).

**Why we need them:** Different problems need different guarantees. Use a **list** when order matters and you'll modify it. Use a **tuple** when data shouldn't change (like coordinates `(x, y)`) — this also makes it safer to pass around and slightly faster. Use a **set** when you need to guarantee uniqueness or quickly check membership, like removing duplicate entries.

**Example:**
```python
my_list = [1, 2, 2, 3]      # list: keeps duplicates, ordered
my_tuple = (10, 20)         # tuple: fixed, can't be changed
my_set = {1, 2, 2, 3}       # set: automatically removes duplicate -> {1, 2, 3}

print(my_list, my_tuple, my_set)
```

**Exercises:**
1. Create a list of 5 favorite movies, then add one more using `.append()`.
2. Create a tuple representing a point `(x, y)` and try to change one value — observe the error, then explain why it happened.
3. Given a list `[1, 2, 2, 3, 4, 4, 5]`, convert it to a set to remove duplicates, then convert it back to a list.

---

### 2D Collections

**What it is:** A collection (usually a list) whose items are themselves collections — like a list of lists. This is used to represent grids, tables, or matrices.

**Why we need it:** Some data is naturally two-dimensional — a spreadsheet, a tic-tac-toe board, a seating chart. A flat 1D list can't represent "row and column" position directly; a 2D list lets you access data with `grid[row][col]`.

**Example:**
```python
grid = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
print(grid[1][2])  # row 1, column 2 -> 6

for row in grid:
    for value in row:
        print(value, end=" ")
    print()
```

**Exercises:**
1. Create a 3x3 tic-tac-toe board (filled with `"-"`) and print it row by row.
2. Write code that finds and prints the sum of all numbers in a 2D list.
3. Given a 2D list representing a grid, write code to print its transpose (rows become columns).

---

### Dictionaries

**What it is:** A collection of `key: value` pairs. You look up a value using its key instead of a numeric index.

**Why we need it:** Lists are great when position matters, but often you want to look things up by *name* — like a phone book (name → number) or a student record (field → value). Searching a list for a matching item is slow (you'd loop through it); a dictionary gives near-instant lookup by key.

**Example:**
```python
student = {
    "name": "Ayesha",
    "age": 20,
    "major": "CS"
}
print(student["name"])
student["age"] = 21  # update value
```

**Exercises:**
1. Create a dictionary of 3 countries and their capitals, then print each capital using a loop over `.items()`.
2. Write a program that counts how many times each word appears in a sentence, storing results in a dictionary.
3. Given a dictionary of product names and prices, write code to find the most expensive product.

---

### Iterables

**What it is:** Any object you can loop over one item at a time (lists, tuples, sets, dictionaries, strings, ranges, files, etc.). Anything usable in a `for` loop is an iterable.

**Why we need it:** It's a unifying concept — instead of writing separate looping logic for lists vs strings vs files, Python lets any object that follows the "iterable" protocol work the same way in a `for` loop. This means the tools you learn once (like `for`, `sum()`, `list()`) work everywhere.

**Example:**
```python
text = "hello"
for char in text:       # strings are iterable
    print(char)

numbers = range(3)      # range is iterable
print(list(numbers))    # [0, 1, 2]
```

**Exercises:**
1. Loop through the characters of your name and print each one on a new line.
2. Use `sum()` directly on a `range(1, 11)` to add numbers 1 through 10 without writing a loop yourself.
3. Write a function that takes any iterable and returns the number of items in it, without using `len()`.

---

### Membership Operators

**What it is:** The `in` and `not in` operators, used to check whether a value exists inside a collection.

**Why we need it:** Without them, checking "does this list contain X?" would require writing a manual loop and comparison every time. Membership operators make this a simple, readable one-line check.

**Example:**
```python
fruits = ["apple", "banana", "cherry"]

print("apple" in fruits)       # True
print("mango" not in fruits)   # True
```

**Exercises:**
1. Check if the number `7` exists in a list of numbers from 1 to 10, and print a message accordingly.
2. Write a program that checks if a user-entered username exists in a predefined list of "banned usernames."
3. Given a sentence, check whether the word `"Python"` appears in it (case-insensitive).

---

### List Comprehensions

**What it is:** A compact, one-line way to create a new list by transforming or filtering an existing iterable.

**Why we need it:** Building a list with a `for` loop usually takes 3+ lines (create empty list, loop, append). A list comprehension does the same thing in a single, readable line, and is often faster. It solves the "verbose loop just to build a list" problem.

**Example:**
```python
# Without comprehension
squares = []
for x in range(5):
    squares.append(x * x)

# With comprehension
squares = [x * x for x in range(5)]
print(squares)  # [0, 1, 4, 9, 16]

# With a filter condition
evens = [x for x in range(10) if x % 2 == 0]
```

**Exercises:**
1. Use a list comprehension to create a list of the first 10 cube numbers (1³, 2³, ...).
2. Given a list of words, use a list comprehension to create a new list containing only words longer than 4 letters.
3. Use a list comprehension to convert a list of Celsius temperatures into Fahrenheit.

---

## 4. Functions

### Functions

**What it is:** A named, reusable block of code that performs a specific task, optionally taking inputs and returning an output.

**Why we need it:** Without functions, you'd copy-paste the same logic everywhere it's needed — making code long and hard to maintain (fix a bug in one copy, forget the other nine). Functions let you write logic once, give it a name, and reuse it — this is the core idea behind writing clean, maintainable code (DRY: "Don't Repeat Yourself").

**Example:**
```python
def greet(name):
    return f"Hello, {name}!"

print(greet("Rafi"))
print(greet("Nadia"))
```

**Exercises:**
1. Write a function `square(n)` that returns the square of a number.
2. Write a function `is_even(n)` that returns `True` if a number is even, `False` otherwise.
3. Write a function `max_of_three(a, b, c)` that returns the largest of three numbers.

---

### Default Arguments

**What it is:** A parameter that has a pre-set value, used automatically if the caller doesn't provide one.

**Why we need it:** Often a function has a "usual" or "sensible" value for a parameter, and requiring the caller to type it every single time is repetitive. Default arguments let common cases stay short while still allowing customization when needed.

**Example:**
```python
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"

print(greet("Sara"))                 # Hello, Sara!
print(greet("Sara", "Good morning")) # Good morning, Sara!
```

**Exercises:**
1. Write a function `power(base, exponent=2)` that returns `base` raised to `exponent`, defaulting to squaring.
2. Write a function `make_coffee(size="medium")` that prints "Making a {size} coffee."
3. Write a function `book_ticket(destination, seat="economy")` and call it with and without specifying the seat.

---

### Keyword Arguments

**What it is:** Passing arguments to a function by explicitly naming the parameter (`name=value`) instead of relying on position.

**Why we need it:** When a function has many parameters, remembering their exact order is error-prone and easy to get wrong (e.g., accidentally swapping `age` and `height`). Keyword arguments make calls self-documenting and let you pass arguments in any order.

**Example:**
```python
def describe_pet(name, animal_type, age):
    print(f"{name} is a {age}-year-old {animal_type}.")

describe_pet(age=3, name="Rex", animal_type="dog")  # order doesn't matter
```

**Exercises:**
1. Write a function `build_profile(name, city, job)` and call it using keyword arguments in a mixed-up order.
2. Write a function `order_pizza(size, topping, crust)` and call it twice — once using positional arguments, once using keyword arguments.
3. Modify a function call that currently uses positional arguments (that are easy to mix up, like three numeric values) to use keyword arguments instead, and explain why it's clearer.

---

### *args & **kwargs

**What it is:**
- `*args` — collects any number of extra **positional** arguments into a tuple.
- `**kwargs` — collects any number of extra **keyword** arguments into a dictionary.

**Why we need it:** Sometimes you don't know in advance how many arguments a function should accept — like a function that sums "any number of numbers," or a logging function that accepts arbitrary named details. Without `*args`/`**kwargs`, you'd need to guess a fixed number of parameters, limiting flexibility.

**Example:**
```python
def add_all(*args):
    return sum(args)

print(add_all(1, 2, 3, 4))  # 10

def print_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_info(name="Tom", age=25)
```

**Exercises:**
1. Write a function `multiply_all(*args)` that returns the product of any number of numbers passed in.
2. Write a function `print_details(**kwargs)` that prints each keyword argument as "key -> value".
3. Write a function `combo(*args, **kwargs)` that prints both the positional arguments and the keyword arguments it received.

---

### Scope Resolution

**What it is:** The rules that determine where a variable is "visible"/accessible from — local (inside a function), enclosing (an outer function), global (module-level), and built-in (Python's own names). Often remembered as **LEGB**.

**Why we need it:** Without scope, every variable would be accessible everywhere, causing name collisions and making it hard to reason about code (a variable in one function accidentally overwriting one in another). Scope keeps variables isolated to where they're needed, and the `global`/`nonlocal` keywords give explicit, intentional ways to break out of that isolation when truly necessary.

**Example:**
```python
x = "global value"

def outer():
    x = "outer value"
    def inner():
        nonlocal x
        x = "changed by inner"
    inner()
    print(x)  # "changed by inner"

outer()
print(x)  # "global value" (unaffected)
```

**Exercises:**
1. Create a global variable `counter = 0` and a function that tries to increment it without `global` — observe the error, then fix it using the `global` keyword.
2. Write a function with a local variable of the same name as a global variable, and print both to show they're independent.
3. Write a nested function example using `nonlocal` to modify a variable in the enclosing function.

---

### Modules

**What it is:** A `.py` file containing reusable code (functions, classes, variables) that can be imported into other files using `import`.

**Why we need it:** As programs grow, keeping everything in one file becomes messy and hard to navigate. Modules let you split code into logical, reusable files (e.g., `math_utils.py`, `db.py`) and share code across multiple projects without copy-pasting.

**Example:**
```python
# file: math_utils.py
def add(a, b):
    return a + b

# file: main.py
import math_utils
print(math_utils.add(2, 3))

# or import a specific function
from math_utils import add
print(add(4, 5))
```

**Exercises:**
1. Create a module `greetings.py` with a function `say_hello(name)`, then import and use it from another file.
2. Import Python's built-in `random` module and use it to generate a random number between 1 and 100.
3. Create a module with two functions (e.g., `add` and `subtract`), then import only one of them using `from module import function_name`.

---


## Quick Reference Summary

| Topic | Core Purpose |
|---|---|
| While Loop | Repeat until a condition becomes false |
| For Loop | Repeat over a known sequence |
| Nested Loops | Handle 2D/combinatorial problems |
| Match-Case | Clean multi-way branching |
| List/Set/Tuple | Choose the right container for order/mutability/uniqueness |
| 2D Collections | Represent grids/tables |
| Dictionary | Fast lookup by key |
| Iterables | Uniform looping over any collection |
| Membership Operators | Quick "does it contain X?" checks |
| List Comprehension | Compact list-building |
| Functions | Reusable, named logic (DRY) |
| Default Arguments | Sensible defaults, less repetition |
| Keyword Arguments | Clear, order-independent calls |
| *args / **kwargs | Accept flexible/unknown numbers of arguments |
| Scope Resolution | Control variable visibility (LEGB) |
| Modules | Organize and reuse code across files |
