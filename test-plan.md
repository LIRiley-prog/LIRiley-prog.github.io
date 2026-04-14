Test Plan Document
==================

IDENTIFICATION INFORMATION
--------------------------

### Product

- **Product Name:** Gizmo – AI-Powered Meccanoid Robot Assistant

### Project Description

The Gizmo project transforms a Meccanoid G15KS toy robot into a fully interactive, voice-controlled AI assistant powered by a Raspberry Pi 5. The system combines offline speech recognition (Vosk), conversational AI (GPT-4o-mini with function calling), a three-tier text-to-speech pipeline (OpenAI TTS / Piper / espeak), custom servo motor control via a proprietary 2400-baud serial protocol bit-banged on GPIO pins, and DC drive motor control via an L298N motor driver. The robot responds to verbal commands, performs physical gestures, searches the web for real-time information, and maintains persistent memory across sessions.

### Testing Objectives

The objective of this test plan is to verify that the main functional and non-functional requirements of the Meccanoid AI Assistant are working as intended. Testing ensures:

- Voice commands are recognized accurately.
- AI responses are generated and spoken correctly.
- Servo and motor systems operate safely and reliably.
- Full system integration functions without failure.
- Performance meets response-time requirements.
- The system runs stably over extended periods without memory leaks or deadlocks.

### Features to be Tested

(Referenced from Requirements Document – CSCI 497)

- Speech Recognition Module (Vosk offline STT)
- AI Response Engine (GPT-4o-mini via OpenAI API)
- Three-Tier Text-to-Speech Pipeline (OpenAI TTS, Piper, espeak)
- Custom Servo Protocol Driver (2400-baud GPIO bit-bang)
- Drive Motor Control (L298N H-Bridge, forward/backward)
- Three-Tier Command Parsing Pipeline (NLP correction, fast-path, GPT function calling)
- Persistent Memory System (gizmo_memory.json)
- Full System End-to-End Interaction
- Performance and Stability (4+ hour runtime test)

### Features Not to Be Tested

- **Internet connectivity reliability:** Dependent on external network infrastructure.
- **Third-party API internal logic:** GPT-4o-mini behavior outside scope of project control.
- **Cosmetic shell design of robot:** Focus is on functionality, not aesthetics.


UNIT TEST
---------

### UNIT TEST STRATEGY / EXTENT OF UNIT TESTING:

Unit testing evaluates individual modules independently before integration. An automated test harness (`test_gizmo.py`) mocks all hardware (GPIO, servos, motors) and OpenAI API calls, allowing the full command parsing pipeline to be tested on any machine without physical hardware.

**Test Environment:**
- Hardware: Raspberry Pi 5
- OS: Raspberry Pi OS (Bookworm)
- Python Version: 3.11
- Servo Control: Custom 2400-baud serial protocol via GPIO bit-banging
- Motor Driver: L298N Dual H-Bridge
- Libraries: Vosk, OpenAI SDK, gpiozero, sounddevice, Piper TTS, espeak

### UNIT TEST CASES

| # | OBJECTIVE | INPUT | EXPECTED RESULTS | TEST DELIVERABLES |
| - | --------- | ----- | ---------------- | ----------------- |
| 1 | Verify wake phrase activates Gizmo | "Hey Gizmo" | Gizmo transitions to awake state | Automated test log |
| 2 | Verify sleep phrase deactivates Gizmo | "Goodnight Gizmo" | Gizmo transitions to sleep state | Automated test log |
| 3 | Verify forward movement (fast-path) | "Go forward" | Motor driver engaged, robot moves forward | Automated test log |
| 4 | Verify backward movement (fast-path) | "Go backward" | Motor driver engaged, robot moves backward | Automated test log |
| 5 | Verify turn left (fast-path) | "Turn left" | Left turn motor sequence | Automated test log |
| 6 | Verify turn right (fast-path) | "Turn right" | Right turn motor sequence | Automated test log |
| 7 | Verify stop command (fast-path) | "Stop" | All motors stop | Automated test log |
| 8 | Verify wave gesture (fast-path) | "Wave" | Wave gesture executed | Automated test log |
| 9 | Verify arms up gesture | "Arms up" | Both arms raise | Automated test log |
| 10 | Verify arms down gesture | "Arms down" | Both arms lower | Automated test log |
| 11 | Verify look left gesture | "Look left" | Head pans left | Automated test log |
| 12 | Verify look right gesture | "Look right" | Head pans right | Automated test log |
| 13 | Verify look forward gesture | "Look forward" | Head returns to center | Automated test log |
| 14 | Verify look up gesture | "Look up" | Head tilts up | Automated test log |
| 15 | Verify look down gesture | "Look down" | Head tilts down | Automated test log |
| 16 | Verify celebrate gesture | "Celebrate" | Celebration animation | Automated test log |
| 17 | Verify park gesture | "Park" | All servos return to neutral | Automated test log |
| 18 | Verify volume up | "Volume up" | System volume increases | Automated test log |
| 19 | Verify volume down | "Volume down" | System volume decreases | Automated test log |
| 20 | Verify mute | "Mute" | System volume set to 0% | Automated test log |
| 21 | Verify louder | "Louder" | System volume increases | Automated test log |
| 22 | Verify quieter | "Quieter" | System volume decreases | Automated test log |
| 23 | Verify AI joke request | "Tell me a joke" | GPT-4o-mini generates joke response | Automated test log |
| 24 | Verify time query | "What time is it?" | AI responds with current time | Automated test log |
| 25 | Verify natural gesture request via AI | "Can you do a wave?" | AI calls perform_gesture function | Automated test log |
| 26 | Verify distance command via AI | "Walk 3 feet" | AI calls move_robot with distance | Automated test log |
| 27 | Verify complex NL command via AI | "Look over there to the left" | AI interprets and calls gesture | Automated test log |
| 28 | Verify conversational fallback | "What's the meaning of life?" | AI generates conversational response | Automated test log |
| 29 | Verify commands ignored while sleeping | Command while sleeping | No action taken | Automated test log |
| 30 | Verify NLP self-correction | "Turn left oh wait right" | Corrected to "turn right" | Automated test log |
| 31 | Verify memory system loads | Load gizmo_memory.json | File loads without errors | Automated test log |


REGRESSION TEST
---------------

### Regression Test Strategy

Ensure that previously developed and tested software still performs after change. After any major code or hardware change, core features are retested to make sure nothing previously working has broken.

### Regression Test Cases

| # | OBJECTIVE | INPUT | EXPECTED RESULTS | OBSERVED |
| - | --------- | ----- | ---------------- | -------- |
| 1 | Confirm servo sweep stability after driver refactor | Sweep all 8 servos | No jitter, crash, or signal corruption | All 8 servos swept cleanly — PASS |
| 2 | Confirm speech-to-action mapping after parser update | "Move backward" | Correct motor response | Motor engaged correctly — PASS |
| 3 | Confirm TTS pipeline after FFmpeg EQ changes | Generate speech output | Audio plays with correct EQ profile | Audio quality consistent — PASS |
| 4 | Confirm wake/sleep after idle animation addition | "Hey Gizmo" / "Goodnight Gizmo" | State transitions correct | Transitions correct — PASS |


INTEGRATION TEST
----------------

### Integration Test Strategy and Extent of Integration Testing

Combine individual software modules and test as a group. Integration testing evaluates all integrations between:
- Speech Recognition → AI Engine → Text-to-Speech
- Speech Recognition → Command Parser → Servo/Motor Control
- Hardware + Software interaction across all concurrent threads

All servo chains, motor driver, TTS pipeline, and AI conversation system are tested together to confirm that hardware and software interact correctly under concurrent operation.

### Integration Test Cases

| # | OBJECTIVE | INPUT | EXPECTED RESULTS | TEST DELIVERABLES |
| - | --------- | ----- | ---------------- | ----------------- |
| 1 | Verify voice-to-response pipeline | "Tell me about robotics" | AI response spoken aloud via TTS | Video demo recording |
| 2 | Verify voice-to-action pipeline | "Turn head left" | Head pan servo rotates left | Movement log |
| 3 | Full command sequence (3 commands) | 3 commands in a row | All executed without crash | Test report |
| 4 | Voice recognition at varying distance | Speak at 1, 2, 3 feet | Correct transcription at all distances | STT log file |
| 5 | Multi-turn conversation | 4+ back-and-forth exchanges | Chat history maintains context | Conversation log |
| 6 | Web search integration | "What's the weather?" | Serper API results injected, accurate response | API response log |
| 7 | Mid-speech interruption | Speak while Gizmo is talking | Playback stops within 50ms | Timing measurement |
| 8 | Concurrent servo + TTS operation | Issue gesture during AI response | Servos maintain timing while TTS plays | Thread timing log |
| 9 | Long-duration runtime (4+ hours) | Run Gizmo continuously | No memory leaks, no deadlocks, no servo drift | Runtime log |
| 10 | Network failure recovery | Disconnect Wi-Fi during AI query | Graceful fallback to Piper TTS, error message | Fallback log |
| 11 | Power cycle recovery | Kill process, verify systemd restart | Service restarts cleanly, servos park | Service log |


USER-ACCEPTANCE TEST
--------------------

### User-Acceptance Test Strategy

User Acceptance Testing (UAT) was conducted using observation and verbal feedback. 3 participants (college students, ages 20–25) were given a brief introduction to Gizmo and asked to interact with the robot naturally using voice commands. Participants were observed during the session and provided verbal feedback afterward. Participants were informed about the purpose of the test before participating.

### User-Acceptance Test Cases

| # | TEST ITEM | EXPECTED RESULTS | ACTUAL RESULTS | DATE |
| - | --------- | ---------------- | -------------- | ---- |
| 1 | User says "Hey Gizmo, who are you?" | Robot responds with personality introduction | Gizmo introduced itself with personality | Feb 2026 |
| 2 | User says "Wave at me" | Robot performs wave gesture | Wave gesture executed successfully | Feb 2026 |
| 3 | User says "What's the weather today?" | Robot searches web and speaks current weather | Correct weather reported | Feb 2026 |
| 4 | Multi-command interaction (5 commands) | No system crash, all commands executed | All commands processed without errors | Feb 2026 |
| 5 | User says "Remember my name is [name]" | Robot stores name in persistent memory | Name stored and recalled after restart | Feb 2026 |


Test Deliverables
-----------------

- Test Plan (this document)
- Automated Test Scripts (`test_gizmo.py` — 31 test cases)
- Hardware Diagnostic Scripts (`diag_quick.py`, `test_wiring.py`, `test_motors.py`, `test_arms.py`)
- Test Result Reports (31/31 automated tests passed)
- Demonstration Video Recording


Schedule
--------

| Milestone | Target Date |
| --------- | ----------- |
| Unit Testing Complete | Week 1 |
| Integration Testing Complete | Week 2 |
| System Stability Testing | Week 3 |
| User Acceptance Testing | Week 4 |
| Final Demo Ready | Before March 2, 2026 |


Risks
-----

| Risk | Mitigation Plan | Contingency Plan |
| ---- | --------------- | ---------------- |
| Servo jitter from GIL timing | Use ctypes clock_nanosleep for precise timing | Replace servo with standard PWM model |
| Speech misrecognition / false triggers | Add MIN_WORDS filter and NLP correction pipeline | Reduce vocabulary set |
| Motor overheating during extended use | Limit continuous motor runtime duration | Install cooling fan |
| API latency causing long silence | Pre-cache thinking phrases, parallel API calls | Use local LLM as offline fallback |
| Self-hearing feedback loops | Flush audio queue + cooldown period after speech | Disable microphone during TTS playback |
| Thread deadlocks with 8+ concurrent threads | Use Events, Locks, and Queues consistently | Add watchdog timer to restart hung threads |


Requirements Traceability Matrix
---------------------------------

| Req ID | Requirement | Type | Test Case(s) | Verified |
| ------ | ----------- | ---- | ------------ | -------- |
| FR-1 | Voice Wake/Sleep — Robot wakes on "Hey Gizmo" and sleeps on "Goodnight Gizmo" | Functional | Unit #1, #2, #29, Regression #4 | Yes |
| FR-2 | Conversational AI — Hold natural, multi-turn conversations using GPT-4o-mini | Functional | Unit #23, #24, #28, Integration #5 | Yes |
| FR-3 | Voice Command Execution — Interpret and execute spoken movement and gesture commands | Functional | Unit #3–#7, #25–#27, #30, Integration #2, #3 | Yes |
| FR-4 | Physical Gesture Library — Perform at least 15 distinct physical gestures | Functional | Unit #8–#17, Integration #2 | Yes |
| FR-5 | Web Search — Search the web for real-time information when the query requires it | Functional | Integration #6, UAT #3 | Yes |
| FR-6 | Persistent Memory — Remember user's name, facts, and events across power cycles | Functional | Unit #31, UAT #5 | Yes |
| FR-7 | Text-to-Speech — Speak responses with a consistent, natural-sounding voice | Functional | Integration #1, Regression #3 | Yes |
| FR-8 | Idle Behavior — Perform subtle autonomous animations when idle | Functional | Integration #9 (observed during 4-hr test) | Yes |
| FR-9 | Volume Control — Adjust speaker volume via voice commands | Functional | Unit #18–#22 | Yes |
| FR-10 | Shutdown — Safely shut down via voice command, parking all servos | Functional | Integration #11 | Yes |
| NFR-1 | Response Latency — Simple commands < 2s, AI queries < 5s | Non-Functional | Integration #7 | Yes |
| NFR-2 | Reliability — Run as systemd service with auto-restart | Non-Functional | Integration #11 | Yes |
| NFR-3 | Graceful Degradation — Continue operating if subsystems fail (TTS fallback, servo skip) | Non-Functional | Integration #10, Regression #3 | Yes |
| NFR-4 | Hardware Safety — Perform boot-time hardware safety check and report wiring issues | Non-Functional | Integration #9 (verified during startup) | Yes |


Appendix
--------

- Hardware Wiring: 8 GPIO pins for individual servo chains, L298N motor driver on GPIO
- Servo Protocol: Custom 2400-baud serial, 6-byte packets (header 0xFF + 4 position bytes + checksum)
- Automated test output: 31/31 passed
