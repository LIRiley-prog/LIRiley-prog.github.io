[Back to Portfolio](./)

Gizmo – Meccanoid AI Assistant
================================

-   **Class:** CSCI 498/499 – Senior Project Design & Implementation/Defense
-   **Grade:** In Progress
-   **Language(s):** Python
-   **Source Code Repository:** [ai_robot](https://github.com/LIRiley-prog/ai_robot)  
    (Please [email me](mailto:Liriley@csustudent.net?subject=GitHub%20Access) to request access.)
-   **Project Documentation:** [CSU-Senior-Project](https://github.com/LIRiley-prog/CSU-Senior-Project)

## Project Description

Gizmo is a capstone senior project that transforms a Meccanoid G15KS toy robot into a fully interactive AI assistant. Powered by a Raspberry Pi 5, Gizmo can hold natural conversations, respond to voice commands, and express itself through physical gestures — waving, nodding, raising its arms, and tilting its head while "thinking."

The robot's brain is powered by OpenAI's GPT-4o model, giving it the ability to answer questions, hold context-aware conversations, and even search the web for real-time information. Vosk provides offline speech recognition, so Gizmo can always listen — even without an internet connection. Speech output is handled through `espeak` text-to-speech synthesis.

On the hardware side, six servo motors (head pan, head tilt, both shoulders, both elbows) are controlled through a PCA9685 servo driver board, with per-servo calibration for precise movement. Drive motors are managed via an L298N motor driver and the Gpiozero library, allowing Gizmo to move forward, backward, and turn.

The project was developed as part of a senior capstone team (Green Team) over two semesters, involving system design, hardware integration, iterative software development, and formal presentations.

## Hardware Components

| Component | Purpose |
|---|---|
| Raspberry Pi 5 | Main controller / AI processing |
| Meccanoid G15KS Body | Physical robot frame with articulated limbs |
| PCA9685 Servo Driver | Controls 6 servos (head, shoulders, elbows) |
| L298N Motor Driver | Controls drive motors for movement |
| USB Microphone | Voice input for speech recognition |
| Speaker | Audio output for text-to-speech |

## Software Architecture

| Library | Role |
|---|---|
| OpenAI API (GPT-4o) | Conversational AI and decision-making |
| Vosk | Offline speech-to-text recognition |
| espeak | Text-to-speech synthesis |
| adafruit-pca9685 | Servo motor control via I2C |
| gpiozero | GPIO-based drive motor control |
| sounddevice | Microphone audio capture |

## How to Run

```bash
# Install dependencies
pip install openai vosk gpiozero adafruit-circuitpython-pca9685 sounddevice

# Run the robot
python main.py

# Optional flags
python main.py --debug      # Verbose logging
python main.py --simulate   # Run without hardware
python main.py --safe       # Restricted movement mode
```

## Voice Interaction

Gizmo is controlled entirely through voice. Once running:

- **Say a wake phrase** — Gizmo wakes up and begins listening
- **Give a movement command** — "move forward," "look left," "wave," "raise arms"
- **Ask a question** — Gizmo uses GPT-4o to respond conversationally
- **Say a sleep phrase** — Gizmo stops listening and parks to a neutral position

Arm movements and gestures are triggered automatically based on conversation context. The terminal displays a real-time log of recognized speech and robot responses.

## Gestures & Animations

Gizmo includes pre-programmed gesture sequences:

- **Wave** — raises and waves one arm
- **Nod** — tilts the head up and down
- **Thinking** — tilts head to one side while processing
- **Raise Arms** — lifts both arms simultaneously
- **Park** — returns all servos to calibrated neutral positions

## Additional Considerations

One of the biggest challenges was integrating multiple hardware components — servos, motors, and a microphone — all running simultaneously without conflicts. Python threading was essential to ensure Gizmo could listen, think, speak, and move at the same time without blocking.

Per-servo calibration was critical since the Meccanoid's original servos have different mechanical ranges. Each servo channel has individually tuned min/max pulse widths and angle limits to prevent damage and ensure smooth motion.

Coordinating the team's work across two semesters required disciplined use of Git, regular status meetings, and iterative design reviews.

[Back to Portfolio](./)
