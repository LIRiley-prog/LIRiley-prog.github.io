[Back to Portfolio](./)

Connect Four
============

-   **Class:** CSCI 325 – Object-Oriented Programming
-   **Grade:** C+
-   **Language(s):** Java (Swing GUI)
-   **Source Code Repository:** [Connect_Four](https://github.com/LIRiley-prog/Connect_Four)  
    (Please [email me](mailto:Liriley@csustudent.net?subject=GitHub%20Access) to request access.)

## Project Description

Connect Four is a fully playable two-player strategy game built in Java using the Swing GUI framework. The project recreates the classic token-dropping board game where two players take turns dropping colored pieces into a 6-row, 7-column vertical grid. The first player to align four of their pieces horizontally, vertically, or diagonally wins the game.

The application features a graphical menu system, player name and color selection with input validation, a live game board, and an end screen with replay functionality. A powerup system was also designed into the architecture, allowing for extended gameplay features such as piece swapping and random moves.

The project is organized under the `csu.csci325` package and structured across multiple Java classes to separate concerns: menu logic, game state, powerup behavior, and end-game handling.

## How to Compile and Run the Program

Compile and run using any Java IDE (such as IntelliJ IDEA or Eclipse), or from the command line:

```bash
javac *.java
java ConnectFour
```

## UI Design

The game opens with a **main menu window** containing two buttons: **Start** and **Rules**. Players enter their names and select their token colors before the game begins.

**During gameplay:**
- The board is rendered graphically as a grid of circles
- Players click to drop their token into a column
- The board updates in real time after each move
- Invalid moves (full column) are handled gracefully

**After the game ends:**
- An **End Screen** displays the winner
- Players can choose to **Restart** the game or **Exit** the application

**Menu validation:** The `MenuLogic` class ensures players cannot select the same color, preventing confusion during play.

## Additional Considerations

This project demonstrates object-oriented design principles in Java, including class decomposition, event-driven programming with Swing listeners, and input validation. The `Powerup` class was architected to support future feature expansion, showcasing forward-thinking software design.

[Back to Portfolio](./)
