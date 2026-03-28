# 📁 Chapter 8 — File Handling

> **Book:** Python for AI | **Chapter:** 8 of 14 | **Level:** 🟡 Intermediate

---

## 🔄 Quick Recap

In Chapter 7 you learned:
- Lists — storing many values in order
- Dictionaries — storing values by name (key-value pairs)
- List of dictionaries — the AI dataset pattern
- How real AI stores detection results and memory

Now let's learn **File Handling** — how Python reads and writes files on your computer or Raspberry Pi. This is how AI **saves data permanently** so it doesn't disappear when the program closes!

---

## 🤔 Why Do We Need File Handling?

Every program you've written so far **loses all data** when it stops running.

Your robot memory from Chapter 7? Gone when you close the terminal.
Your chatbot conversation? Gone.
Your sensor readings? Gone.

**File handling fixes this.** It lets Python:

| Task | Real AI Use |
|------|-------------|
| ✍️ Write to a file | Save sensor readings, log detections |
| 📖 Read from a file | Load a dataset, read a config |
| ➕ Append to a file | Add new data without deleting old |
| 📊 Read CSV files | Load AI training data |

---

## 📖 Reading a File

First, let's create a file to read. On your terminal:

```bash
nano message.txt
```

Type this inside and save:
```
Hello from AITraining!
This is line 2.
Python file handling is powerful.
```

Now read it with Python:

```python
# Open and read the whole file at once
file = open("message.txt", "r")
content = file.read()
file.close()

print(content)
```

Output:
```
Hello from AITraining!
This is line 2.
Python file handling is powerful.
```

> ⚠️ Always `.close()` a file after using it — or use the `with` method below which closes it automatically!

---

## ✅ The `with` Statement — Best Practice

The `with` statement is the **correct way** to handle files. It closes the file automatically, even if something goes wrong:

```python
# ✅ Best practice — always use with
with open("message.txt", "r") as file:
    content = file.read()

print(content)
# File is automatically closed here!
```

From now on, always use `with open(...)`.

---

## 📂 File Modes

When opening a file, you choose a **mode**:

| Mode | Symbol | What it does |
|------|--------|--------------|
| Read | `"r"` | Read an existing file |
| Write | `"w"` | Create a new file (overwrites if exists!) |
| Append | `"a"` | Add to end of existing file |
| Read + Write | `"r+"` | Read and write |

---

## ✍️ Writing to a File

```python
# "w" mode — creates file or OVERWRITES existing file
with open("robot_log.txt", "w") as file:
    file.write("🤖 Robot started\n")
    file.write("✅ Camera initialized\n")
    file.write("✅ Microphone ready\n")

print("Log saved!")
```

This creates `robot_log.txt` with:
```
🤖 Robot started
✅ Camera initialized
✅ Microphone ready
```

> 💡 `\n` means **new line** — without it everything goes on one line!

---

## ➕ Appending to a File

```python
# "a" mode — adds to end without deleting existing content
with open("robot_log.txt", "a") as file:
    file.write("🎙️ Voice module activated\n")
    file.write("🔋 Battery at 87%\n")
```

Now `robot_log.txt` contains:
```
🤖 Robot started
✅ Camera initialized
✅ Microphone ready
🎙️ Voice module activated
🔋 Battery at 87%
```

---

## 📜 Reading Line by Line

For large files, read one line at a time instead of the whole file:

```python
# Read all lines into a list
with open("robot_log.txt", "r") as file:
    lines = file.readlines()

print(f"Total lines: {len(lines)}")

for i, line in enumerate(lines, 1):
    print(f"Line {i}: {line.strip()}")   # .strip() removes the \n at the end
```

Output:
```
Total lines: 5
Line 1: 🤖 Robot started
Line 2: ✅ Camera initialized
Line 3: ✅ Microphone ready
Line 4: 🎙️ Voice module activated
Line 5: 🔋 Battery at 87%
```

> 💡 `.strip()` removes extra spaces and `\n` from the start and end of a string — use this whenever reading lines from a file!

---

## 🛡️ Handling Missing Files

If the file doesn't exist and you try to read it — Python crashes! Fix this with `try / except`:

```python
try:
    with open("data.txt", "r") as file:
        content = file.read()
    print(content)

except FileNotFoundError:
    print("❌ File not found! Creating a new one...")
    with open("data.txt", "w") as file:
        file.write("New file created.\n")
    print("✅ New file created!")
```

This pattern is used in **every real robot program** — check if the log file exists, if not create it.

---

## 📊 Working with CSV Files

CSV (**Comma Separated Values**) is the most common format for AI datasets. Every row is one record, every column is one value, separated by commas.

Example `students.csv`:
```
name,score,grade,city
Aagney,95,A,Vadakara
Rahul,82,B,Kochi
Priya,78,C,Thrissur
Arjun,91,A,Kozhikode
Meera,67,D,Kannur
```

**Writing a CSV file:**

```python
import csv

students = [
    {"name": "Aagney",  "score": 95, "grade": "A", "city": "Vadakara"},
    {"name": "Rahul",   "score": 82, "grade": "B", "city": "Kochi"},
    {"name": "Priya",   "score": 78, "grade": "C", "city": "Thrissur"},
    {"name": "Arjun",   "score": 91, "grade": "A", "city": "Kozhikode"},
    {"name": "Meera",   "score": 67, "grade": "D", "city": "Kannur"},
]

with open("students.csv", "w", newline="") as file:
    writer = csv.DictWriter(file, fieldnames=["name", "score", "grade", "city"])
    writer.writeheader()          # writes the column names
    writer.writerows(students)    # writes all rows

print("✅ CSV file saved!")
```

**Reading a CSV file:**

```python
import csv

with open("students.csv", "r") as file:
    reader = csv.DictReader(file)

    print(f"{'Name':<10} {'Score':<8} {'Grade':<8} {'City'}")
    print("-" * 40)

    for row in reader:
        print(f"{row['name']:<10} {row['score']:<8} {row['grade']:<8} {row['city']}")
```

Output:
```
Name       Score    Grade    City
----------------------------------------
Aagney     95       A        Vadakara
Rahul      82       B        Kochi
Priya      78       C        Thrissur
Arjun      91       A        Kozhikode
Meera      67       D        Kannur
```

This is **exactly** how you load an AI training dataset in real projects!

---

## 🤖 Full Project — Robot Activity Logger

Every real robot keeps a log of what it does. Let's build one!

Create `robot_logger.py`:

```python
# 🤖 Robot Activity Logger — Chapter 8 Project
import csv
from datetime import datetime

LOG_FILE = "robot_activity.csv"
SUMMARY_FILE = "robot_summary.txt"

# ── Functions ─────────────────────────────────

def log_activity(action, status, detail=""):
    """Save one activity to the CSV log"""
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    row = {
        "timestamp": timestamp,
        "action": action,
        "status": status,
        "detail": detail
    }
    # Append to CSV
    try:
        with open(LOG_FILE, "a", newline="") as file:
            writer = csv.DictWriter(file, fieldnames=["timestamp","action","status","detail"])
            writer.writerow(row)
    except:
        # File doesn't exist yet — create with header
        with open(LOG_FILE, "w", newline="") as file:
            writer = csv.DictWriter(file, fieldnames=["timestamp","action","status","detail"])
            writer.writeheader()
            writer.writerow(row)

def read_log():
    """Read and display all activity logs"""
    try:
        with open(LOG_FILE, "r") as file:
            reader = csv.DictReader(file)
            logs = list(reader)

        if not logs:
            print("📭 No activities logged yet.")
            return

        print(f"\n📋 Activity Log ({len(logs)} entries)")
        print("=" * 65)
        for log in logs:
            status_icon = "✅" if log["status"] == "OK" else "❌"
            print(f"{status_icon} [{log['timestamp']}] {log['action']}")
            if log["detail"]:
                print(f"   ↳ {log['detail']}")
        print("=" * 65)

    except FileNotFoundError:
        print("📭 No log file found yet.")

def save_summary():
    """Save a text summary of the session"""
    try:
        with open(LOG_FILE, "r") as file:
            logs = list(csv.DictReader(file))

        total = len(logs)
        ok_count = sum(1 for l in logs if l["status"] == "OK")
        error_count = total - ok_count

        summary = f"""
=== ROBOT SESSION SUMMARY ===
Generated : {datetime.now().strftime("%Y-%m-%d %H:%M:%S")}
Total logs : {total}
Successful : {ok_count}
Errors     : {error_count}
==============================
"""
        with open(SUMMARY_FILE, "w") as file:
            file.write(summary)

        print(f"\n📄 Summary saved to {SUMMARY_FILE}")
        print(summary)

    except FileNotFoundError:
        print("No logs to summarize.")

# ── Main Program ──────────────────────────────

print("=" * 45)
print("  🤖 Robot Activity Logger")
print("=" * 45)

while True:
    print("\nWhat do you want to do?")
    print("  1. Log an activity")
    print("  2. View all logs")
    print("  3. Save summary")
    print("  4. Quit")

    choice = input("\nChoice: ").strip()

    if choice == "1":
        action = input("Action name (e.g. 'Camera scan'): ")
        status = input("Status (OK/ERROR): ").upper()
        detail = input("Detail (optional, press Enter to skip): ")
        log_activity(action, status, detail)
        print("✅ Activity logged!")

    elif choice == "2":
        read_log()

    elif choice == "3":
        save_summary()

    elif choice == "4":
        log_activity("Shutdown", "OK", "User exited program")
        print("\n👋 Goodbye! All activities saved.")
        break

    else:
        print("❌ Invalid choice.")
```

---

## 🏋️ Practice Exercises

**Exercise 1 — Personal Diary**

Build a diary app that:
1. Asks the user to write an entry
2. Saves it to `diary.txt` with today's date
3. Has an option to read all previous entries

```python
from datetime import datetime

def write_entry():
    entry = input("Write your diary entry:\n> ")
    date = datetime.now().strftime("%d-%m-%Y %H:%M")
    # save to diary.txt with date

def read_entries():
    # read and print diary.txt
    pass

# Main menu
while True:
    print("\n1. Write entry  2. Read entries  3. Quit")
    choice = input("Choice: ")
    # complete this...
```

---

**Exercise 2 — Score Tracker**

Build a program that saves student scores to a CSV and can find the highest score:

```python
import csv

def save_score(name, score):
    # append to scores.csv
    pass

def show_highest():
    # read scores.csv and find highest score
    pass

save_score("Aagney", 95)
save_score("Rahul", 88)
save_score("Priya", 91)
show_highest()   # Should print: Aagney — 95
```

---

**Exercise 3 — Fix the bug**

What is wrong here?

```python
with open("notes.txt", "r") as file:
    file.write("New note added!")
```

<details>
<summary>💡 Hint (click to reveal)</summary>

You opened the file in `"r"` (read) mode but tried to write to it! Change to `"a"` to append:

```python
with open("notes.txt", "a") as file:
    file.write("New note added!\n")
```

</details>

---

## 📝 Chapter Summary

| Task | Code |
|------|------|
| Read whole file | `file.read()` |
| Read all lines | `file.readlines()` |
| Write new file | `open("file.txt", "w")` |
| Append to file | `open("file.txt", "a")` |
| Remove `\n` | `line.strip()` |
| Safe open | `try / except FileNotFoundError` |
| Write CSV | `csv.DictWriter` + `writerows()` |
| Read CSV | `csv.DictReader` |
| Get timestamp | `datetime.now().strftime(...)` |
| Always use | `with open(...) as file:` |

---

## ➡️ What's Next?

In **Chapter 9**, you'll learn **Modules and Libraries** — how to use Python's massive collection of ready-made tools. This is the gateway to using `speech_recognition`, `opencv`, `google-generativeai` and all the libraries your robot uses!

[👉 Chapter 9 — Modules and Libraries](./09-modules-and-libraries.md)

---

<div align="center">

**Progress — Book 1: Python for AI**

`✅ Ch1` `✅ Ch2` `✅ Ch3` `✅ Ch4` `✅ Ch5` `✅ Ch6` `✅ Ch7` `✅ Ch8` `⬜ Ch9` `⬜ Ch10` `⬜ Ch11` `⬜ Ch12` `⬜ Ch13` `⬜ Ch14`

---

**⭐ If this helped you, star the repo!**

[← Chapter 7](./07-lists-and-dicts.md) | [Back to Book Index](../README.md) | [Chapter 9 →](./09-modules-and-libraries.md)

</div>
