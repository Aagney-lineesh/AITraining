# 📦 Chapter 9 — Modules and Libraries

> **Book:** Python for AI | **Chapter:** 9 of 14 | **Level:** 🟡 Intermediate

---

## 🔄 Quick Recap

In Chapter 8 you learned:
- How to read and write text files
- How to append data without overwriting
- How to work with CSV files — the AI dataset format
- How to handle missing files safely with `try / except`
- How to build a robot activity logger

Now let's learn **Modules and Libraries** — the single biggest unlock in Python. This is the chapter where you go from beginner to someone who can build **real AI projects**!

---

## 🤔 What is a Module?

A **module** is a Python file that contains ready-made functions you can use.

Instead of writing everything from scratch, you simply **import** someone else's code and use it instantly.

You've already used one — `csv` in Chapter 8:

```python
import csv   # ← you imported the csv module
```

Python comes with **hundreds of built-in modules**. And the internet has **hundreds of thousands more** you can install!

---

## 📥 Importing Modules — 3 Ways

```python
# Way 1 — Import the whole module
import math
print(math.sqrt(25))    # 5.0
print(math.pi)          # 3.14159...

# Way 2 — Import only what you need
from math import sqrt, pi
print(sqrt(25))         # 5.0  (no "math." needed)
print(pi)               # 3.14159...

# Way 3 — Import with a nickname (alias)
import math as m
print(m.sqrt(25))       # 5.0
```

> 💡 Way 3 is very common in AI — you'll see `import numpy as np` and `import pandas as pd` everywhere!

---

## 🔧 Python's Built-in Modules

These come with Python — no installation needed!

---

### 📐 `math` — Mathematics

```python
import math

print(math.sqrt(144))       # 12.0  — square root
print(math.pow(2, 10))      # 1024.0 — 2 to the power 10
print(math.pi)              # 3.141592653589793
print(math.floor(9.8))      # 9  — round down
print(math.ceil(9.1))       # 10 — round up
print(math.factorial(5))    # 120 — 5!
print(math.log(100, 10))    # 2.0 — log base 10
```

---

### 🎲 `random` — Random Numbers

Used in AI for shuffling datasets, generating test data, and simulations:

```python
import random

print(random.randint(1, 100))       # random whole number 1–100
print(random.random())              # random float 0.0–1.0
print(random.choice(["red", "blue", "green"]))   # random item from list

# Shuffle a list
cards = ["Ace", "King", "Queen", "Jack", "10"]
random.shuffle(cards)
print(cards)    # shuffled randomly!

# Pick multiple random items
scores = [85, 92, 78, 96, 61, 88, 74, 95, 83]
sample = random.sample(scores, 3)   # pick 3 without repeating
print(sample)
```

---

### 🕐 `datetime` — Dates and Times

Used in every log file, sensor reading, and data timestamp:

```python
from datetime import datetime

now = datetime.now()
print(now)                                      # 2026-03-27 14:35:22.123456

# Formatted timestamps
print(now.strftime("%d-%m-%Y"))                 # 27-03-2026
print(now.strftime("%H:%M:%S"))                 # 14:35:22
print(now.strftime("%d %B %Y, %I:%M %p"))       # 27 March 2026, 02:35 PM

# Individual parts
print(now.year)     # 2026
print(now.month)    # 3
print(now.day)      # 27
print(now.hour)     # 14
```

---

### ⏱️ `time` — Pausing and Timing

Used in robots to add delays between actions:

```python
import time

print("🤖 Robot starting...")
time.sleep(2)                  # pause for 2 seconds
print("✅ Systems ready!")
time.sleep(1)
print("🎙️ Listening...")

# Measure how long something takes
start = time.time()

total = 0
for i in range(1000000):
    total += i

end = time.time()
print(f"Calculated in {end - start:.3f} seconds")
```

---

### 🖥️ `os` — Operating System

Control your computer/Pi from Python:

```python
import os

# Current folder
print(os.getcwd())                  # /home/techaagney2012

# List all files
files = os.listdir(".")
print(files)

# Create a new folder
os.makedirs("robot_logs", exist_ok=True)

# Check if file exists
print(os.path.exists("robot_log.txt"))   # True or False

# Get file size
size = os.path.getsize("robot_log.txt")
print(f"File size: {size} bytes")

# Run a terminal command from Python!
os.system("echo Hello from Python!")
```

---

## 📦 Installing External Libraries

Python's built-in modules are great, but the **real power** comes from external libraries installed using `pip`.

### Installing on Raspberry Pi

```bash
pip3 install library-name --break-system-packages
```

### The Most Important AI Libraries

| Library | What it does | Install command |
|---------|-------------|-----------------|
| `speech_recognition` | Convert voice to text | `pip3 install SpeechRecognition` |
| `pyttsx3` | Convert text to speech | `pip3 install pyttsx3` |
| `opencv-python` | Computer vision / camera | `pip3 install opencv-python` |
| `google-generativeai` | Google Gemini AI API | `pip3 install google-generativeai` |
| `anthropic` | Claude AI API | `pip3 install anthropic` |
| `RPi.GPIO` | Raspberry Pi GPIO pins | Pre-installed on Pi |
| `requests` | Download data from internet | `pip3 install requests` |
| `numpy` | Fast number calculations | `pip3 install numpy` |
| `pandas` | Work with datasets/CSV | `pip3 install pandas` |

---

## 🌐 `requests` — Get Data from the Internet

This library lets your robot download live data:

```python
import requests

# Get a random joke from the internet
response = requests.get("https://official-joke-api.appspot.com/random_joke")

if response.status_code == 200:     # 200 means success!
    joke = response.json()
    print(f"😂 {joke['setup']}")
    print(f"   {joke['punchline']}")
else:
    print("❌ Could not connect.")
```

**Check the weather (using wttr.in):**

```python
import requests

city = input("Enter city name: ")
url = f"https://wttr.in/{city}?format=3"

response = requests.get(url)
if response.status_code == 200:
    print(f"🌤️ {response.text}")
```

Output:
```
Enter city name: Vadakara
🌤️ Vadakara: ⛅️ +29°C
```

---

## 🎙️ `speech_recognition` — Voice to Text

This is inside your voice robot! Here's how it works:

```python
import speech_recognition as sr

recognizer = sr.Recognizer()

print("🎙️ Listening... speak now!")

with sr.Microphone() as source:
    recognizer.adjust_for_ambient_noise(source, duration=1)
    audio = recognizer.listen(source, timeout=5)

try:
    text = recognizer.recognize_google(audio)
    print(f"You said: {text}")

except sr.UnknownValueError:
    print("❌ Could not understand audio")
except sr.RequestError:
    print("❌ Could not connect to Google API")
```

---

## 🔊 `pyttsx3` — Text to Speech

Make your robot talk:

```python
import pyttsx3

engine = pyttsx3.init()

# Customize the voice
engine.setProperty("rate", 150)     # speed — 150 words per minute
engine.setProperty("volume", 0.9)   # volume — 0.0 to 1.0

# Speak!
engine.say("Hello! I am your AI robot. How can I help you today?")
engine.runAndWait()

# Speak a variable
name = input("What is your name? ")
engine.say(f"Hello {name}! Nice to meet you!")
engine.runAndWait()
```

---

## 🤖 Full Project — AI Assistant with Voice, Time & Weather

Let's combine `pyttsx3`, `datetime`, `requests` and `speech_recognition` into one mini AI assistant!

Create `ai_assistant.py`:

```python
# 🤖 Mini AI Assistant — Chapter 9 Project
import pyttsx3
import speech_recognition as sr
from datetime import datetime
import requests
import random

# ── Setup ─────────────────────────────────────
engine = pyttsx3.init()
engine.setProperty("rate", 145)
engine.setProperty("volume", 0.9)

recognizer = sr.Recognizer()

# ── Functions ─────────────────────────────────

def speak(text):
    """Make the robot say something"""
    print(f"🤖 Robot: {text}")
    engine.say(text)
    engine.runAndWait()

def listen():
    """Listen for one voice command"""
    with sr.Microphone() as source:
        print("🎙️ Listening...")
        recognizer.adjust_for_ambient_noise(source, duration=0.5)
        try:
            audio = recognizer.listen(source, timeout=5)
            text = recognizer.recognize_google(audio).lower()
            print(f"👤 You said: {text}")
            return text
        except:
            return ""

def get_time():
    now = datetime.now()
    return now.strftime("The time is %I:%M %p")

def get_date():
    now = datetime.now()
    return now.strftime("Today is %A, %d %B %Y")

def get_weather(city="Vadakara"):
    try:
        response = requests.get(f"https://wttr.in/{city}?format=3", timeout=5)
        return response.text
    except:
        return "Could not fetch weather right now."

def respond(command):
    """Decide what to do based on the command"""
    if "time" in command:
        speak(get_time())

    elif "date" in command or "day" in command:
        speak(get_date())

    elif "weather" in command:
        speak(get_weather())

    elif "hello" in command or "hi" in command:
        greetings = [
            "Hello! How are you doing?",
            "Hi there! Ready to learn some AI?",
            "Hey! Great to hear from you!"
        ]
        speak(random.choice(greetings))

    elif "your name" in command or "who are you" in command:
        speak("I am RoboBuddy, your personal AI assistant built with Python!")

    elif "joke" in command:
        speak("Why do programmers prefer dark mode? Because light attracts bugs!")

    elif "bye" in command or "stop" in command or "exit" in command:
        speak("Goodbye! Keep building amazing things!")
        return False   # signal to stop

    else:
        speak(f"I heard you say {command}, but I don't know how to respond to that yet!")

    return True   # signal to keep running

# ── Main Loop ─────────────────────────────────

speak("Hello! I am RoboBuddy. I am ready. You can ask me the time, date, weather, or say hello!")

running = True
while running:
    command = listen()
    if command:
        running = respond(command)
    else:
        speak("Sorry, I did not catch that. Please try again.")
```

---

## 🏋️ Practice Exercises

**Exercise 1 — Module Explorer**

Run each of these and write down what you see:

```python
import math, random, os
from datetime import datetime

print(math.sqrt(256))
print(math.factorial(6))
print(random.randint(1, 1000))
print(random.choice(["AI", "Robotics", "Python", "Computer Vision"]))
print(datetime.now().strftime("%A %d %B %Y"))
print(os.getcwd())
```

---

**Exercise 2 — Random Quiz Generator**

Use the `random` module to build a maths quiz:

```python
import random

score = 0
questions = 5

for i in range(questions):
    a = random.randint(1, 20)
    b = random.randint(1, 20)
    operation = random.choice(["+", "-", "*"])

    if operation == "+":
        answer = a + b
    elif operation == "-":
        answer = a - b
    else:
        answer = a * b

    guess = int(input(f"Q{i+1}: What is {a} {operation} {b}? "))

    if guess == answer:
        print("✅ Correct!")
        score += 1
    else:
        print(f"❌ Wrong! Answer was {answer}")

print(f"\n🏆 Your score: {score}/{questions}")
```

---

**Exercise 3 — System Info Reporter**

Use `os` and `datetime` to print a system report:

```python
import os
from datetime import datetime

print("=" * 40)
print("  🖥️ SYSTEM REPORT")
print("=" * 40)
# Print current time, current directory,
# and list all files in the current folder
```

<details>
<summary>💡 Answer (click to reveal)</summary>

```python
import os
from datetime import datetime

print("=" * 40)
print("  🖥️ SYSTEM REPORT")
print("=" * 40)
print(f"  Time     : {datetime.now().strftime('%d-%m-%Y %H:%M:%S')}")
print(f"  Folder   : {os.getcwd()}")
files = os.listdir(".")
print(f"  Files    : {len(files)} found")
for f in files:
    print(f"    📄 {f}")
print("=" * 40)
```

</details>

---

## 📝 Chapter Summary

### Built-in Modules

| Module | Key functions |
|--------|--------------|
| `math` | `sqrt()`, `pow()`, `pi`, `floor()`, `ceil()`, `factorial()` |
| `random` | `randint()`, `random()`, `choice()`, `shuffle()`, `sample()` |
| `datetime` | `datetime.now()`, `.strftime()` |
| `time` | `sleep()`, `time()` |
| `os` | `getcwd()`, `listdir()`, `makedirs()`, `path.exists()` |
| `csv` | `DictWriter`, `DictReader` (from Chapter 8) |

### Key Concepts

| Concept | Code |
|---------|------|
| Import module | `import math` |
| Import specific | `from math import sqrt` |
| Import with alias | `import numpy as np` |
| Install library | `pip3 install name --break-system-packages` |
| Check HTTP success | `response.status_code == 200` |
| Parse JSON | `response.json()` |

---

## ➡️ What's Next?

In **Chapter 10**, you'll learn **Object Oriented Programming (OOP)** — how to create your own custom types using **Classes**. This is how every real AI project organizes its code — your robot, your detector, your assistant — all as clean, powerful Python classes!

[👉 Chapter 10 — Classes and OOP](./10-classes-and-oop.md)

---

<div align="center">

**Progress — Book 1: Python for AI**

`✅ Ch1` `✅ Ch2` `✅ Ch3` `✅ Ch4` `✅ Ch5` `✅ Ch6` `✅ Ch7` `✅ Ch8` `✅ Ch9` `⬜ Ch10` `⬜ Ch11` `⬜ Ch12` `⬜ Ch13` `⬜ Ch14`

---

**⭐ If this helped you, star the repo!**

[← Chapter 8](./08-file-handling.md) | [Back to Book Index](../README.md) | [Chapter 10 →](./10-classes-and-oop.md)

</div>
