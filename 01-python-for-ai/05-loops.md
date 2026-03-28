# 🔁 Chapter 5 — Loops

> **Book:** Python for AI | **Chapter:** 5 of 14 | **Level:** 🟢 Beginner

---

## 🔄 Quick Recap

In Chapter 4 you learned:
- How to use `if`, `elif`, and `else` to make decisions
- Comparison operators like `==`, `>`, `<`
- Logical operators — `and`, `or`, `not`
- How to build a smart chatbot that responds to what the user says

Now let's learn **Loops** — how to make Python repeat things automatically!

---

## 🤔 What is a Loop?

Imagine you want to print numbers from 1 to 100.

Without loops you'd have to write:

```python
print(1)
print(2)
print(3)
# ... 97 more lines 😭
print(100)
```

With a loop — just 2 lines:

```python
for i in range(1, 101):
    print(i)
```

A **loop** tells Python: *"Keep doing this over and over until I say stop."*

Loops are everywhere in AI:
- Processing **every frame** of a camera video
- Training a model **thousands of times**
- Reading **every line** of a dataset
- Running a robot **forever** until turned off

---

## 🔵 The `for` Loop

A `for` loop repeats a fixed number of times.

```python
for i in range(5):
    print(i)
```

Output:
```
0
1
2
3
4
```

> 💡 `range(5)` gives numbers **0, 1, 2, 3, 4** — it starts from 0 and stops **before** 5!

---

### Controlling `range()`

`range()` can take 1, 2, or 3 arguments:

```python
range(5)          # 0, 1, 2, 3, 4
range(1, 6)       # 1, 2, 3, 4, 5
range(1, 11, 2)   # 1, 3, 5, 7, 9  (step by 2)
range(10, 0, -1)  # 10, 9, 8, 7, ... 1  (count down!)
```

Examples:

```python
# Count from 1 to 10
for i in range(1, 11):
    print(i)

# Count down from 5
for i in range(5, 0, -1):
    print(i)
print("🚀 Launch!")

# Even numbers only
for i in range(2, 21, 2):
    print(i)
```

Countdown output:
```
5
4
3
2
1
🚀 Launch!
```

---

### Looping Through a List

You can loop through any collection of items:

```python
fruits = ["apple", "banana", "mango", "grape"]

for fruit in fruits:
    print(f"I like {fruit}! 😋")
```

Output:
```
I like apple! 😋
I like banana! 😋
I like mango! 😋
I like grape! 😋
```

This is exactly how AI processes a **dataset** — looping through every item one by one!

---

### Looping Through a String

Strings are just a sequence of characters — you can loop through them too:

```python
word = "Python"

for letter in word:
    print(letter)
```

Output:
```
P
y
t
h
o
n
```

---

## 🟠 The `while` Loop

A `while` loop keeps running **as long as a condition is True**.

```python
count = 1

while count <= 5:
    print(f"Count: {count}")
    count += 1   # same as count = count + 1

print("Done!")
```

Output:
```
Count: 1
Count: 2
Count: 3
Count: 4
Count: 5
Done!
```

> ⚠️ **Always make sure the condition eventually becomes False!**
> If you forget `count += 1`, the loop runs forever — this is called an **infinite loop** and will crash your program!

---

### `while` Loop — Real Robot Use Case

In real robots, `while True` loops are used to keep the robot running forever:

```python
# This is how a real robot loop works!
import time

is_running = True

while is_running:
    print("🤖 Robot is listening...")
    command = input("Enter command (or 'stop' to quit): ").lower()

    if command == "hello":
        print("👋 Hello! I am your AI robot!")
    elif command == "status":
        print("🟢 All systems are working fine.")
    elif command == "stop":
        print("👋 Shutting down. Goodbye!")
        is_running = False
    else:
        print(f"🤔 Unknown command: '{command}'")

    print()
```

Run it:
```
🤖 Robot is listening...
Enter command (or 'stop' to quit): hello
👋 Hello! I am your AI robot!

🤖 Robot is listening...
Enter command (or 'stop' to quit): status
🟢 All systems are working fine.

🤖 Robot is listening...
Enter command (or 'stop' to quit): stop
👋 Shutting down. Goodbye!
```

🎉 This is the structure of almost every real robot program!

---

## 🛑 `break` and `continue`

### `break` — Exit the loop immediately

```python
for i in range(1, 11):
    if i == 5:
        print("Found 5! Stopping.")
        break
    print(i)
```

Output:
```
1
2
3
4
Found 5! Stopping.
```

### `continue` — Skip this step and go to the next

```python
for i in range(1, 11):
    if i % 2 == 0:   # skip even numbers
        continue
    print(i)
```

Output:
```
1
3
5
7
9
```

> 💡 `break` is used in AI when you find what you're looking for and don't need to keep searching. `continue` is used to skip bad or invalid data in a dataset!

---

## 🔢 Loop + Math = Power

**Sum of numbers:**

```python
total = 0

for i in range(1, 101):
    total += i   # same as total = total + i

print(f"Sum of 1 to 100 = {total}")
# Output: Sum of 1 to 100 = 5050
```

**Multiplication table:**

```python
number = int(input("Enter a number for its table: "))
print(f"\n📊 Multiplication Table of {number}")
print("-" * 25)

for i in range(1, 11):
    result = number * i
    print(f"  {number} × {i:2} = {result}")
```

Output:
```
📊 Multiplication Table of 7
-------------------------
  7 ×  1 = 7
  7 ×  2 = 14
  7 ×  3 = 21
  ...
  7 × 10 = 70
```

> 💡 `{i:2}` inside an f-string pads the number to 2 spaces wide — makes the output line up neatly!

---

## 🤖 AI Project — Frame Processor Simulator

In Computer Vision, your camera sends video as **frames** (individual pictures). Your AI must process every single frame. Here's a simulator:

```python
import time

print("📷 Starting Camera...")
print("🧠 AI Object Detection Running")
print("=" * 40)

total_frames = 10
objects_found = 0

for frame in range(1, total_frames + 1):
    # Simulate AI detecting something every 3rd frame
    detected = (frame % 3 == 0)

    if detected:
        objects_found += 1
        print(f"Frame {frame:2}: ✅ Object detected!")
    else:
        print(f"Frame {frame:2}: ⬜ Nothing found.")

print("=" * 40)
print(f"📊 Processed {total_frames} frames")
print(f"🎯 Objects detected in {objects_found} frames")
print(f"📈 Detection rate: {(objects_found/total_frames)*100:.1f}%")
```

Output:
```
📷 Starting Camera...
🧠 AI Object Detection Running
========================================
Frame  1: ⬜ Nothing found.
Frame  2: ⬜ Nothing found.
Frame  3: ✅ Object detected!
Frame  4: ⬜ Nothing found.
Frame  5: ⬜ Nothing found.
Frame  6: ✅ Object detected!
...
========================================
📊 Processed 10 frames
🎯 Objects detected in 3 frames
📈 Detection rate: 30.0%
```

This is the exact pattern used in your traffic violation detector! 🚗

---

## 🔲 Nested Loops — Loops Inside Loops

You can put a loop inside another loop. This is called a **nested loop**:

```python
for row in range(1, 4):
    for col in range(1, 4):
        print(f"({row},{col})", end="  ")
    print()   # new line after each row
```

Output:
```
(1,1)  (1,2)  (1,3)
(2,1)  (2,2)  (2,3)
(3,1)  (3,2)  (3,3)
```

**Star pattern using nested loops:**

```python
rows = int(input("How many rows? "))

for i in range(1, rows + 1):
    for j in range(i):
        print("★", end=" ")
    print()
```

Output (rows = 5):
```
★
★ ★
★ ★ ★
★ ★ ★ ★
★ ★ ★ ★ ★
```

---

## 🏋️ Practice Exercises

**Exercise 1 — FizzBuzz**

The most famous coding interview question! Print numbers 1 to 30, but:
- If the number is divisible by 3 → print `Fizz`
- If divisible by 5 → print `Buzz`
- If divisible by both 3 and 5 → print `FizzBuzz`
- Otherwise → print the number

```python
for i in range(1, 31):
    # Write your if/elif/else here
    pass
```

<details>
<summary>💡 Answer (click to reveal)</summary>

```python
for i in range(1, 31):
    if i % 15 == 0:
        print("FizzBuzz")
    elif i % 3 == 0:
        print("Fizz")
    elif i % 5 == 0:
        print("Buzz")
    else:
        print(i)
```

> Check `% 15` first — if you check `% 3` first, you'll never reach the FizzBuzz case!

</details>

---

**Exercise 2 — Number Guessing Game**

Build a full number guessing game using a `while` loop:
1. The secret number is 37
2. Keep asking the user to guess
3. Tell them if they're too high or too low
4. Count the number of attempts
5. When they get it right, show how many tries it took

```python
secret = 37
attempts = 0

while True:
    guess = int(input("Guess the number (1-100): "))
    attempts += 1

    # Write your if/elif/else here
```

<details>
<summary>💡 Answer (click to reveal)</summary>

```python
secret = 37
attempts = 0

while True:
    guess = int(input("Guess the number (1-100): "))
    attempts += 1

    if guess == secret:
        print(f"🎉 Correct! You got it in {attempts} attempts!")
        break
    elif guess > secret:
        print("📉 Too high! Try lower.")
    else:
        print("📈 Too low! Try higher.")
```

</details>

---

**Exercise 3 — Fix the infinite loop**

This code runs forever. Find the bug and fix it:

```python
count = 10

while count > 0:
    print(f"T-minus {count}...")

print("🚀 Liftoff!")
```

<details>
<summary>💡 Hint (click to reveal)</summary>

`count` never changes so the condition `count > 0` is always True! Add `count -= 1` inside the loop:

```python
count = 10

while count > 0:
    print(f"T-minus {count}...")
    count -= 1

print("🚀 Liftoff!")
```

</details>

---

## 📝 Chapter Summary

| Concept | Code | What it does |
|---------|------|--------------|
| For loop | `for i in range(5):` | Repeats 5 times (0 to 4) |
| Custom range | `range(1, 11)` | 1 to 10 |
| Step range | `range(0, 20, 2)` | 0, 2, 4, ... 18 |
| Loop a list | `for item in my_list:` | Goes through every item |
| While loop | `while condition:` | Repeats while condition is True |
| Run forever | `while True:` | Robot main loop |
| Add to variable | `x += 1` | Same as `x = x + 1` |
| Exit loop | `break` | Stops the loop immediately |
| Skip one step | `continue` | Jumps to next iteration |
| Nested loop | Loop inside a loop | Used for grids, patterns, tables |

---

## ➡️ What's Next?

In **Chapter 6**, you'll learn **Functions** — how to write reusable blocks of code. Functions are what make large AI programs organized and clean!

[👉 Chapter 6 — Functions](./06-functions.md)

---

<div align="center">

**⭐ If this helped you, star the repo!**

[← Chapter 4](./04-if-else.md) | [Back to Book Index](../README.md) | [Chapter 6 →](./06-functions.md)

</div>
