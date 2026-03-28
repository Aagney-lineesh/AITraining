# 🏗️ Chapter 10 — Classes and OOP

> **Book:** Python for AI | **Chapter:** 10 of 14 | **Level:** 🟠 Intermediate → Advanced

---

## 🔄 Quick Recap

In Chapter 9 you learned:
- How to import built-in modules like `math`, `random`, `datetime`, `os`
- How to install and use external libraries with `pip3`
- How to use `requests` to fetch live data from the internet
- How `speech_recognition` and `pyttsx3` power your voice robot

Now let's learn **Classes and OOP** — the most powerful concept in Python. This is the chapter that separates beginner code from professional AI code!

---

## 🤔 What is OOP?

**OOP** stands for **Object Oriented Programming**.

Everything in the real world is an **object** — a robot, a car, a student, a camera. Every object has:

- **Attributes** — what it *has* (properties, data)
- **Methods** — what it *can do* (actions, functions)

| Object | Attributes | Methods |
|--------|-----------|---------|
| 🤖 Robot | name, battery, speed | move(), speak(), detect() |
| 🚗 Car | brand, color, speed | start(), brake(), honk() |
| 👤 Student | name, age, score | study(), answer(), pass_exam() |
| 📷 Camera | resolution, fps, is_on | capture(), record(), stop() |

A **Class** is the **blueprint** for creating objects.

Think of it like this:

```
Class = Blueprint of a house 🏠
Object = The actual house built from that blueprint
```

One blueprint → many different houses.
One class → many different objects.

---

## ✍️ Creating Your First Class

```python
class Robot:
    pass   # empty class for now
```

Creating an **object** from the class:

```python
robot1 = Robot()
robot2 = Robot()

print(robot1)   # <__main__.Robot object at 0x...>
print(robot2)   # different object, same blueprint
```

---

## 🔧 The `__init__` Method — Setting Attributes

`__init__` is a **special method** that runs automatically when you create a new object. It sets the starting values (attributes):

```python
class Robot:
    def __init__(self, name, battery, speed):
        self.name    = name      # store the name
        self.battery = battery   # store the battery level
        self.speed   = speed     # store the speed

# Create two different robots from the same blueprint
robot1 = Robot("RoboBuddy", 85, 3)
robot2 = Robot("SuperBot",  92, 7)

# Access their attributes
print(robot1.name)      # RoboBuddy
print(robot1.battery)   # 85
print(robot2.name)      # SuperBot
print(robot2.speed)     # 7
```

> 💡 `self` refers to **the object itself**. When you write `self.name = name`, you're storing the name *inside* that specific object. Always write `self` as the first parameter in every method!

---

## ⚙️ Adding Methods — What the Object Can Do

```python
class Robot:
    def __init__(self, name, battery, speed):
        self.name    = name
        self.battery = battery
        self.speed   = speed
        self.is_on   = False        # starts turned off

    def turn_on(self):
        self.is_on = True
        print(f"✅ {self.name} is now ON!")

    def turn_off(self):
        self.is_on = False
        print(f"🔴 {self.name} is now OFF.")

    def speak(self, message):
        if self.is_on:
            print(f"🤖 {self.name} says: '{message}'")
        else:
            print(f"⚠️ {self.name} is off — turn it on first!")

    def check_battery(self):
        if self.battery >= 80:
            status = "🟢 FULL"
        elif self.battery >= 50:
            status = "🟡 GOOD"
        elif self.battery >= 20:
            status = "🟠 LOW"
        else:
            status = "🔴 CRITICAL"
        print(f"🔋 {self.name} battery: {self.battery}%  {status}")

    def charge(self, amount):
        self.battery = min(100, self.battery + amount)
        print(f"⚡ Charged! Battery now at {self.battery}%")

    def status(self):
        state = "ON 🟢" if self.is_on else "OFF 🔴"
        print(f"─── {self.name} Status ───")
        print(f"  Power:   {state}")
        print(f"  Battery: {self.battery}%")
        print(f"  Speed:   {self.speed} m/s")


# ── Using the Robot ───────────────────────────

buddy = Robot("RoboBuddy", 45, 3)

buddy.status()
buddy.speak("Hello!")       # won't work — it's off!
buddy.turn_on()
buddy.speak("Hello! I am ready!")
buddy.check_battery()
buddy.charge(30)
buddy.check_battery()
buddy.turn_off()
buddy.status()
```

Output:
```
─── RoboBuddy Status ───
  Power:   OFF 🔴
  Battery: 45%
  Speed:   3 m/s
⚠️ RoboBuddy is off — turn it on first!
✅ RoboBuddy is now ON!
🤖 RoboBuddy says: 'Hello! I am ready!'
🔋 RoboBuddy battery: 45%  🟠 LOW
⚡ Charged! Battery now at 75%
🔋 RoboBuddy battery: 75%  🟡 GOOD
🔴 RoboBuddy is now OFF.
─── RoboBuddy Status ───
  Power:   OFF 🔴
  Battery: 75%
  Speed:   3 m/s
```

---

## 🌟 The `__str__` Method — Nice Printing

When you `print()` an object, Python shows something ugly like `<Robot object at 0x7f...>`. Fix it with `__str__`:

```python
class Robot:
    def __init__(self, name, battery):
        self.name    = name
        self.battery = battery

    def __str__(self):
        return f"🤖 Robot '{self.name}' | Battery: {self.battery}%"


buddy = Robot("RoboBuddy", 85)
print(buddy)   # 🤖 Robot 'RoboBuddy' | Battery: 85%
```

---

## 🧬 Inheritance — Classes Built from Classes

**Inheritance** lets you create a **child class** that gets all the features of a **parent class**, plus its own extras.

```
Robot (parent)
├── VoiceRobot (child) — has everything Robot has + voice features
├── CameraRobot (child) — has everything Robot has + camera features
└── RescueRobot (child) — has everything Robot has + rescue features
```

```python
# Parent class
class Robot:
    def __init__(self, name, battery):
        self.name    = name
        self.battery = battery
        self.is_on   = False

    def turn_on(self):
        self.is_on = True
        print(f"✅ {self.name} is ON!")

    def check_battery(self):
        print(f"🔋 Battery: {self.battery}%")

    def __str__(self):
        return f"Robot: {self.name}"


# Child class — VoiceRobot
class VoiceRobot(Robot):
    def __init__(self, name, battery, language="English"):
        super().__init__(name, battery)   # call parent's __init__
        self.language = language
        self.words_spoken = 0

    def speak(self, message):
        if self.is_on:
            self.words_spoken += len(message.split())
            print(f"🔊 [{self.language}] {self.name}: '{message}'")
        else:
            print(f"⚠️ Turn on {self.name} first!")

    def speech_stats(self):
        print(f"📊 Words spoken so far: {self.words_spoken}")


# Child class — CameraRobot
class CameraRobot(Robot):
    def __init__(self, name, battery, resolution="1080p"):
        super().__init__(name, battery)
        self.resolution  = resolution
        self.photos_taken = 0

    def capture(self):
        if self.is_on:
            self.photos_taken += 1
            print(f"📸 {self.name} captured photo #{self.photos_taken} at {self.resolution}")
        else:
            print(f"⚠️ Turn on {self.name} first!")

    def camera_stats(self):
        print(f"📷 Photos taken: {self.photos_taken} | Resolution: {self.resolution}")


# ── Using Both ────────────────────────────────

voice_bot  = VoiceRobot("SpeakBot", 90, "Malayalam")
camera_bot = CameraRobot("SnapBot", 78, "4K")

voice_bot.turn_on()           # inherited from Robot!
voice_bot.speak("Namaskaram! Suhkamano?")
voice_bot.speak("Njan ninne sahayikkam!")
voice_bot.check_battery()     # inherited from Robot!
voice_bot.speech_stats()      # VoiceRobot only

print()

camera_bot.turn_on()          # inherited from Robot!
camera_bot.capture()
camera_bot.capture()
camera_bot.capture()
camera_bot.check_battery()    # inherited from Robot!
camera_bot.camera_stats()     # CameraRobot only
```

Output:
```
✅ SpeakBot is ON!
🔊 [Malayalam] SpeakBot: 'Namaskaram! Suhkamano?'
🔊 [Malayalam] SpeakBot: 'Njan ninne sahayikkam!'
🔋 Battery: 90%
📊 Words spoken so far: 5

✅ SnapBot is ON!
📸 SnapBot captured photo #1 at 4K
📸 SnapBot captured photo #2 at 4K
📸 SnapBot captured photo #3 at 4K
🔋 Battery: 78%
📷 Photos taken: 3 | Resolution: 4K
```

> 💡 `super().__init__(...)` calls the **parent class's `__init__`** so you don't have to repeat code!

---

## 🤖 Full Project — Complete AI Robot System

Now let's build a full, professional robot using everything you've learned!

Create `ai_robot_system.py`:

```python
# 🤖 AI Robot System — Chapter 10 Project
import random
import time
from datetime import datetime

class Robot:
    """Base robot class — all robots inherit from this"""

    def __init__(self, name, battery=100, speed=3):
        self.name         = name
        self.battery      = battery
        self.speed        = speed
        self.is_on        = False
        self.activity_log = []

    def _log(self, action):
        """Private method — logs every action with timestamp"""
        timestamp = datetime.now().strftime("%H:%M:%S")
        entry = f"[{timestamp}] {action}"
        self.activity_log.append(entry)

    def turn_on(self):
        self.is_on = True
        self._log("Robot turned ON")
        print(f"✅ {self.name} — Power ON")

    def turn_off(self):
        self.is_on = False
        self._log("Robot turned OFF")
        print(f"🔴 {self.name} — Power OFF")

    def move(self, direction, steps=1):
        if not self.is_on:
            print(f"⚠️ {self.name} is off!")
            return
        self.battery -= steps * 2
        self._log(f"Moved {direction} for {steps} steps")
        print(f"🏃 {self.name} moved {direction} {steps} step(s). Battery: {self.battery}%")

    def charge(self, amount=20):
        self.battery = min(100, self.battery + amount)
        self._log(f"Charged +{amount}%")
        print(f"⚡ {self.name} charged! Battery: {self.battery}%")

    def show_log(self):
        print(f"\n📋 Activity log for {self.name}:")
        print("─" * 40)
        if not self.activity_log:
            print("  No activities yet.")
        for entry in self.activity_log:
            print(f"  {entry}")
        print("─" * 40)

    def status(self):
        state = "🟢 ON" if self.is_on else "🔴 OFF"
        print(f"\n┌── {self.name} ──────────────────┐")
        print(f"│  Status  : {state}")
        print(f"│  Battery : {self.battery}%")
        print(f"│  Speed   : {self.speed} m/s")
        print(f"│  Logs    : {len(self.activity_log)} entries")
        print(f"└──────────────────────────────┘")

    def __str__(self):
        return f"🤖 {self.name} | Battery: {self.battery}% | {'ON' if self.is_on else 'OFF'}"


class AIRobot(Robot):
    """Advanced robot with AI capabilities"""

    RESPONSES = {
        "hello":   ["Hello there! 👋", "Hi! How can I help?", "Hey! Ready to assist!"],
        "time":    None,   # handled dynamically
        "weather": ["It's a beautiful day! 🌤️", "Looks cloudy outside! ☁️", "Sunny and warm! ☀️"],
        "joke":    [
            "Why do robots never get cold? Because they have good fans! 😄",
            "What do you call a robot that always takes the longest route? R2-Detour! 😂",
            "Why did the robot go on a diet? Too many bytes! 🤣"
        ],
        "name":    None,   # handled dynamically
    }

    def __init__(self, name, battery=100, speed=3, ai_model="GeminiNano"):
        super().__init__(name, battery, speed)
        self.ai_model        = ai_model
        self.conversation    = []
        self.objects_detected = []

    def think(self, user_input):
        """Process input and return a response"""
        if not self.is_on:
            return f"⚠️ {self.name} is off!"

        user_input = user_input.lower().strip()
        self.conversation.append({"role": "user", "text": user_input})
        self._log(f"Received input: '{user_input}'")

        # Decide response
        if "hello" in user_input or "hi" in user_input:
            response = random.choice(self.RESPONSES["hello"])

        elif "time" in user_input:
            now = datetime.now().strftime("%I:%M %p")
            response = f"🕐 The current time is {now}."

        elif "name" in user_input or "who are you" in user_input:
            response = f"I am {self.name}, powered by {self.ai_model}! 🤖"

        elif "joke" in user_input:
            response = random.choice(self.RESPONSES["joke"])

        elif "weather" in user_input:
            response = random.choice(self.RESPONSES["weather"])

        elif "battery" in user_input or "charge" in user_input:
            response = f"🔋 My battery is at {self.battery}%."

        elif "bye" in user_input or "stop" in user_input:
            response = f"Goodbye! It was great talking to you! 👋"

        else:
            response = f"Interesting! You said '{user_input}'. I'm still learning! 🧠"

        self.conversation.append({"role": "robot", "text": response})
        self._log(f"Responded to user")
        return response

    def detect_object(self, object_name, confidence):
        """Simulate detecting an object with YOLO"""
        if not self.is_on:
            print(f"⚠️ {self.name} is off!")
            return
        detection = {
            "object":     object_name,
            "confidence": confidence,
            "time":       datetime.now().strftime("%H:%M:%S")
        }
        self.objects_detected.append(detection)
        icon = "✅" if confidence > 0.8 else "⚠️"
        print(f"📷 {icon} Detected: {object_name} ({confidence*100:.1f}% confidence)")
        self._log(f"Detected: {object_name}")

    def detection_report(self):
        if not self.objects_detected:
            print("📭 No objects detected yet.")
            return
        print(f"\n📊 Detection Report — {self.name}")
        print("─" * 45)
        for i, d in enumerate(self.objects_detected, 1):
            bar = "█" * int(d["confidence"] * 10)
            print(f"  {i}. {d['object']:<12} | {bar:<10} | {d['confidence']*100:.0f}%")
        print(f"─" * 45)
        print(f"  Total detections: {len(self.objects_detected)}")

    def chat_history(self):
        print(f"\n💬 Conversation History — {self.name}")
        print("─" * 45)
        for msg in self.conversation:
            icon = "👤" if msg["role"] == "user" else "🤖"
            print(f"  {icon} {msg['text']}")
        print("─" * 45)


# ── Main Program ──────────────────────────────

print("=" * 48)
print("   🤖  AI ROBOT SYSTEM — Chapter 10 Demo")
print("=" * 48)

# Create the robot
robot = AIRobot("RoboBuddy", battery=80, speed=4, ai_model="GeminiNano")
robot.status()

# Boot up
robot.turn_on()

# Simulate some detections
print("\n📷 Running object detection...")
detections = [
    ("person",   0.97),
    ("car",      0.89),
    ("bicycle",  0.73),
    ("dog",      0.91),
    ("person",   0.65),
]
for obj, conf in detections:
    robot.detect_object(obj, conf)
    time.sleep(0.3)

robot.detection_report()

# Chat session
print("\n💬 Starting chat session...")
print("─" * 40)
queries = ["hello", "what is your name", "tell me a joke", "what time is it", "battery level", "bye"]
for query in queries:
    print(f"👤 You: {query}")
    reply = robot.think(query)
    print(f"🤖 {robot.name}: {reply}\n")
    time.sleep(0.4)

# Move around
print("🏃 Testing movement...")
robot.move("forward", 3)
robot.move("left",    2)
robot.move("forward", 2)

# Final report
robot.status()
robot.chat_history()
robot.show_log()
```

---

## 🏋️ Practice Exercises

**Exercise 1 — Student Class**

Build a `Student` class with:
- Attributes: `name`, `age`, `scores` (a list)
- Methods: `add_score(score)`, `average()`, `highest()`, `lowest()`, `grade()`

```python
class Student:
    def __init__(self, name, age):
        self.name   = name
        self.age    = age
        self.scores = []

    def add_score(self, score):
        # add score to the list
        pass

    def average(self):
        # return average of all scores
        pass

    def highest(self):
        # return highest score
        pass

    def grade(self):
        # return A/B/C/D/F based on average
        pass

    def __str__(self):
        # return a nice string representation
        pass

# Test it
s = Student("Aagney", 14)
s.add_score(95)
s.add_score(88)
s.add_score(92)
print(s)
print(f"Average: {s.average()}")
print(f"Grade: {s.grade()}")
```

---

**Exercise 2 — Bank Account**

Build a `BankAccount` class:

```python
class BankAccount:
    def __init__(self, owner, balance=0):
        self.owner   = owner
        self.balance = balance
        self.history = []

    def deposit(self, amount):
        # add amount, log it
        pass

    def withdraw(self, amount):
        # subtract amount if enough balance
        # if not enough, print warning
        pass

    def show_history(self):
        # print all transactions
        pass

# Test
acc = BankAccount("Aagney", 1000)
acc.deposit(500)
acc.withdraw(200)
acc.withdraw(2000)   # should warn: not enough!
acc.show_history()
```

---

**Exercise 3 — Fix the bug**

```python
class Car:
    def __init__(name, color, speed):
        name    = name
        color   = color
        speed   = speed

    def honk():
        print(f"{name} goes BEEP BEEP!")

my_car = Car("Tesla", "red", 120)
my_car.honk()
```

<details>
<summary>💡 Hint (click to reveal)</summary>

Three bugs — all related to missing `self`:

```python
class Car:
    def __init__(self, name, color, speed):   # missing self
        self.name  = name     # missing self.
        self.color = color    # missing self.
        self.speed = speed    # missing self.

    def honk(self):           # missing self
        print(f"{self.name} goes BEEP BEEP!")  # missing self.

my_car = Car("Tesla", "red", 120)
my_car.honk()   # Tesla goes BEEP BEEP!
```

</details>

---

## 📝 Chapter Summary

| Concept | Code | What it means |
|---------|------|---------------|
| Define class | `class Robot:` | Creates a blueprint |
| Constructor | `def __init__(self, ...):` | Runs when object is created |
| Self | `self.name = name` | Stores data inside the object |
| Create object | `r = Robot("Buddy", 85)` | Makes a real object from blueprint |
| Call method | `r.turn_on()` | Runs the method on that object |
| Nice print | `def __str__(self):` | Controls what `print(obj)` shows |
| Inheritance | `class VoiceRobot(Robot):` | Child gets all parent features |
| Call parent | `super().__init__(...)` | Runs parent's constructor |
| Private method | `def _log(self, ...):` | Convention for internal use only |

---

## ➡️ What's Next?

In **Chapter 11**, you'll learn **Error Handling** — how to write programs that never crash, no matter what the user does. This is essential for real robots that run 24/7 without a programmer watching!

[👉 Chapter 11 — Error Handling](./11-error-handling.md)

---

<div align="center">

**Progress — Book 1: Python for AI**

`✅ Ch1` `✅ Ch2` `✅ Ch3` `✅ Ch4` `✅ Ch5` `✅ Ch6` `✅ Ch7` `✅ Ch8` `✅ Ch9` `✅ Ch10` `⬜ Ch11` `⬜ Ch12` `⬜ Ch13` `⬜ Ch14`

---

**⭐ If this helped you, star the repo!**

[← Chapter 9](./09-modules-and-libraries.md) | [Back to Book Index](../README.md) | [Chapter 11 →](./11-error-handling.md)

</div>
