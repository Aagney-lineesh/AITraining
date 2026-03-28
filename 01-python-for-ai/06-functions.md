# ⚙️ Chapter 6 — Functions

> **Book:** Python for AI | **Chapter:** 6 of 14 | **Level:** 🟡 Beginner → Intermediate

---

## 🔄 Quick Recap

In Chapter 5 you learned:
- `for` loops — repeat a fixed number of times
- `while` loops — repeat while a condition is True
- `break` and `continue` — control loop flow
- How real robots use `while True` to keep running

Now let's learn **Functions** — the most important concept for writing clean, powerful AI programs!

---

## 🤔 What is a Function?

Imagine you work at a juice shop. Every time someone orders mango juice you:

1. Pick the mangoes
2. Wash them
3. Peel them
4. Blend them
5. Pour and serve

Instead of doing all 5 steps from memory every single time, you write them down once as a **recipe** — and just follow it whenever needed.

That's exactly what a function is — **a block of code you write once and use as many times as you want.**

You've already been using built-in functions this whole time:

```python
print("Hello")       # print is a function
int("42")            # int is a function
input("Enter: ")     # input is a function
len("Python")        # len is a function
```

Now let's write our **own** functions!

---

## ✍️ Creating a Function

Use the `def` keyword (short for **define**):

```python
def greet():
    print("👋 Hello! I am your AI assistant!")
    print("🤖 Ready to help you today.")
```

This **defines** the function but doesn't run it yet.

To **call** (run) the function:

```python
greet()
```

Output:
```
👋 Hello! I am your AI assistant!
🤖 Ready to help you today.
```

Call it as many times as you want:

```python
greet()
greet()
greet()
```

---

## 📦 Functions with Parameters

Parameters let you **pass information into** a function:

```python
def greet(name):
    print(f"👋 Hello, {name}!")
    print(f"🤖 Welcome to AITraining, {name}!")
```

Now call it with different names:

```python
greet("Aagney")
greet("Rahul")
greet("Priya")
```

Output:
```
👋 Hello, Aagney!
🤖 Welcome to AITraining, Aagney!
👋 Hello, Rahul!
🤖 Welcome to AITraining, Rahul!
👋 Hello, Priya!
🤖 Welcome to AITraining, Priya!
```

**Multiple parameters:**

```python
def introduce(name, age, city):
    print(f"My name is {name}, I am {age} years old, from {city}.")

introduce("Aagney", 14, "Vadakara")
introduce("Rohan", 16, "Kochi")
```

---

## 🔙 Functions that Return Values

The most powerful type of function — it **calculates something and sends the result back**:

```python
def add(a, b):
    result = a + b
    return result
```

Now you can use the returned value:

```python
total = add(10, 5)
print(total)           # 15
print(add(100, 200))   # 300
print(add(7, 3) * 2)   # 20
```

**More examples:**

```python
def calculate_area(length, width):
    return length * width

def celsius_to_fahrenheit(c):
    return (c * 9/5) + 32

def is_even(number):
    return number % 2 == 0

# Use them
print(calculate_area(5, 3))              # 15
print(celsius_to_fahrenheit(100))        # 212.0
print(is_even(8))                        # True
print(is_even(7))                        # False
```

---

## 🎯 Default Parameters

You can give parameters a **default value** — used when the caller doesn't provide one:

```python
def greet(name, language="English"):
    if language == "English":
        print(f"Hello, {name}!")
    elif language == "Malayalam":
        print(f"Namaskaram, {name}!")
    elif language == "Hindi":
        print(f"Namaste, {name}!")

greet("Aagney")                    # uses default: English
greet("Aagney", "Malayalam")       # uses Malayalam
greet("Rohan", "Hindi")            # uses Hindi
```

Output:
```
Hello, Aagney!
Namaskaram, Aagney!
Namaste, Rohan!
```

---

## 🧠 Why Functions Matter in AI

Here's the same robot program — **without** and **with** functions:

**❌ Without functions — messy and repetitive:**

```python
# Check battery
battery = 75
if battery >= 80:
    print("🟢 Battery: FULL")
elif battery >= 50:
    print("🟡 Battery: GOOD")
elif battery >= 20:
    print("🟠 Battery: LOW")
else:
    print("🔴 Battery: CRITICAL")

# Later in the program... same code again!
battery = 23
if battery >= 80:
    print("🟢 Battery: FULL")
elif battery >= 50:
    print("🟡 Battery: GOOD")
elif battery >= 20:
    print("🟠 Battery: LOW")
else:
    print("🔴 Battery: CRITICAL")
```

**✅ With functions — clean and reusable:**

```python
def check_battery(battery):
    if battery >= 80:
        print("🟢 Battery: FULL")
    elif battery >= 50:
        print("🟡 Battery: GOOD")
    elif battery >= 20:
        print("🟠 Battery: LOW")
    else:
        print("🔴 Battery: CRITICAL")

# Use it anywhere, any time!
check_battery(75)
check_battery(23)
check_battery(95)
```

This is exactly how professional AI code is organized!

---

## 🤖 AI Robot Dashboard — Full Project

Let's build a complete robot status dashboard using functions!

Create `robot_dashboard.py`:

```python
# 🤖 AI Robot Dashboard — Chapter 6 Project

# ── Helper Functions ──────────────────────────

def print_header(title):
    print()
    print("=" * 45)
    print(f"  {title}")
    print("=" * 45)

def check_battery(level):
    if level >= 80:
        status = "🟢 FULL"
    elif level >= 50:
        status = "🟡 GOOD"
    elif level >= 20:
        status = "🟠 LOW"
    else:
        status = "🔴 CRITICAL"
    print(f"  Battery:     {level}%  {status}")

def check_wifi(strength):
    if strength >= 70:
        status = "📶 Strong"
    elif strength >= 40:
        status = "📶 Medium"
    else:
        status = "📶 Weak"
    print(f"  WiFi:        {strength}%  {status}")

def check_temperature(temp):
    if temp > 80:
        status = "🔥 OVERHEATING!"
    elif temp > 60:
        status = "⚠️  Warm"
    else:
        status = "✅ Normal"
    print(f"  CPU Temp:    {temp}°C  {status}")

def calculate_uptime(minutes):
    hours = minutes // 60
    mins = minutes % 60
    return f"{hours}h {mins}m"

def robot_greeting(name):
    print(f"\n  👋 Hello! I am {name}.")
    print("  🤖 All systems checked and ready.")

# ── Main Program ──────────────────────────────

print_header("🤖 AI ROBOT STATUS DASHBOARD")

robot_name = input("  Enter robot name: ")
battery   = int(input("  Battery level (%): "))
wifi      = int(input("  WiFi strength (%): "))
cpu_temp  = int(input("  CPU temperature (°C): "))
uptime_m  = int(input("  Uptime (minutes): "))

print_header("📊 SYSTEM STATUS")
check_battery(battery)
check_wifi(wifi)
check_temperature(cpu_temp)
print(f"  Uptime:      {calculate_uptime(uptime_m)}")

robot_greeting(robot_name)
print("=" * 45)
```

Run it:
```
=============================================
  🤖 AI ROBOT STATUS DASHBOARD
=============================================
  Enter robot name: RoboBuddy
  Battery level (%): 65
  WiFi strength (%): 82
  CPU temperature (°C): 55
  Uptime (minutes): 137

=============================================
  📊 SYSTEM STATUS
=============================================
  Battery:     65%  🟡 GOOD
  WiFi:        82%  📶 Strong
  CPU Temp:    55°C  ✅ Normal
  Uptime:      2h 17m

  👋 Hello! I am RoboBuddy.
  🤖 All systems checked and ready.
=============================================
```

---

## 🔍 Variable Scope — Local vs Global

Variables inside a function only exist **inside** that function:

```python
def my_function():
    x = 10        # local variable — only exists inside here
    print(x)      # works ✅

my_function()
print(x)          # ❌ ERROR! x doesn't exist outside the function
```

If you need a variable everywhere, define it **outside** all functions:

```python
robot_name = "RoboBuddy"    # global variable — exists everywhere

def greet():
    print(f"Hello from {robot_name}!")   # ✅ can read it

greet()
print(robot_name)                        # ✅ works here too
```

---

## 🏋️ Practice Exercises

**Exercise 1 — Calculator using functions**

Rewrite the Chapter 3 calculator using functions — one function for each operation:

```python
def add(a, b):
    return a + b

def subtract(a, b):
    # write this

def multiply(a, b):
    # write this

def divide(a, b):
    # write this (careful about dividing by zero!)

# Main program
num1 = float(input("Enter first number: "))
num2 = float(input("Enter second number: "))

print(f"Add:      {add(num1, num2)}")
print(f"Subtract: {subtract(num1, num2)}")
# complete the rest...
```

---

**Exercise 2 — Grade function**

Write a function `get_grade(score)` that returns the grade letter:

```python
def get_grade(score):
    # return "A", "B", "C", "D" or "F"
    pass

# Test it
print(get_grade(95))   # A
print(get_grade(82))   # B
print(get_grade(71))   # C
print(get_grade(63))   # D
print(get_grade(45))   # F
```

<details>
<summary>💡 Answer (click to reveal)</summary>

```python
def get_grade(score):
    if score >= 90:
        return "A"
    elif score >= 80:
        return "B"
    elif score >= 70:
        return "C"
    elif score >= 60:
        return "D"
    else:
        return "F"
```

</details>

---

**Exercise 3 — Fix the bug**

What is wrong with this code?

```python
def multiply(a, b):
    answer = a * b

result = multiply(6, 7)
print(result)   # prints: None
```

<details>
<summary>💡 Hint (click to reveal)</summary>

The function calculates the answer but never **returns** it! Add `return answer`:

```python
def multiply(a, b):
    answer = a * b
    return answer       # ✅ now it sends the result back

result = multiply(6, 7)
print(result)           # 42
```

</details>

---

## 📝 Chapter Summary

| Concept | Code | What it does |
|---------|------|--------------|
| Define function | `def my_func():` | Creates a reusable block of code |
| Call function | `my_func()` | Runs the function |
| With parameter | `def greet(name):` | Accepts input |
| Return value | `return result` | Sends result back to caller |
| Default value | `def greet(name="AI"):` | Used when argument not given |
| Local variable | Inside a function | Only exists inside that function |
| Global variable | Outside all functions | Available everywhere |

---

## ➡️ What's Next?

In **Chapter 7**, you'll learn **Lists and Dictionaries** — how Python stores and organizes collections of data. This is fundamental to AI — every dataset, every model result, every sensor reading is stored in lists and dictionaries!

[👉 Chapter 7 — Lists and Dictionaries](./07-lists-and-dicts.md)

---

<div align="center">

**Progress — Book 1: Python for AI**

`✅ Ch1` `✅ Ch2` `✅ Ch3` `✅ Ch4` `✅ Ch5` `✅ Ch6` `⬜ Ch7` `⬜ Ch8` `⬜ Ch9` `⬜ Ch10` `⬜ Ch11` `⬜ Ch12` `⬜ Ch13` `⬜ Ch14`

---

**⭐ If this helped you, star the repo!**

[← Chapter 5](./05-loops.md) | [Back to Book Index](../README.md) | [Chapter 7 →](./07-lists-and-dicts.md)

</div>
