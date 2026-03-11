[Back to Portfolio](./)

AI Robot – Senior Project
==========================

-   **Class:** CSCI 499 – Senior Project Implementation/Defense
-   **Grade:** In Progress
-   **Language(s):** Python
-   **Source Code Repository:** [ai_robot](https://github.com/LIRiley-prog/ai_robot)  
    (Please [email me](mailto:Liriley@csustudent.net?subject=GitHub%20Access) to request access.)

## Project Description

The AI Robot project is a capstone senior project built using a Meccanoid G15KS robot body controlled by a Raspberry Pi 5. The robot can hold a conversation, respond to voice commands, and move its arms using servo motors.

The software is written in Python and uses several libraries to handle different parts of the project. OpenAI's API is used to generate intelligent responses to whatever the user says. Vosk handles offline speech recognition so the robot can understand spoken commands without needing an internet connection to listen. The robot's servo motors are controlled through a PCA9685 board, and wheel movement is managed using the Gpiozero library.

The project was developed collaboratively as part of a senior capstone team (Green Team) and involved planning, designing, and presenting the system over two semesters.

## How to Compile and Run the Program

```bash
pip install openai vosk gpiozero adafruit-circuitpython-pca9685
python main.py
```

## UI Design

The robot is controlled entirely through voice. Once running:

- **Say a wake phrase** — the robot wakes up and begins listening
- **Ask a question or give a command** — the robot processes it and responds out loud using text-to-speech
- **Say a sleep phrase** — the robot stops listening and goes idle

Arm movements are triggered automatically based on the conversation context. The terminal shows a log of what the robot heard and how it responded.

## Additional Considerations

One of the biggest challenges was integrating multiple hardware components — servos, motors, and a microphone — all running at the same time without conflicts. Managing threads in Python was important to make sure the robot could listen and respond simultaneously without freezing up. Coordinating the team's work across two semesters also required using Git and holding regular status meetings.

[Back to Portfolio](./)
