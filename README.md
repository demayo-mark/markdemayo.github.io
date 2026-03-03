# Mark DeMayo — Hardware Test & Validation Portfolio

Senior Battery Test Technician (Lucid Motors) • B.S. Electronic Systems Engineering Technology (ABET) — Oct 2025  

Located: San Fransico Bay Area

Email: demayo.markc@proton.me 

LinkedIn: https://www.linkedin.com/in/demayo-mark 

GitHub: https://github.com/demayo-mark/markdemayo.github.io

---

## About
I’m a hardware-focused engineering professional with hands-on experience in bench level tests, high-voltage tests, test execution, debugging, and data-driven validation.

**Core strengths:** Test engineering • Validation • Troubleshooting • Lab instrumentation • Automation mindset

---

## Featured School Projects
---

WiFi-Controlled Autonomous Vehicle (Manual + Sensor Modes)

**<ins>Individual Project</ins>**

**Overview:** Vehicle that switches between manual drive and autonomous obstacle-avoidance using IR + ultrasonic sensing

**Components:** Arduino, L298N, PWM speed control, IR sensors, ultrasonic sensor, state-based control logic  

**Highlights:**
- Designed mode switching and safety behavior
- Verified sensor-triggered decisions and motor control response
- Tuned thresholds and validated behavior in real environments

**Autonomous Vehicle as Object Follower**

Brief video of my vehicle reacting to an object in front of it 

https://github.com/user-attachments/assets/c5019ed8-b64d-4b65-9c5e-7fa9bb188d0f




---

## RFID “Chicken Tracker” Capstone (RFID + Sensors + Actuation)

**<ins>Group Project</ins>**

**Overview:** RFID-based coop monitoring with environment sensing + motion control

**Components:** Mega 2560, MFRC522, LCD, DHT11, stepper motors, water-level sensors  

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


**Latest Chapter Notification** 
```python
import re
import time
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin
from winotify import Notification, audio

# Hardcoded VIZ chapter list
SERIES_URL = "https://www.viz.com/shonenjump/chapters/dandadan"
BASE_URL = "https://www.viz.com"

MINUTES = int(input("Check every how many minutes? ").strip())
STATE_FILE = "last_seen_dandadan.txt"

HEADERS = {
    "User-Agent": (
        "Mozilla/5.0 (Windows NT 10.0; Win64; x64) "
        "AppleWebKit/537.36 (KHTML, like Gecko) "
        "Chrome/120.0 Safari/537.36"
    )
}

# Pull chapter number from the chapter URL path 
CHAPTER_HREF_RE = re.compile(r"/shonenjump/dandadan-chapter-(\d+(?:\.\d+)?)/", re.I)

def toast_new_chapter(ch_num: float, ch_url: str):
    t = Notification(
        app_id="Manga Notifier",
        title="Dandadan: New chapter!",
        msg=f"Chapter {ch_num} is out."
    )
    t.set_audio(audio.Mail, loop=False)
    # Clickable button that opens the chapter in your browser
    t.add_actions(label="Open on VIZ", launch=ch_url)
    t.show()

def get_latest_chapter():
    r = requests.get(SERIES_URL, headers=HEADERS, timeout=30)
    r.raise_for_status()

    soup = BeautifulSoup(r.text, "html.parser")

    found = []  # (chapter_num, chapter_url)
    for a in soup.find_all("a", href=True):
        href = a["href"]
        m = CHAPTER_HREF_RE.search(href)
        if not m:
            continue
        ch_num = float(m.group(1))
        ch_url = urljoin(BASE_URL, href)
        found.append((ch_num, ch_url))

    return max(found, key=lambda x: x[0]) if found else None

def load_last():
    try:
        with open(STATE_FILE, "r", encoding="utf-8") as f:
            return float(f.read().strip())
    except:
        return 0.0

def save_last(x: float):
    with open(STATE_FILE, "w", encoding="utf-8") as f:
        f.write(str(x))

last = load_last()
print("Last seen:", last)

while True:
    try:
        latest = get_latest_chapter()

        if latest is None:
            print("Couldn't detect chapters on the page.")
        else:
            latest_num, latest_url = latest

            if last == 0.0:
                last = latest_num
                save_last(last)
                print("Initialized to:", last)
            elif latest_num > last:
                toast_new_chapter(latest_num, latest_url)
                print("NEW:", latest_num, latest_url)
                last = latest_num
                save_last(last)
            else:
                print("No update. Latest:", latest_num)

    except Exception as e:
        print("Check failed:", e)

    time.sleep(MINUTES * 60)
```

---

## Skills 

**Test Equipment:** Oscilloscope • DMM • LCR • Power supplies • Hi-Pot • Environmental test equipment • CANoe/CANanalyzer 

**Software/Tools:** Jira • Confluence • JMP • Multisim • Fritzing • CAN tools • CAD

**Programming/Scripting:** Python • Shell (basic) • Embedded C/C++ (Arduino) • LabView

---

## How I Work

- Requirements → Design → Build → Bring-up → Debug → Validate → Document
- I prioritize **Repeatable tests**, **Clear measurements**, and **Root-cause reasoning**

---

## Hobbies
- Weightlifting
- Gaming
- Building Gundam Model Kits

![IMG_0275](https://github.com/user-attachments/assets/5b51d109-6858-44f1-a0da-bd5fb4795c9b)
![IMG_0345](https://github.com/user-attachments/assets/3045bb62-a0b6-421c-b2a1-34d4e5ac693f)
![IMG_1067](https://github.com/user-attachments/assets/77773533-1d42-48cc-8d6e-2ac7453cadc9)
![IMG_1858](https://github.com/user-attachments/assets/c1b5b023-d8de-4ec9-ae9b-b1af51436db8)


---


## Contact
If you want to talk hardware validation, test engineering, or lab automation:  
📧 demayo.markc@proton.me • 📍 San Jose, CA
