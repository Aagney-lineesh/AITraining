# 🧠 Chapter 4 — If / Else Statements

> **Book:** Python for AI | **Chapter:** 4 of 14 | **Level:** 🟢 Beginner

---

## 🔄 Quick Recap

In Chapter 3 you learned:
- How to use `input()` to get data from the user
- That `input()` always returns a string
- How to convert types using `int()` and `float()`
- How to build a simple chatbot and calculator

Now let's teach Python how to **make decisions** — the most important skill in all of programming and AI!

---

## 🤔 What is an If / Else Statement?

Every intelligent system makes decisions.

- A traffic light decides: *"Is it red? Stop. Is it green? Go."*
- A spam filter decides: *"Is this email suspicious? Block it. Is it safe? Deliver it."*
- Your voice robot decides: *"Did the user say hello? Reply with a greeting."*

In Python, decisions are made using **if / else statements**.

The idea is simple:

```
IF something is true → do this
ELSE → do that instead
```

---

## ✍️ Basic Syntax

```python
if condition:
    # code to run if condition is True
else:
    # code to run if condition is False
```

> ⚠️ **The colon `:` at the end of `if` and `else` is required!**
> ⚠️ **The code inside must be indented — 4 spaces or 1 Tab!**

---

## 🟢 Your First If / Else

```python
age = int(input("Enter your age: "))

if age >= 18:
    print("You are an adult ✅")
else:
    print("You are a minor 🔒")
```

Run it:

```
Enter your age: 14
You are a minor 🔒
```

```
Enter your age: 20
You are an adult ✅
```

---

## ⚖️ Comparison Operators

These are used inside `if` conditions to compare values:

| Operator | Meaning | Example | Result |
|----------|---------|---------|--------|
| `==` | Equal to | `5 == 5` | `True` |
| `!=` | Not equal to | `5 != 3` | `True` |
| `>` | Greater than | `10 > 7` | `True` |
| `<` | Less than | `3 < 8` | `True` |
| `>=` | Greater than or equal | `5 >= 5` | `True` |
| `<=` | Less than or equal | `4 <= 6` | `True` |

> ⚠️ Don't confuse `=` and `==`!
> - `=` means **assign** → `age = 14` (store 14 in age)
> - `==` means **compare** → `age == 14` (is age equal to 14?)

---

## 🔀 elif — More Than Two Choices

What if you need more than just two options? Use `elif` (short for "else if"):

```python
score = int(input("Enter your exam score: "))

if score >= 90:
    print("🏆 Grade: A — Excellent!")
elif score >= 80:
    print("🥈 Grade: B — Very Good!")
elif score >= 70:
    print("🥉 Grade: C — Good!")
elif score >= 60:
    print("📘 Grade: D — Pass")
else:
    print("❌ Grade: F — Please study more")
```

Run it:

```
Enter your exam score: 85
🥈 Grade: B — Very Good!
```

Python checks each condition **from top to bottom** and stops at the first one that is `True`.

---

## 🔗 Logical Operators — Combining Conditions

Sometimes one condition isn't enough. Use `and`, `or`, `not`:

| Operator | Meaning | Example |
|----------|---------|---------|
| `and` | Both must be True | `age > 10 and age < 18` |
| `or` | At least one must be True | `day == "Sat" or day == "Sun"` |
| `not` | Flips True to False | `not is_raining` |

```python
age = int(input("Enter age: "))
has_id = input("Do you have an ID? (yes/no): ")

if age >= 18 and has_id == "yes":
    print("✅ Entry allowed!")
elif age >= 18 and has_id == "no":
    print("⚠️ You need an ID card.")
else:
    print("❌ You must be 18 or older.")
```

---

## 🤖 Real AI Example — Smart Chatbot

Let's upgrade the chatbot from Chapter 3 to make it respond intelligently!

Create `smart_chatbot.py`:

```python
# Smart Chatbot — Chapter 4 Project

print("=" * 45)
print("   🤖 SmartBot — AI Powered Chatbot")
print("=" * 45)
print()

name = input("Hi! What's your name? ")
print(f"Hello, {name}! 👋")
print()

mood = input("How are you feeling today? (good/bad/okay): ").lower()

if mood == "good":
    print("That's amazing! 😄 Let's learn some AI today!")
elif mood == "bad":
    print("Sorry to hear that 😔 I'm here for you. Let's cheer up with some coding!")
elif mood == "okay":
    print("Okay is perfectly fine! 🙂 Let's make it better with Python!")
else:
    print(f"I don't know what '{mood}' means, but I'm sure you're doing great! 💪")

print()
subject = input("What subject do you want to learn? (python/ai/robotics): ").lower()

if subject == "python":
    print("🐍 Great choice! Python is the language of AI. You're on the right track!")
elif subject == "ai":
    print("🧠 AI is the future! You're going to build amazing things.")
elif subject == "robotics":
    print("🤖 Robotics is SO cool! Raspberry Pi + Python = unlimited power!")
else:
    print(f"📚 {subject} sounds interesting! Keep exploring!")

print()
print(f"See you soon, {name}! Keep building! 🚀")
print("=" * 45)
```

Run it:

```
=============================================
   🤖 SmartBot — AI Powered Chatbot
=============================================

Hi! What's your name? Aagney
Hello, Aagney! 👋

How are you feeling today? (good/bad/okay): good
That's amazing! 😄 Let's learn some AI today!

What subject do you want to learn? (python/ai/robotics): robotics
🤖 Robotics is SO cool! Raspberry Pi + Python = unlimited power!

See you soon, Aagney! Keep building! 🚀
=============================================
```

> 💡 Notice `.lower()` — this converts whatever the user types to lowercase. So whether they type `"Good"`, `"GOOD"`, or `"good"`, it always becomes `"good"`. Always use `.lower()` when comparing strings from user input!

---

## 🔋 Robot Battery Checker

Here's a practical example you could use in a real Raspberry Pi robot:

```python
# Robot Battery Status Checker

battery = float(input("Enter battery level (%): "))

print()
if battery >= 80:
    print("🟢 Battery: FULL — Robot is ready to go!")
elif battery >= 50:
    print("🟡 Battery: GOOD — Running normally.")
elif battery >= 20:
    print("🟠 Battery: LOW — Please charge soon.")
elif battery > 0:
    print("🔴 Battery: CRITICAL — Robot shutting down soon!")
else:
    print("⚫ Battery: DEAD — Please charge immediately!")

if battery < 20:
    print("⚠️  WARNING: Connect charger now!")
```

---

## 🔍 Checking Strings with `in`

You can check if a word **contains** something using `in`:

```python
message = input("Say something: ").lower()

if "hello" in message or "hi" in message:
    print("👋 Hey there! Nice to meet you!")
elif "bye" in message or "goodbye" in message:
    print("👋 Goodbye! Come back soon!")
elif "help" in message:
    print("🆘 I'm here to help! What do you need?")
else:
    print(f"🤔 You said: '{message}' — I'm still learning!")
```

This is exactly how a basic chatbot recognizes what the user says — real AI chatbots work the same way, just much more advanced!

---

## 🏋️ Practice Exercises

**Exercise 1 — Number Guessing Hint**

The secret number is 42. Ask the user to guess and tell them if they are too high, too low, or correct:

```python
secret = 42
guess = int(input("Guess the number (1-100): "))

# Write your if/elif/else here
```

<details>
<summary>💡 Answer (click to reveal)</summary>

```python
secret = 42
guess = int(input("Guess the number (1-100): "))

if guess == secret:
    print("🎉 Correct! You got it!")
elif guess > secret:
    print("📉 Too high! Try lower.")
else:
    print("📈 Too low! Try higher.")
```

</details>

---

**Exercise 2 — Triangle Type Checker**

Ask for 3 angles and tell the user what type of triangle it is:
- All angles equal 60 → **Equilateral**
- Two angles are equal → **Isosceles**
- All angles different → **Scalene**
- Any angle is 90 → **Right-angled**

```python
a = int(input("Enter angle 1: "))
b = int(input("Enter angle 2: "))
c = int(input("Enter angle 3: "))

# First check if it's a valid triangle
if a + b + c != 180:
    print("❌ Not a valid triangle! Angles must add up to 180.")
else:
    # Write your conditions here
    pass
```

---

**Exercise 3 — Fix the bug**

Find all mistakes in this code:

```python
temperature = float(input("Enter temperature: "))

if temperature = 100:
    print("Water is boiling!")
elif temperature > 0 AND temperature < 100:
    print("Water is liquid.")
Else:
    print("Water is frozen!")
```

<details>
<summary>💡 Hint (click to reveal)</summary>

Three bugs:
1. `=` should be `==` inside the `if`
2. `AND` should be lowercase `and`
3. `Else` should be lowercase `else`

```python
temperature = float(input("Enter temperature: "))

if temperature == 100:
    print("Water is boiling!")
elif temperature > 0 and temperature < 100:
    print("Water is liquid.")
else:
    print("Water is frozen!")
```

</details>

---

## 📝 Chapter Summary

| Concept | Code | What it does |
|---------|------|--------------|
| Basic decision | `if condition:` | Runs if condition is True |
| Alternative | `else:` | Runs if condition is False |
| Extra options | `elif condition:` | Checks another condition |
| Equal | `==` | Compares two values |
| Not equal | `!=` | Checks if values differ |
| Both true | `and` | Both conditions must pass |
| Either true | `or` | At least one must pass |
| Flip condition | `not` | Reverses True / False |
| Lowercase text | `.lower()` | Makes string comparison reliable |
| Word inside text | `"word" in text` | Checks if text contains word |

---

## ➡️ What's Next?

In **Chapter 5**, you'll learn **Loops** — how to make Python repeat things automatically. Loops are everywhere in AI — from training models to processing every frame of a video!

[👉 Chapter 5 — Loops](./05-loops.md)

---

<div align="center">

**⭐ If this helped you, star the repo!**

[← Chapter 3](./03-user-input.md) | [Back to Book Index](../README.md) | [Chapter 5 →](./05-loops.md)

</div>
