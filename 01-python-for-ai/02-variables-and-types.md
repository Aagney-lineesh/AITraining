# 🧮 Chapter 2 — Variables and Data Types

> **Book:** Python for AI | **Chapter:** 2 of 14 | **Level:** 🟢 Beginner

---

## 🔄 Quick Recap

In Chapter 1 you learned:
- What Python is
- How to install it
- How to use `print()`

Now let's learn something even more powerful — **Variables**.

---

## 🤔 What is a Variable?

A variable is like a **box with a label** — you put something inside it and give it a name so you can use it later.

Imagine this:

```
📦 box labeled "my_name"  →  contains "Aagney"
📦 box labeled "my_age"   →  contains 14
📦 box labeled "my_score" →  contains 98.5
```

In Python, creating a variable looks like this:

```python
my_name = "Aagney"
my_age = 14
my_score = 98.5
```

Now you can use these variables anywhere in your code!

```python
my_name = "Aagney"
my_age = 14

print(my_name)   # Output: Aagney
print(my_age)    # Output: 14
```

---

## 📏 Rules for Naming Variables

Not every name is allowed. Follow these rules:

| Rule | Example |
|------|---------|
| ✅ Use letters, numbers, underscores | `my_robot`, `score1`, `ai_model` |
| ✅ Start with a letter or underscore | `name`, `_speed` |
| ❌ Cannot start with a number | ~~`1name`~~ |
| ❌ No spaces allowed | ~~`my name`~~ → use `my_name` |
| ❌ No special characters | ~~`my-robot`~~, ~~`ai@bot`~~ |
| ❌ Cannot use Python keywords | ~~`print`~~, ~~`for`~~, ~~`if`~~ |

**Good naming style** — use `snake_case` (words separated by underscores):

```python
# Good ✅
robot_speed = 10
player_score = 250
ai_response = "Hello!"

# Bad ❌
x = 10          # unclear name
RobotSpeed = 10 # works but not Python style
```

---

## 🗂️ Data Types

Every variable has a **type** — what kind of data it holds.

Python has 4 basic types you need to know:

---

### 1. 🔤 String (`str`) — Text

Strings are text. Always wrap them in quotes.

```python
name = "Aagney Lineesh"
city = "Vadakara"
greeting = 'Hello, AI world!'

print(name)     # Aagney Lineesh
print(city)     # Vadakara
```

You can join strings together using `+`:

```python
first = "Rasp"
second = "berry Pi"
full = first + second
print(full)   # RaspBerry Pi
```

You can also mix variables into text using **f-strings** (very useful!):

```python
name = "Aagney"
age = 14
print(f"My name is {name} and I am {age} years old.")
# Output: My name is Aagney and I am 14 years old.
```

> 💡 **f-string** = put `f` before the quote, then use `{}` to insert a variable. You'll use this **all the time** in AI projects!

---

### 2. 🔢 Integer (`int`) — Whole Numbers

Integers are whole numbers — no decimal point.

```python
age = 14
year = 2026
raspberry_pi_ram = 4096   # MB of RAM
num_cameras = 2

print(age + 1)    # 15
print(year - 10)  # 2016
print(4 * 5)      # 20
print(10 // 3)    # 3  (floor division — no remainder)
print(10 % 3)     # 1  (remainder only)
```

---

### 3. 🔣 Float (`float`) — Decimal Numbers

Floats are numbers with a decimal point.

```python
temperature = 36.6
battery_level = 87.5
pi = 3.14159

print(temperature)          # 36.6
print(battery_level / 100)  # 0.875
print(round(pi, 2))         # 3.14
```

> 💡 `round(number, digits)` rounds a float to a certain number of decimal places. Super useful in AI when dealing with percentages and probabilities!

---

### 4. ✅ Boolean (`bool`) — True or False

Booleans can only be **True** or **False**. They are used to make decisions in code.

```python
is_robot_on = True
is_charging = False
camera_detected = True

print(is_robot_on)    # True
print(is_charging)    # False
```

> You'll use booleans constantly in AI — for example: `object_detected = True` or `voice_heard = False`

---

## 🔍 Checking the Type of a Variable

Not sure what type a variable is? Use `type()`:

```python
name = "Aagney"
age = 14
score = 98.5
is_on = True

print(type(name))    # <class 'str'>
print(type(age))     # <class 'int'>
print(type(score))   # <class 'float'>
print(type(is_on))   # <class 'bool'>
```

---

## 🔄 Changing Types (Type Conversion)

Sometimes you need to convert one type to another:

```python
# String to Integer
number_text = "42"
number = int(number_text)
print(number + 8)   # 50

# Integer to String
age = 14
message = "I am " + str(age) + " years old"
print(message)   # I am 14 years old

# Integer to Float
x = 5
print(float(x))   # 5.0

# Float to Integer (removes decimal)
y = 9.99
print(int(y))   # 9
```

> ⚠️ If you try `"hello" + 5` Python will crash! You must convert first: `"hello" + str(5)`

---

## 🤖 Real AI Example

Here's how variables are used in a real AI robot program:

```python
# Robot settings
robot_name = "RoboBuddy"
robot_version = 2.1
is_listening = True
battery_percent = 85

# Display status
print(f"🤖 Robot: {robot_name} v{robot_version}")
print(f"🔋 Battery: {battery_percent}%")
print(f"🎙️ Listening: {is_listening}")
```

Output:

```
🤖 Robot: RoboBuddy v2.1
🔋 Battery: 85%
🎙️ Listening: True
```

---

## 🏋️ Practice Exercises

**Exercise 1 — Your robot profile**

Create variables for your own AI robot and print them nicely:

```python
robot_name = ""       # give your robot a name
robot_color = ""      # what color is it?
robot_speed = 0       # speed in km/h
is_voice_enabled = True

# Print them using f-strings
print(f"Robot name: {robot_name}")
# add more prints below...
```

---

**Exercise 2 — Type conversion challenge**

Fix this broken code:

```python
speed = "120"
time = 2
distance = speed * time   # ❌ This will crash!
print(f"Distance: {distance} km")
```

<details>
<summary>💡 Hint (click to reveal)</summary>

Convert `speed` from string to integer first:

```python
speed = int("120")
time = 2
distance = speed * time   # ✅ Now works!
print(f"Distance: {distance} km")
# Output: Distance: 240 km
```

</details>

---

**Exercise 3 — Predict the output**

What will Python print? Try to guess before running:

```python
a = 10
b = 3
print(a + b)
print(a - b)
print(a * b)
print(a / b)
print(a // b)
print(a % b)
```

---

## 📝 Chapter Summary

| Type | Keyword | Example | Used for |
|------|---------|---------|----------|
| Text | `str` | `"Aagney"` | Names, words, sentences |
| Whole number | `int` | `14` | Age, count, year |
| Decimal | `float` | `98.5` | Temperature, battery, scores |
| True/False | `bool` | `True` | On/off, yes/no, detected |

| Trick | Code |
|-------|------|
| Check type | `type(variable)` |
| Insert in text | `f"Hello {name}"` |
| Convert to int | `int(x)` |
| Convert to str | `str(x)` |
| Convert to float | `float(x)` |

---

## ➡️ What's Next?

In **Chapter 3**, you'll learn **Input from the user** — how to make Python ask the user a question and store their answer in a variable. This is how chatbots and voice robots start!

[👉 Chapter 3 — User Input](./03-user-input.md)

---

<div align="center">

**⭐ If this helped you, star the repo!**

[← Chapter 1](./01-getting-started.md) | [Back to Book Index](../README.md) | [Chapter 3 →](./03-user-input.md)

</div>
