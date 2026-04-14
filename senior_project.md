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

The robot's brain is powered by OpenAI's GPT-4o-mini model, giving it the ability to answer questions, hold context-aware conversations, and even search the web for real-time information. Vosk provides offline speech recognition, so Gizmo can always listen — even without an internet connection. Speech output is handled through a three-tier TTS system: OpenAI TTS for highest quality, Piper for offline neural synthesis, and espeak as a last-resort fallback.

On the hardware side, eight Meccanoid G15KS Smart Servos (head pan, head tilt, left/right shoulder ×2, left/right elbow) are controlled via a custom 2400-baud bit-bang serial protocol on individual GPIO pins. An LED eye module on GPIO 21 displays state-based colors. Drive motors are managed via an L298N motor driver and the gpiozero library, allowing Gizmo to move forward, backward, and turn.

The project was developed as part of a senior capstone team (Green Team) over two semesters, involving system design, hardware integration, iterative software development, and formal presentations.

## Hardware Components

| Component | Purpose |
|---|---|
| Raspberry Pi 5 | Main controller / AI processing |
| Meccanoid G15KS Body | Physical robot frame with articulated limbs |
| Meccanoid Smart Servos (×8) | Head pan, head tilt, shoulders, elbows — custom 2400-baud serial protocol via GPIO |
| Meccanoid LED Eyes (GPIO 21) | 7-color state indicator (blue=idle, green=speaking, yellow=thinking, red=error) |
| L298N Motor Driver | Controls drive motors for movement |
| USB Microphone | Voice input for speech recognition |
| Speaker | Audio output for text-to-speech |

## Software Architecture

| Library | Role |
|---|---|
| OpenAI API (GPT-4o-mini) | Conversational AI, function calling, and TTS |
| Vosk | Offline speech-to-text recognition |
| Piper TTS | Offline neural text-to-speech (fallback) |
| espeak | Lightweight TTS (last-resort fallback) |
| gpiozero | GPIO pin control for servo bit-banging and motor driver |
| sounddevice | Microphone audio capture |

## How to Run

```bash
# Install dependencies
pip install openai vosk gpiozero sounddevice numpy python-dotenv requests

# Run the robot
python main.py
```

## Voice Interaction

Gizmo is controlled entirely through voice. Once running:

- **Say a wake phrase** — Gizmo wakes up and begins listening
- **Give a movement command** — "move forward," "look left," "wave," "raise arms"
- **Ask a question** — Gizmo uses GPT-4o-mini to respond conversationally
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

The most significant technical challenge was the servo control protocol. The Meccanoid smart servos use a proprietary 2400-baud serial protocol — not standard PWM. A custom bit-bang driver was built using `ctypes` to call the Linux kernel's `clock_nanosleep` for precise timing, which also releases the Python GIL to prevent audio processing from corrupting servo signals.

Per-servo calibration was critical since each servo has different mechanical ranges. Park positions were tuned by hand so Gizmo starts in a natural resting pose without jerking on boot.

Coordinating the team's work across two semesters required disciplined use of Git, regular status meetings, and iterative design reviews.

[Back to Portfolio](./)
