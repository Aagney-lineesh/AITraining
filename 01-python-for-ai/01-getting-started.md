# 🐍 Chapter 1 — Getting Started with Python

> **Book:** Python for AI | **Chapter:** 1 of 14 | **Level:** 🟢 Beginner

---

## 👋 Welcome!

Before building AI robots and voice assistants, you need one thing — **Python**.

Python is the language of AI. Almost every AI project in the world uses it. The good news? It's the easiest programming language to learn. If you can read English, you can read Python.

By the end of this chapter you will:

- ✅ Understand what Python is and why it matters for AI
- ✅ Install Python on your computer or Raspberry Pi
- ✅ Write and run your very first Python program
- ✅ Understand how the terminal works

---

## 🤔 What is Python?

Python is a **programming language** — a way to give instructions to a computer.

Think of it like this:

```
You (human) → Python code → Computer understands → Computer does the task
```

**Why Python for AI?**

| Language | Used for |
|----------|----------|
| Python 🐍 | AI, Machine Learning, Robots, Data |
| JavaScript | Websites |
| C++ | Games, System software |
| Java | Android apps |

Almost every AI tool — ChatGPT, Google Gemini, OpenCV — is built using Python. So learning Python = learning the language of AI.

---

## 💻 Installing Python

### On Windows

1. Go to → [python.org/downloads](https://python.org/downloads)
2. Click **Download Python 3.x.x** (latest version)
3. Run the installer
4. ⚠️ **IMPORTANT:** Check the box that says **"Add Python to PATH"** before clicking Install
5. Click **Install Now**

To verify it worked, open **Command Prompt** and type:

```bash
python --version
```

You should see something like:

```
Python 3.12.0
```

---

### On Raspberry Pi

Great news — Python is **already installed** on Raspberry Pi OS! Just open the terminal and check:

```bash
python3 --version
```

You should see:

```
Python 3.11.2
```

On Raspberry Pi, always use `python3` instead of `python`.

---

## 🖥️ Understanding the Terminal

The **terminal** (also called command prompt or shell) is where you run Python programs. It looks scary at first but it's just a text-based way to talk to your computer.

| What you want to do | Command |
|---|---|
| See where you are | `pwd` |
| List files in folder | `ls` (Mac/Pi) or `dir` (Windows) |
| Go into a folder | `cd folder-name` |
| Go back one folder | `cd ..` |
| Run a Python file | `python3 filename.py` |

---

## ✍️ Your First Python Program

Let's write the most famous program in the world.

**Step 1** — Open your terminal

**Step 2** — Create a new file called `hello.py`

```bash
nano hello.py
```

**Step 3** — Type this inside:

```python
print("Hello, World!")
print("My name is Aagney and I am learning AI 🤖")
```

**Step 4** — Save and exit (press `Ctrl + X`, then `Y`, then `Enter`)

**Step 5** — Run it!

```bash
python3 hello.py
```

**Output:**

```
Hello, World!
My name is Aagney and I am learning AI 🤖
```

🎉 **Congratulations! You just ran your first Python program.**

---

## 🧠 How `print()` Works

`print()` is a **function** — it tells Python to display something on the screen.

```python
print("anything you write here appears on screen")
```

- The text must be inside **quotes** `" "` or `' '`
- The text inside quotes is called a **string**
- You can print numbers too — without quotes!

```python
print("I am in class 8")   # text → use quotes
print(8)                   # number → no quotes needed
print(2 + 2)               # math → Python calculates it!
```

Output:

```
I am in class 8
8
4
```

---

## 💬 Comments in Python

A **comment** is a line Python ignores. It's just a note for the human reading the code.

```python
# This is a comment — Python skips this line
print("But Python runs this!")  # You can also comment at the end
```

Comments start with `#`. Use them to explain what your code does. Professional developers use comments everywhere — it's a good habit.

---

## 🏋️ Practice Exercises

Try these on your own before moving to Chapter 2!

**Exercise 1 — Print your details**

Write a program that prints your name, class, favourite subject, and dream job:

```python
# Your code here
print("Name: ")
print("Class: ")
print("Favourite subject: ")
print("Dream: ")
```

---

**Exercise 2 — Math with print**

What will this output? Try to guess before running it:

```python
print(10 + 5)
print(100 - 37)
print(6 * 7)
print(20 / 4)
```

---

**Exercise 3 — Fix the bug**

This code has a mistake. Find it and fix it:

```python
print(Hello World)
```

<details>
<summary>💡 Hint (click to reveal)</summary>

The text `Hello World` needs to be inside quotes!

```python
print("Hello World")
```

</details>

---

## 📝 Chapter Summary

| Concept | What it means |
|---|---|
| Python | Programming language used for AI |
| Terminal | Text-based way to run programs |
| `print()` | Displays text on screen |
| String | Text inside quotes `"like this"` |
| Comment | Notes in code starting with `#` |

---

## ➡️ What's Next?

In **Chapter 2**, you'll learn about **Variables** — the way Python stores and remembers information. This is where things start getting really interesting!

[👉 Chapter 2 — Variables and Data Types](./02-variables-and-types.md)

---

<div align="center">

**⭐ If this helped you, star the repo!**

[← Back to Book Index](../README.md) | [Chapter 2 →](./02-variables-and-types.md)

</div>
