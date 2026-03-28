# 🎙️ Chapter 3 — User Input

> **Book:** Python for AI | **Chapter:** 3 of 14 | **Level:** 🟢 Beginner

---

## 🔄 Quick Recap

In Chapter 2 you learned:
- What variables are and how to create them
- The 4 data types — `str`, `int`, `float`, `bool`
- How to use f-strings to insert variables into text
- How to convert between types

Now let's make Python **talk to the user** — this is where programs start feeling alive!

---

## 🤔 What is User Input?

So far, everything in your programs was written by **you** — the programmer.

But what about programs that **ask questions**?

- A chatbot asks: *"What is your name?"*
- A voice robot asks: *"What would you like to know?"*
- A calculator asks: *"Enter a number:"*

This is called **user input** — the program waits, the user types something, and Python stores it in a variable.

---

## ✍️ The `input()` Function

`input()` is how Python asks the user a question.

```python
name = input("What is your name? ")
print(f"Hello, {name}!")
```

Run it and Python will wait:

```
What is your name? Aagney
Hello, Aagney!
```

How it works:

```
input("Question here")
  ↓
Python prints the question
  ↓
Python WAITS for the user to type and press Enter
  ↓
Whatever they typed is stored in the variable
```

> 💡 Notice the **space before the closing quote** in `"What is your name? "` — this adds a space between the question and where the user types. Always do this — it looks much cleaner!

---

## ⚠️ Important: Input Always Returns a String

This is the **most common mistake** beginners make.

Whatever the user types — even if it's a number — Python stores it as a **string**.

```python
age = input("How old are you? ")
print(type(age))   # <class 'str'> ← it's a string, not a number!
```

So if you try to do math with it:

```python
age = input("How old are you? ")
next_year = age + 1   # ❌ CRASH! Cannot add string + number
```

You must **convert it first**:

```python
age = int(input("How old are you? "))
next_year = age + 1   # ✅ Works!
print(f"Next year you will be {next_year}")
```

---

## 🔢 Getting Number Input

For whole numbers → use `int(input(...))`

```python
score = int(input("Enter your score: "))
print(f"Your score is {score} out of 100")
print(f"You got {100 - score} wrong")
```

For decimal numbers → use `float(input(...))`

```python
temperature = float(input("Enter temperature in Celsius: "))
fahrenheit = (temperature * 9/5) + 32
print(f"{temperature}°C = {fahrenheit}°F")
```

---

## 🤖 Building Your First Chatbot

Let's put everything together and build a simple chatbot!

Create a file called `chatbot.py`:

```python
# Simple AI Chatbot — Chapter 3 Project
print("=" * 40)
print("   🤖 Welcome to RoboChat!")
print("=" * 40)
print()

# Ask for user details
name = input("What is your name? ")
age = int(input("How old are you? "))
city = input("Which city are you from? ")
favourite = input("What is your favourite subject? ")

# Calculate future age
future_age = age + 5

# Respond like a chatbot
print()
print("=" * 40)
print(f"Nice to meet you, {name}! 👋")
print(f"So you are {age} years old and from {city}.")
print(f"Interesting! You love {favourite}.")
print(f"In 5 years you will be {future_age} years old.")
print(f"Keep learning AI, {name} — you're going to be amazing! 🚀")
print("=" * 40)
```

Run it:

```
========================================
   🤖 Welcome to RoboChat!
========================================

What is your name? Aagney
How old are you? 14
Which city are you from? Vadakara
What is your favourite subject? Computer Science

========================================
Nice to meet you, Aagney! 👋
So you are 14 years old and from Vadakara.
Interesting! You love Computer Science.
In 5 years you will be 19 years old.
Keep learning AI, Aagney — you're going to be amazing! 🚀
========================================
```

🎉 **You just built your first chatbot!**

---

## 🎨 Making Output Look Nice

Good programs don't just show raw data — they make it look clean and readable.

**Trick 1 — Blank lines with `print()`**

```python
print("Line 1")
print()           # prints a blank line
print("Line 3")
```

**Trick 2 — Separator lines**

```python
print("=" * 40)   # prints: ========================================
print("-" * 20)   # prints: --------------------
print("*" * 30)   # prints: ******************************
```

**Trick 3 — Tabs with `\t`**

```python
print("Name:\tAagney")       # Name:    Aagney
print("City:\tVadakara")     # City:    Vadakara
```

**Trick 4 — New lines with `\n`**

```python
print("Line 1\nLine 2\nLine 3")
```

Output:
```
Line 1
Line 2
Line 3
```

---

## 🧮 Mini Calculator Project

Create a file called `calculator.py`:

```python
# Mini Calculator — Chapter 3 Mini Project

print("🧮 Mini Calculator")
print("-" * 25)

num1 = float(input("Enter first number: "))
num2 = float(input("Enter second number: "))

print("-" * 25)
print(f"➕ Addition:       {num1 + num2}")
print(f"➖ Subtraction:    {num1 - num2}")
print(f"✖️  Multiplication: {num1 * num2}")

# Avoid dividing by zero
if num2 != 0:
    print(f"➗ Division:       {num1 / num2:.2f}")
else:
    print("➗ Division:       Cannot divide by zero!")
```

Run it:

```
🧮 Mini Calculator
-------------------------
Enter first number: 10
Enter second number: 3
-------------------------
➕ Addition:       13.0
➖ Subtraction:    7.0
✖️  Multiplication: 30.0
➗ Division:       3.33
```

> 💡 `:.2f` inside an f-string rounds the output to 2 decimal places. Very handy for calculators and AI outputs!

---

## 🏋️ Practice Exercises

**Exercise 1 — BMI Calculator**

Build a program that:
1. Asks for the user's name, weight (kg), and height (m)
2. Calculates BMI using the formula: `BMI = weight / (height * height)`
3. Prints the result nicely

```python
name = input("Enter your name: ")
weight = float(input("Enter your weight in kg: "))
height = float(input("Enter your height in meters: "))

bmi = weight / (height * height)

print(f"\n{name}'s BMI is: {bmi:.1f}")
```

---

**Exercise 2 — Temperature Converter**

Ask the user for a temperature in Celsius and print it in both Fahrenheit and Kelvin:

- Fahrenheit = `(C × 9/5) + 32`
- Kelvin = `C + 273.15`

```python
celsius = float(input("Enter temperature in Celsius: "))

# Your calculations here
fahrenheit = 0   # fix this
kelvin = 0       # fix this

print(f"{celsius}°C = {fahrenheit}°F = {kelvin}K")
```

<details>
<summary>💡 Answer (click to reveal)</summary>

```python
celsius = float(input("Enter temperature in Celsius: "))

fahrenheit = (celsius * 9/5) + 32
kelvin = celsius + 273.15

print(f"{celsius}°C = {fahrenheit:.1f}°F = {kelvin:.2f}K")
```

</details>

---

**Exercise 3 — Fix the bug**

This program crashes. Can you find all the mistakes?

```python
name = input("What is your name?")
age = input("What is your age?")
next_birthday = age + 1
print("Hello " + name + "! Next year you will be " + next_birthday)
```

<details>
<summary>💡 Hint (click to reveal)</summary>

Two bugs:
1. `age` from `input()` is a string — convert it: `age = int(input(...))`
2. `next_birthday` is an int but you're joining it with strings — use an f-string or `str(next_birthday)`

```python
name = input("What is your name? ")
age = int(input("What is your age? "))
next_birthday = age + 1
print(f"Hello {name}! Next year you will be {next_birthday}")
```

</details>

---

## 📝 Chapter Summary

| Concept | Code | What it does |
|---------|------|--------------|
| Get text input | `name = input("Question: ")` | Stores whatever user types |
| Get whole number | `n = int(input("Number: "))` | Stores as integer |
| Get decimal number | `n = float(input("Number: "))` | Stores as float |
| Blank line | `print()` | Prints empty line |
| Separator | `print("=" * 30)` | Prints a line of `=` |
| Round in f-string | `f"{value:.2f}"` | Shows 2 decimal places |

---

## ➡️ What's Next?

In **Chapter 4**, you'll learn **If / Else Statements** — how Python makes **decisions**. This is how AI knows what to respond based on what you say!

[👉 Chapter 4 — If / Else Statements](./04-if-else.md)

---

<div align="center">

**⭐ If this helped you, star the repo!**

[← Chapter 2](./02-variables-and-types.md) | [Back to Book Index](../README.md) | [Chapter 4 →](./04-if-else.md)

</div>
