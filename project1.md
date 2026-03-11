[Back to Portfolio](./)

Hangman
=======

-   **Class:** CSCI 301 – Survey of Scripting Languages
-   **Grade:** B+
-   **Language(s):** C++
-   **Source Code Repository:** [CSCI-301-code-repository](https://github.com/LIRiley-prog/CSCI-301-code-repository)  
    (Please [email me](mailto:Liriley@csustudent.net?subject=GitHub%20Access) to request access.)

## Project Description

This project is a command-line implementation of the classic word-guessing game Hangman, written in C++ as the final project for CSCI 301 – Programming Languages. The program selects a secret word and challenges the player to guess it one letter at a time before running out of attempts.

The project demonstrates core C++ programming concepts including string manipulation, control flow, loops, and user input handling. As the player makes incorrect guesses, the familiar hangman figure is progressively drawn in the terminal, adding a visual element to the game.

## How to Compile and Run the Program

```bash
g++ -o hangman hangman.cpp
./hangman
```

## UI Design

The game runs entirely in the terminal. Upon launch, the program displays a series of blank spaces representing the letters of the secret word. The player is prompted to enter one letter at a time.

- **Correct guess:** The letter is revealed in its correct position(s) in the word.
- **Incorrect guess:** The hangman figure gains a new body part, and the incorrect letter is added to a list of used guesses.
- **Win condition:** The player wins by correctly identifying all letters before the hangman is complete.
- **Lose condition:** After a set number of incorrect guesses, the full hangman is drawn and the secret word is revealed.

The terminal display updates after each guess, showing the current state of the word, the hangman figure, and all previously guessed letters.

## Additional Considerations

This project was developed as part of CSCI 301 – Programming Languages, which introduced students to multiple programming paradigms and languages including Prolog, Perl, Racket, and C++. The Hangman final project served as a comprehensive application of C++ fundamentals learned throughout the course.

[Back to Portfolio](./)
