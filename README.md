# Mark DeMayo — Hardware Test & Validation Portfolio

Senior Battery Test Technician (Lucid Motors) • B.S. Electronic Systems Engineering Technology (ABET) — Oct 2025  
San Jose, CA • Email: demayo.markc@proton.me • Phone: (408) 813-0297  
LinkedIn: https://www.linkedin.com/in/demayo-mark • GitHub: https://github.com/demayo-mark/markdemayo.github.io

---

## About
I’m a hardware-focused engineering professional with hands-on experience in bench level tests, high-voltage tests, test execution, debugging, and data-driven validation.

**Core strengths:** Test engineering • Validation • Troubleshooting • Lab instrumentation • Automation mindset

---

## Featured School Projects
---

WiFi-Controlled Autonomous Vehicle (Manual + Sensor Modes)
**Individual Project**
**What it is:** Vehicle that switches between manual drive and autonomous obstacle-avoidance using IR + ultrasonic sensing.  
**Tech:** Arduino, L298N, PWM speed control, IR sensors, ultrasonic sensor, state-based control logic  
**Highlights:**
- Designed mode switching and safety behavior
- Verified sensor-triggered decisions and motor control response
- Tuned thresholds and validated behavior in real environments

**Autonomous Vehicle as Object Follower**


https://github.com/user-attachments/assets/c5019ed8-b64d-4b65-9c5e-7fa9bb188d0f




---

RFID “Chicken Tracker” Capstone (RFID + Sensors + Actuation)
**Group Project**
**What it is:** RFID-based coop monitoring with environment sensing + motion control.  
**Tech:** Mega 2560, MFRC522, LCD, DHT11, stepper motors, water-level sensors  
**Highlights:**
- Integrated multiple sensors and actuators into a coherent system
- Built repeatable tests for sensor read reliability and actuation timing
- Created documentation and diagrams for system design

Schematics
<img width="995" height="1164" alt="image" src="https://github.com/user-attachments/assets/5dff7cc6-31f1-473d-8150-0158027af5d8" />

PCB Design *work in progress*

<img width="728" height="788" alt="image" src="https://github.com/user-attachments/assets/18b6226e-c4e1-4346-b347-3725562bf4e8" />

---
## Personal Projects 


**Latest Chapter Notification** - work in progress
```python
import re, time, requests
from bs4 import BeautifulSoup
from winotify import Notification

URL = input("Chapter list URL: ").strip()
MINUTES = int(input("Check every how many minutes? ").strip())
STATE_FILE = "last_seen.txt"

CHAPTER_RE = re.compile(r"(?:chapter|ch)\D*(\d+(?:\.\d+)?)", re.I)

def toast(msg):
    Notification(app_id="Manga Notifier", title="New chapter!", msg=msg).show()

def get_latest_chapter(url):
    html = requests.get(url, timeout=30).text
    soup = BeautifulSoup(html, "html.parser")

    nums = []
    for a in soup.find_all("a"):
        s = (a.get("href","") + " " + a.get_text(" ", strip=True))
        m = CHAPTER_RE.search(s)
        if m:
            nums.append(float(m.group(1)))

    return max(nums) if nums else None

def load_last():
    try:
        return float(open(STATE_FILE, "r").read().strip())
    except:
        return 0.0

def save_last(x):
    open(STATE_FILE, "w").write(str(x))

last = load_last()
print("Last seen:", last)

while True:
    latest = get_latest_chapter(URL)

    if latest is None:
        print("Couldn't detect chapters on the page.")
    elif last == 0.0:
        last = latest
        save_last(last)
        print("Initialized to:", last)
    elif latest > last:
        toast(f"Chapter {latest} is out! (was {last})")
        print("NEW:", latest)
        last = latest
        save_last(last)
    else:
        print("No update. Latest:", latest)

    time.sleep(MINUTES * 60)

```

---

## Skills & Tools
**Test Equipment:** Oscilloscope • DMM • LCR • Power supplies • Hi-Pot • Environmental test equipment  
**Software/Tools:** Jira • Confluence • JMP • Multisim • Fritzing • CAN tools • CAD
**Programming/Scripting:** Python • Shell (basic) • Embedded C/C++ (Arduino)

---

## How I Work
- Requirements → design → build → bring-up → debug → validate → document
- I prioritize **repeatable tests**, **clear measurements**, and **root-cause reasoning**

---

## Contact
If you want to talk hardware validation, test engineering, or lab automation:  
📧 demayo.markc@proton.me • 📍 San Jose, CA
