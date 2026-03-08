# 🎧 AeroMix

> **Interact with your music through hand gestures.**

AeroMix is a low-cost DJ hand gesture recognition glove that lets you apply effects in **Ableton Live** using natural hand movements — no knobs, sliders, or controllers required.

---

## ✨ Demo

[![AeroMix Demo](https://img.youtube.com/vi/f09dZ_bI0Fw/maxresdefault.jpg)](https://youtu.be/f09dZ_bI0Fw)

---

## 🧠 Inspiration

Traditional DJ equipment is expensive and often requires clicking buttons or adjusting sliders on a screen. We wanted to create a more **immersive and expressive** experience — one that lets users physically engage with music rather than just clicking controls in software like Ableton Live.

AeroMix transforms music control into **natural, intuitive movement**.

---

## 🎛️ What It Does

The glove integrates:
- **3 flex sensors** — mounted on the thumb, index, and middle fingers
- **1 ultrasonic distance sensor** — mounted on the palm

Each sensor maps directly to a parameter in Ableton Live:

| Sensor | Gesture | Effect |
|--------|---------|--------|
| 👍 Thumb flex sensor | Curl thumb | Adjusts **track volume** |
| ☝️ Index finger flex sensor | Curl index finger | Controls **reverb** |
| 🖕 Middle finger flex sensor | Curl middle finger | Changes **pitch** |
| 🤚 Palm ultrasonic sensor | Move hand closer/further | Controls **tempo** |

---

## 🔧 How It's Built

### Hardware
- **Arduino Uno R4 WiFi** — main microcontroller for reading and processing sensor data
- **Breadboard** — organizes the circuit and distributes 5V/GND to all components
- Each flex sensor is wired in a **voltage divider circuit** with a 10kΩ resistor for stable analog readings
- A **3D-printed enclosure** houses the Arduino and wiring for portability and durability

### Software
- **Python + PySide6** — desktop application with a live GUI showing real-time sensor readings (progress bars for each finger + ultrasonic distance in cm)
- **Mathematical smoothing pipeline** — filters noisy raw sensor data into clean, normalized 0–1 values
- **`mido` library** — translates sensor values into virtual **MIDI Control Change (CC) commands**
- **ElevenLabs TTS** — guides the user through the calibration process with audio feedback
- **Ableton Live** — receives MIDI input and applies real-time audio effects

### Pipeline
```
Physical Gesture → Arduino → Python App → MIDI (mido) → Ableton Live
                                    ↑
                              ElevenLabs TTS
                           (calibration guidance)
```

---

## 🚀 Getting Started

### Prerequisites
- Python 3.8+
- Arduino IDE
- Ableton Live (with a virtual MIDI loopback driver, e.g. [loopMIDI](https://www.tobias-erichsen.de/software/loopmidi.html) on Windows or IAC Driver on macOS)

### Installation

```bash
# Clone the repository
git clone https://github.com/your-username/aeromix.git
cd aeromix

# Install Python dependencies
pip install -r requirements.txt
```

### Running the App

1. Upload the Arduino sketch to your Arduino Uno R4 WiFi via USB
2. Launch the Python app:
   ```bash
   python main.py
   ```
3. Follow the ElevenLabs voice prompts to calibrate each sensor

### Setting Up Ableton Live

1. Create a new **MIDI track** and import your music into it

**Volume (Thumb)**
1. Import **Utility** into the MIDI track
2. Enter MIDI mapping mode, select **Gain**, then curl your thumb

**Reverb (Index Finger)**
1. Import **Reverb** into the MIDI track
2. Enter MIDI mapping mode, select **Decay**, then curl your index finger

Once mapped, launch your set and start performing! 🎶

---

## 🛠️ Tech Stack

| Technology | Role |
|------------|------|
| Arduino Uno R4 WiFi | Microcontroller / sensor reading |
| Python + PySide6 | Desktop GUI + data processing |
| mido | MIDI output |
| ElevenLabs TTS | Voice-guided calibration |
| Ableton Live 12 | Digital Audio Workstation |
| Flex Sensors (×3) | Finger gesture detection |
| Ultrasonic Distance Sensor | Tempo control via hand distance |

---

## ⚠️ Known Limitations

- Currently requires a **USB connection** between the glove and the host laptop (Bluetooth was attempted but not yet stable)
- Flex sensor readings can be **sensitive** — calibration is important for best results

---

## 🔮 What's Next

- [ ] **Bluetooth connectivity** — eliminate the USB cable for a fully wireless experience
- [ ] **Accelerometer support** — detect rapid hand swings for more expressive DJ interactions
- [ ] Expanded gesture mapping for more Ableton effects

---

## 👥 Team

Built at **MakeUofT**
---

