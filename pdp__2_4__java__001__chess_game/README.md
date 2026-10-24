
# Java 001 — Chess Game

**Repository:** `java-001-chess-game`  
**Level:** Beginner+  
**Language:** Java  
**Focus:** Object-Oriented Programming (OOP)

## Project Overview

Build a fully playable two-player chess game in Java using Object-Oriented Programming.

The application runs in the terminal and allows two players to play chess by entering moves.

The project is developed incrementally. Each chapter introduces new Java programming concepts and adds functionality to the existing application.

## Learning Objectives

- Object-Oriented Programming
- Classes and Objects
- Constructors
- Encapsulation
- Inheritance
- Polymorphism
- Method Overriding
- Abstract Classes
- Interfaces
- Composition

## Project Versions

| Version | Chapter | Feature |
|---|---|---|
| V1 | Classes and Objects | Chessboard and pieces |
| V2 | Constructors and Encapsulation | Piece initialization and controlled movement |
| V3 | Inheritance | Chess piece hierarchy |
| V4 | Polymorphism | Individual piece movement rules |
| V5 | Interfaces and Composition | Game architecture |
| V6 | Object-Oriented Rule Design | Complete chess rules |

---

# Chapter 1 — Classes and Objects

## Topics

- Classes
- Objects
- Fields
- Methods
- Object References
- Object Creation

### Task 1.1 — Create a Chess Piece

**New concepts:** Classes, Objects, Fields, Methods

**Assignment:**

1. Create a `Piece` class.
2. Add fields for the piece name and color.
3. Create a method that displays the piece information.
4. Instantiate white and black chess pieces in `Main`.
5. Print their information to the console.

**Example:**

```java
class Piece {
    String name;
    String color;

    void display() {
        System.out.println(color + " " + name);
    }
}
```

**Expected result:**

```text
White King
Black Queen
```

### Task 1.2 — Create the Chessboard

**New concepts:** Object References, Object Arrays, Object Interaction

**Assignment:**

1. Create a `Board` class.
2. Represent the board using an 8×8 array of `Piece` objects.
3. Add a method to place pieces at specified coordinates.
4. Add a method to retrieve a piece from a square.
5. Add a method to display the board.
6. Place two pieces on the board and display their positions.

**Example:**

```java
class Board {
    Piece[][] squares = new Piece[8][8];

    void placePiece(Piece piece, int row, int col) {
        squares[row][col] = piece;
    }

    Piece getPiece(int row, int col) {
        return squares[row][col];
    }
}
```

**Completion criteria:**

- An 8×8 chessboard exists.
- Pieces can be placed on the board.
- Empty squares are represented.
- The board can be displayed in the terminal.

---

# Chapter 2 — Constructors and Encapsulation

## Topics

- Constructors
- Constructor Parameters
- Constructor Overloading
- Access Modifiers
- Private Fields
- Getters
- Encapsulation

### Task 2.1 — Initialize Chess Pieces with Constructors

**New concepts:** Constructors, Constructor Parameters, `this`

**Assignment:**

1. Replace direct field assignment with a constructor.
2. Require every piece to have a name and color.
3. Initialize these fields using `this`.
4. Create multiple pieces using the constructor.
5. Add an overloaded constructor with a default color.

**Example:**

```java
class Piece {
    String name;
    String color;

    Piece(String name, String color) {
        this.name = name;
        this.color = color;
    }
}
```

### Task 2.2 — Encapsulate the Chessboard

**New concepts:** Private Fields, Public Methods, Encapsulation

**Assignment:**

1. Make the board array private.
2. Make the piece fields private.
3. Introduce getters for information that other classes need.
4. Prevent external classes from directly modifying the board array.
5. Add a `movePiece()` method.
6. Reject moves with coordinates outside the board.

**Example:**

```java
public class Board {
    private final Piece[][] squares = new Piece[8][8];

    public Piece getPiece(int row, int col) {
        return squares[row][col];
    }

    public boolean movePiece(
            int fromRow,
            int fromCol,
            int toRow,
            int toCol) {

        // Validate coordinates and perform the move.
        return false;
    }
}
```

**Completion criteria:**

- Board state is protected.
- Pieces are initialized through constructors.
- Moves are performed through public methods.
- Invalid coordinates are rejected.

---

# Chapter 3 — Inheritance

## Topics

- Inheritance
- Superclasses
- Subclasses
- `extends`
- `super`
- Abstract Classes
- Protected Members

### Task 3.1 — Create a Chess Piece Hierarchy

**New concepts:** Inheritance, Superclasses, Subclasses

**Assignment:**

1. Convert `Piece` into an abstract superclass.
2. Create six subclasses:
   - `King`
   - `Queen`
   - `Rook`
   - `Bishop`
   - `Knight`
   - `Pawn`
3. Make each subclass inherit from `Piece`.
4. Use `super()` to initialize inherited properties.
5. Replace generic pieces on the board with specific piece objects.

**Example:**

```java
public abstract class Piece {
    private final String color;

    protected Piece(String color) {
        this.color = color;
    }

    public String getColor() {
        return color;
    }
}

public class King extends Piece {
    public King(String color) {
        super(color);
    }
}
```

### Task 3.2 — Initialize a Complete Chessboard

**New concepts:** Subclass Objects, Inheritance-Based Object Modeling

**Assignment:**

1. Create the standard starting arrangement.
2. Instantiate the correct subclasses for every piece.
3. Place white pieces on ranks 1 and 2.
4. Place black pieces on ranks 7 and 8.
5. Display the complete board.
6. Verify that the board contains 32 pieces.

**Completion criteria:**

- Six distinct chess piece classes exist.
- All pieces inherit from `Piece`.
- The starting chess position is correct.
- Both queens begin on the d-file.

---

# Chapter 4 — Polymorphism

## Topics

- Polymorphism
- Method Overriding
- Abstract Methods
- Dynamic Method Dispatch
- Runtime Polymorphism

### Task 4.1 — Implement Individual Movement Rules

**New concepts:** Abstract Methods, Method Overriding

**Assignment:**

1. Declare an abstract `isValidMove()` method in `Piece`.
2. Override it in each chess piece subclass.
3. Implement the movement pattern of every piece.
4. Prevent pieces from moving outside the board.
5. Prevent a piece from capturing a friendly piece.
6. Use the board to check whether sliding paths are blocked.

**Example:**

```java
public abstract class Piece {
    public abstract boolean isValidMove(
        Board board,
        int fromRow,
        int fromCol,
        int toRow,
        int toCol
    );
}
```

```java
public class Rook extends Piece {
    // Constructor omitted.

    @Override
    public boolean isValidMove(
        Board board,
        int fromRow,
        int fromCol,
        int toRow,
        int toCol
    ) {
        return fromRow == toRow || fromCol == toCol;
    }
}
```

The rook example checks only its movement direction. The complete implementation must also validate the path, destination, and nonzero movement.

### Task 4.2 — Execute Moves Polymorphically

**New concepts:** Runtime Polymorphism, Dynamic Method Dispatch

**Assignment:**

1. Retrieve a `Piece` reference from the board.
2. Call its `isValidMove()` method.
3. Allow Java to select the correct subclass implementation.
4. Execute valid moves.
5. Reject invalid moves.
6. Implement captures.

**Completion criteria:**

- Every chess piece has its own movement rules.
- The board works with `Piece` references.
- Movement rules are selected at runtime.
- Players can move and capture pieces.

---

# Chapter 5 — Interfaces and Composition

## Topics

- Interfaces
- `implements`
- Interface Contracts
- Composition
- Object Collaboration
- Separation of Responsibilities

### Task 5.1 — Create a Chess Game Interface

**New concepts:** Interfaces, Interface Implementation

**Assignment:**

1. Create a `Game` interface.
2. Declare methods for starting, displaying, and running a game.
3. Create a `ChessGame` class implementing the interface.
4. Implement the required methods.
5. Run the application through the interface type.

**Example:**

```java
public interface Game {
    void start();
    void display();
    void run();
}
```

```java
public class ChessGame implements Game {
    @Override
    public void start() {
        // Initialize the game.
    }

    @Override
    public void display() {
        // Display the board.
    }

    @Override
    public void run() {
        // Run the game loop.
    }
}
```

### Task 5.2 — Build the Game Architecture

**New concepts:** Composition, Object Collaboration, Separation of Responsibilities

**Assignment:**

1. Create a `Player` class.
2. Give each player a name and color.
3. Give `ChessGame` a `Board` object.
4. Give `ChessGame` two `Player` objects.
5. Alternate between white and black turns.
6. Accept moves using chess coordinates such as `e2 e4`.
7. Display the updated board after every valid move.
8. Reject attempts to move an opponent's piece.

**Suggested structure:**

```text
src/
└── main/
    └── java/
        └── chess/
            ├── Main.java
            ├── Game.java
            ├── ChessGame.java
            ├── Board.java
            ├── Player.java
            └── pieces/
                ├── Piece.java
                ├── King.java
                ├── Queen.java
                ├── Rook.java
                ├── Bishop.java
                ├── Knight.java
                └── Pawn.java
```

**Completion criteria:**

- Two players can play in the terminal.
- The game alternates turns.
- Players cannot move their opponent's pieces.
- The game is organized into collaborating objects.

---

# Chapter 6 — Object-Oriented Rule Design

## Topics

- Object-Oriented Rule Modeling
- Delegation
- Responsibility Assignment
- Object Collaboration
- Polymorphic Rule Evaluation

### Task 6.1 — Implement Advanced Chess Rules

**New concepts:** Delegation, Responsibility Assignment, Rule Modeling

**Assignment:**

1. Create a `Move` class containing the starting and destination squares.
2. Create a `MoveValidator` class.
3. Delegate legal move validation to `MoveValidator`.
4. Detect whether a king is in check.
5. Reject moves that leave the moving player's king in check.
6. Detect checkmate and stalemate.
7. Implement castling.
8. Implement en passant.
9. Implement pawn promotion.
10. Prevent illegal king captures.

**Suggested additional classes:**

```text
chess/
├── Move.java
├── MoveValidator.java
└── GameStatus.java
```

### Task 6.2 — Complete the Chess Game

**New concepts:** Object Collaboration, Polymorphic Rule Evaluation, Application Integration

**Assignment:**

1. Integrate all previous chapters.
2. Start the application with the standard chess position.
3. Allow two players to enter moves.
4. Validate every move before updating the board.
5. Display captured pieces.
6. Display the current player.
7. Announce check, checkmate, and stalemate.
8. Implement draw conditions, including insufficient material, repetition, and the 50/75-move rules.
9. End the game when a terminal result occurs.
10. Allow players to start a new game.

**Expected console interaction:**

```text
       JAVA CHESS GAME

    a b c d e f g h
  8 r n b q k b n r 8
  7 p p p p p p p p 7
  6 . . . . . . . . 6
  5 . . . . . . . . 5
  4 . . . . . . . . 4
  3 . . . . . . . . 3
  2 P P P P P P P P 2
  1 R N B Q K B N R 1
    a b c d e f g h

White to move.

Enter move: e2 e4

Move accepted.

Black to move.

Enter move: e7 e5

Move accepted.
```

---

# Final Project Requirements

The completed application must support:

- [ ] Object-oriented chess piece hierarchy
- [ ] Standard 8×8 chessboard
- [ ] Two-player gameplay
- [ ] Individual piece movement rules
- [ ] Legal move validation
- [ ] Captures
- [ ] Alternating turns
- [ ] Check detection
- [ ] Checkmate detection
- [ ] Stalemate detection
- [ ] Castling
- [ ] En passant
- [ ] Pawn promotion
- [ ] Draw conditions
- [ ] Restarting a game

## Final Learning Outcome

After completing `java-001-chess-game`, you should be able to design and implement an object-oriented Java application using classes, objects, constructors, encapsulation, inheritance, abstract classes, polymorphism, interfaces, and composition.

**Next project:** `java-002-movie-recommendation-system`

**Next programming chapters:** Collections Framework; Generics; Enumerations; Records; Functional Interfaces; Lambda Expressions; Streams API.
