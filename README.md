# Web & Hand-Controlled Mobile Robot using ESP32

A mobile robot controlled in two ways: via a web interface in the browser, or by hand gestures through a camera using computer vision.

## How it works

**Option 1 — Web control:**
ESP32 hosts a web page accessible from any device on the same Wi-Fi. Buttons on the page send HTTP commands to the robot (forward, back, left, right, stop, speed).

**Option 2 — Hand gesture control:**
A Python script reads the camera, detects hand landmarks via MediaPipe, and sends HTTP requests to the ESP32 based on the gesture.

| Gesture | Command |
|---|---|
| Index finger up | Forward |
| Hand turned (thumb right) | Left |
| Hand turned (thumb left) | Right |
| Other | Stop |

## Stack

- **ESP32** — Wi-Fi, web server, motor control
- **L298N** — motor driver
- **Python**, OpenCV, MediaPipe — hand gesture recognition
- **Arduino (C++)** — ESP32 firmware

## Project structure

```
├── esp32_code.ino      # ESP32 firmware: Wi-Fi, web server, motor control
├── hand_control.py     # Python script: gesture recognition via camera
```

## Hardware

- ESP32 dev board
- L298N motor driver
- 2x DC motors
- Power supply for motors

**Motor pin mapping:**

| Motor | Pin1 | Pin2 | Enable (PWM) |
|---|---|---|---|
| Motor 1 | 27 | 26 | 14 |
| Motor 2 | 33 | 25 | 32 |

## Setup

**ESP32:**
1. Open `esp32_code.ino` in Arduino IDE
2. Set your Wi-Fi credentials (`ssid`, `password`)
3. Flash to ESP32
4. Open Serial Monitor to get the IP address

**Python (hand control):**
```bash
pip install opencv-python mediapipe requests
```

Set the ESP32 IP in `hand_control.py`:
```python
ESP32_IP = "http://<your-esp32-ip>"
```

Then run:
```bash
python hand_control.py
```

Press `Esc` to exit.

**Web interface:**
Open `http://<your-esp32-ip>` in any browser on the same network.
