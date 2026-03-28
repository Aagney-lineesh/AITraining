# 🗂️ Chapter 7 — Lists and Dictionaries

> **Book:** Python for AI | **Chapter:** 7 of 14 | **Level:** 🟡 Intermediate

---

## 🔄 Quick Recap

In Chapter 6 you learned:
- How to define and call functions using `def`
- Parameters and return values
- Default parameters
- Local vs global variables
- How functions make AI code clean and reusable

Now let's learn **Lists and Dictionaries** — how Python stores and organizes collections of data. This chapter is huge for AI — every dataset, every camera detection, every chatbot response history is stored using these!

---

## 📋 Part 1 — Lists

### 🤔 What is a List?

So far every variable stored **one value**:

```python
name = "Aagney"
score = 95
```

But what if you need to store **many values together**?

- All scores from an exam
- All words a user has spoken
- All objects detected by a camera
- All sensor readings from a robot

That's what a **list** is — a variable that holds **many values in order**.

```python
scores = [95, 87, 72, 91, 65]
fruits = ["apple", "mango", "banana", "grape"]
mixed  = [42, "hello", True, 3.14]   # lists can mix types!
empty  = []                           # an empty list
```

---

### 🔢 Accessing Items — Indexing

Every item in a list has a **position number** called an **index**.

> ⚠️ Python starts counting from **0**, not 1!

```python
fruits = ["apple", "mango", "banana", "grape"]
#index:      0        1        2        3
```

```python
print(fruits[0])    # apple
print(fruits[1])    # mango
print(fruits[2])    # banana
print(fruits[3])    # grape
```

**Negative indexing** — count from the end:

```python
print(fruits[-1])   # grape   (last item)
print(fruits[-2])   # banana  (second from last)
```

---

### ✂️ Slicing — Getting a Portion

```python
numbers = [10, 20, 30, 40, 50, 60, 70]

print(numbers[0:3])    # [10, 20, 30]   — index 0 up to (not including) 3
print(numbers[2:5])    # [30, 40, 50]
print(numbers[:4])     # [10, 20, 30, 40]  — from start
print(numbers[4:])     # [50, 60, 70]      — to the end
print(numbers[::2])    # [10, 30, 50, 70]  — every 2nd item
```

---

### 🛠️ Useful List Methods

```python
robots = ["RoboBuddy", "AIBot", "PyRobot"]

# Add to the END
robots.append("SuperBot")
print(robots)   # ["RoboBuddy", "AIBot", "PyRobot", "SuperBot"]

# Add at a specific position
robots.insert(1, "MiniBot")
print(robots)   # ["RoboBuddy", "MiniBot", "AIBot", "PyRobot", "SuperBot"]

# Remove a specific item
robots.remove("AIBot")
print(robots)   # ["RoboBuddy", "MiniBot", "PyRobot", "SuperBot"]

# Remove and get the last item
last = robots.pop()
print(last)     # SuperBot
print(robots)   # ["RoboBuddy", "MiniBot", "PyRobot"]

# Sort alphabetically
robots.sort()
print(robots)   # ["MiniBot", "PyRobot", "RoboBuddy"]

# Reverse
robots.reverse()
print(robots)   # ["RoboBuddy", "PyRobot", "MiniBot"]

# Count items
print(len(robots))      # 3

# Check if something is in the list
print("PyRobot" in robots)    # True
print("AIBot" in robots)      # False

# Find the index of an item
print(robots.index("PyRobot"))  # 1
```

---

### 🔁 Looping Through a List

This is where lists and loops come together — and this is **exactly** how AI processes data:

```python
scores = [85, 92, 78, 96, 61, 88, 74]

# Print every score
for score in scores:
    print(score)

# Find all scores above 80
print("\nTop scorers:")
for score in scores:
    if score >= 80:
        print(f"  ✅ {score}")

# Calculate average
total = 0
for score in scores:
    total += score
average = total / len(scores)
print(f"\nAverage score: {average:.1f}")
```

Output:
```
Top scorers:
  ✅ 85
  ✅ 92
  ✅ 96
  ✅ 88

Average score: 82.0
```

---

### 🤖 AI Use Case — Detection Log

In Computer Vision, every object your camera detects gets added to a list:

```python
# Simulating what YOLO object detection stores
detected_objects = []

# Objects detected frame by frame
detected_objects.append("person")
detected_objects.append("car")
detected_objects.append("person")
detected_objects.append("bicycle")
detected_objects.append("car")
detected_objects.append("person")

print(f"Total detections: {len(detected_objects)}")
print(f"People detected:  {detected_objects.count('person')}")
print(f"Cars detected:    {detected_objects.count('car')}")
print(f"Unique objects:   {list(set(detected_objects))}")
```

Output:
```
Total detections: 6
People detected:  3
Cars detected:    2
Unique objects:   ['bicycle', 'person', 'car']
```

> 💡 `set()` removes duplicates from a list — very useful for finding unique detected objects!

---

## 📖 Part 2 — Dictionaries

### 🤔 What is a Dictionary?

A list stores items by **position number** (index 0, 1, 2...).

A **dictionary** stores items by **name** (called a **key**).

Think of it like a real dictionary — you look up a **word** (key) and find its **meaning** (value).

```python
# List — access by position
person_list = ["Aagney", 14, "Vadakara"]
print(person_list[0])   # Aagney — but what is index 0? Not obvious!

# Dictionary — access by name
person_dict = {
    "name": "Aagney",
    "age": 14,
    "city": "Vadakara"
}
print(person_dict["name"])   # Aagney — much clearer!
```

---

### ✍️ Creating a Dictionary

```python
robot = {
    "name": "RoboBuddy",
    "version": 2.1,
    "battery": 85,
    "is_online": True,
    "features": ["voice", "camera", "GPS"]   # a list inside a dict!
}
```

Access values using their key:

```python
print(robot["name"])       # RoboBuddy
print(robot["battery"])    # 85
print(robot["features"])   # ['voice', 'camera', 'GPS']
print(robot["features"][0])  # voice  (list inside dict!)
```

---

### 🛠️ Modifying Dictionaries

```python
robot = {"name": "RoboBuddy", "battery": 85, "speed": 5}

# Change a value
robot["battery"] = 72
print(robot["battery"])   # 72

# Add a new key-value pair
robot["color"] = "blue"
print(robot)

# Remove a key
del robot["speed"]
print(robot)

# Check if a key exists
print("battery" in robot)   # True
print("speed" in robot)     # False

# Get all keys
print(robot.keys())     # dict_keys(['name', 'battery', 'color'])

# Get all values
print(robot.values())   # dict_values(['RoboBuddy', 72, 'blue'])

# Get a value safely (no crash if key missing)
print(robot.get("speed", "Not found"))   # Not found
```

---

### 🔁 Looping Through a Dictionary

```python
robot = {
    "name": "RoboBuddy",
    "battery": 85,
    "wifi": 92,
    "temperature": 47
}

# Loop through keys only
for key in robot:
    print(key)

# Loop through keys AND values
for key, value in robot.items():
    print(f"  {key}: {value}")
```

Output:
```
  name: RoboBuddy
  battery: 85
  wifi: 92
  temperature: 47
```

---

### 📚 List of Dictionaries — The AI Dataset Pattern

This is the most important pattern in all of AI programming — a **list of dictionaries** is exactly how datasets are stored!

```python
# This is what an AI dataset looks like in Python
students = [
    {"name": "Aagney",  "score": 95, "grade": "A", "city": "Vadakara"},
    {"name": "Rahul",   "score": 82, "grade": "B", "city": "Kochi"},
    {"name": "Priya",   "score": 78, "grade": "C", "city": "Thrissur"},
    {"name": "Arjun",   "score": 91, "grade": "A", "city": "Kozhikode"},
    {"name": "Meera",   "score": 67, "grade": "D", "city": "Kannur"},
]

# Print all students
print("📋 Student Report")
print("-" * 45)
for student in students:
    print(f"  {student['name']:<10} | Score: {student['score']} | Grade: {student['grade']}")

# Find top scorer
top = students[0]
for student in students:
    if student["score"] > top["score"]:
        top = student
print(f"\n🏆 Top scorer: {top['name']} with {top['score']}")

# Count grade A students
a_students = []
for student in students:
    if student["grade"] == "A":
        a_students.append(student["name"])
print(f"⭐ Grade A students: {a_students}")
```

Output:
```
📋 Student Report
---------------------------------------------
  Aagney     | Score: 95 | Grade: A
  Rahul      | Score: 82 | Grade: B
  Priya      | Score: 78 | Grade: C
  Arjun      | Score: 91 | Grade: A
  Meera      | Score: 67 | Grade: D

🏆 Top scorer: Aagney with 95
⭐ Grade A students: ['Aagney', 'Arjun']
```

---

## 🤖 Full Project — AI Robot Memory System

Real AI assistants remember things you've told them. Let's build one!

Create `robot_memory.py`:

```python
# 🤖 Robot Memory System — Chapter 7 Project

# Robot's memory — a dictionary of lists
memory = {
    "name": "",
    "known_facts": [],
    "conversation_history": [],
    "favourite_topics": []
}

def save_memory(key, value):
    if isinstance(value, list):
        memory[key].append(value)
    else:
        memory[key] = value

def show_memory():
    print("\n🧠 Robot Memory:")
    print("-" * 35)
    print(f"  Your name:      {memory['name']}")
    print(f"  Facts I know:   {len(memory['known_facts'])}")
    print(f"  Topics I know:  {memory['favourite_topics']}")
    print(f"  Chats so far:   {len(memory['conversation_history'])}")
    print("-" * 35)

# ── Main Program ──────────────────────────────
print("=" * 40)
print("  🤖 RoboMemory — AI with Memory!")
print("=" * 40)

name = input("\nHello! What's your name? ")
memory["name"] = name
print(f"Nice to meet you, {name}! I'll remember that. 🧠")

# Teach the robot some facts
print(f"\nTeach me 3 facts about yourself, {name}!")
for i in range(1, 4):
    fact = input(f"  Fact {i}: ")
    memory["known_facts"].append(fact)

# Ask favourite topics
print("\nWhat topics do you like? (type one at a time, 'done' to stop)")
while True:
    topic = input("  Topic: ").lower()
    if topic == "done":
        break
    if topic not in memory["favourite_topics"]:
        memory["favourite_topics"].append(topic)
        print(f"  Got it! I'll remember you like {topic}. ✅")
    else:
        print("  I already know that! 😄")

# Save this to conversation history
memory["conversation_history"].append(f"First chat with {name}")

# Show what the robot remembers
show_memory()

print(f"\n🤖 I know these facts about you, {name}:")
for i, fact in enumerate(memory["known_facts"], 1):
    print(f"  {i}. {fact}")

print(f"\nYour favourite topics: {', '.join(memory['favourite_topics'])}")
print("\nSee you next time! 👋")
print("=" * 40)
```

---

## 🏋️ Practice Exercises

**Exercise 1 — Shopping List Manager**

Build a program that lets the user add items to a shopping list, view the list, and remove items:

```python
shopping_list = []

while True:
    print("\n1. Add item")
    print("2. View list")
    print("3. Remove item")
    print("4. Quit")
    choice = input("Choose: ")

    if choice == "1":
        # add item to list
        pass
    elif choice == "2":
        # print all items
        pass
    elif choice == "3":
        # remove an item
        pass
    elif choice == "4":
        break
```

---

**Exercise 2 — Contact Book**

Create a dictionary-based contact book:

```python
contacts = {}

# Add some contacts
contacts["Aagney"]  = {"phone": "9876543210", "city": "Vadakara"}
contacts["Rahul"]   = {"phone": "9123456789", "city": "Kochi"}

# Search for a contact
name = input("Search contact: ")

# Write code to find and print the contact
# If not found, print "Contact not found"
```

<details>
<summary>💡 Answer (click to reveal)</summary>

```python
if name in contacts:
    info = contacts[name]
    print(f"\n📞 {name}")
    print(f"   Phone: {info['phone']}")
    print(f"   City:  {info['city']}")
else:
    print(f"❌ '{name}' not found in contacts.")
```

</details>

---

**Exercise 3 — Find the bug**

```python
fruits = ["apple", "mango", "banana"]

# Try to print the 4th item
print(fruits[3])

# Try to find watermelon
position = fruits.index("watermelon")
print(position)
```

<details>
<summary>💡 Hint (click to reveal)</summary>

Two bugs:
1. `fruits[3]` → list only has indices 0, 1, 2. Use `fruits[-1]` for the last item or check `len(fruits)` first.
2. `.index("watermelon")` crashes if item not in list. Use `if "watermelon" in fruits:` first.

```python
fruits = ["apple", "mango", "banana"]

# Safe last item
print(fruits[-1])   # banana

# Safe search
if "watermelon" in fruits:
    print(fruits.index("watermelon"))
else:
    print("watermelon not in list")
```

</details>

---

## 📝 Chapter Summary

### Lists

| Concept | Code | What it does |
|---------|------|--------------|
| Create | `items = [1, 2, 3]` | Makes a list |
| Access | `items[0]` | Gets item at index 0 |
| Last item | `items[-1]` | Gets last item |
| Slice | `items[1:3]` | Gets items at index 1 and 2 |
| Add to end | `items.append(x)` | Adds x at the end |
| Insert | `items.insert(i, x)` | Inserts x at position i |
| Remove | `items.remove(x)` | Removes first x found |
| Remove last | `items.pop()` | Removes and returns last item |
| Length | `len(items)` | Number of items |
| Count | `items.count(x)` | How many times x appears |
| Check | `x in items` | True if x is in list |
| Sort | `items.sort()` | Sorts alphabetically/numerically |
| Remove duplicates | `list(set(items))` | Keeps only unique items |

### Dictionaries

| Concept | Code | What it does |
|---------|------|--------------|
| Create | `d = {"key": "value"}` | Makes a dictionary |
| Access | `d["key"]` | Gets value for key |
| Safe access | `d.get("key", default)` | Returns default if key missing |
| Add/Update | `d["key"] = value` | Adds or updates a key |
| Delete | `del d["key"]` | Removes a key |
| Check key | `"key" in d` | True if key exists |
| All keys | `d.keys()` | Returns all keys |
| All values | `d.values()` | Returns all values |
| Loop both | `for k, v in d.items():` | Loop key and value together |

---

## ➡️ What's Next?

In **Chapter 8**, you'll learn **File Handling** — how Python reads and writes files. This is how AI saves data, stores trained results, logs sensor readings, and loads datasets from CSV files!

[👉 Chapter 8 — File Handling](./08-file-handling.md)

---

<div align="center">

**Progress — Book 1: Python for AI**

`✅ Ch1` `✅ Ch2` `✅ Ch3` `✅ Ch4` `✅ Ch5` `✅ Ch6` `✅ Ch7` `⬜ Ch8` `⬜ Ch9` `⬜ Ch10` `⬜ Ch11` `⬜ Ch12` `⬜ Ch13` `⬜ Ch14`

---

**⭐ If this helped you, star the repo!**

[← Chapter 6](./06-functions.md) | [Back to Book Index](../README.md) | [Chapter 8 →](./08-file-handling.md)

</div>
