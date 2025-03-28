# TIC-TAC-TOE
Below is an example README file you can include with your project. You can copy the content into a file named `README.md` in your project directory.

---

- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
  - [Starting the Server](#starting-the-server)
  - [Starting a Player (Client)](#starting-a-player-client)
- [How It Works](#how-it-works)
  - [Server Code Overview](#server-code-overview)
  - [Player Code Overview](#player-code-overview)
- [Notes and Improvements](#notes-and-improvements)
- [License](#license)

## Features

- **Two-player gameplay:** Two players can connect to the server and play against each other.
- **Graphical User Interface:** Uses Pygame for rendering the game board, moves, and messages.
- **Real-time network communication:** Sockets are used to send and receive game data between the server and players.
- **Basic game logic:** Handles alternating turns, move validation (with basic checks), and win/draw conditions.

## Requirements

- **Python 3.6+**
- **Pygame:** Used for GUI development.
- **Socket:** The standard Python library for network communication.
- (Optional) **pickle:** Imported in the code for potential serialization purposes, though not used in the current version.

## Installation

1. **Clone the repository or download the source code:**

   ```bash
   git clone <repository_url>
   cd TIC-TAC-TOE-main
   ```

2. **Install the required Python packages.** For Pygame, run:

   ```bash
   pip install pygame
   ```

   _Note: The `socket` and `pickle` modules are part of Python's standard library, so no additional installation is needed for them._

## Usage

### Starting the Server

1. Open a terminal or command prompt.
2. Navigate to the directory containing your scripts.
3. Run the server script:

   ```bash
   python server.py
   ```

   The server will bind to port `9999` (or the port specified in the code) and wait for two client connections.

### Starting a Player (Client)

1. Open another terminal or command prompt.
2. Navigate to the directory containing your scripts.
3. Run the player (client) script:

   ```bash
   python player.py
   ```

4. When prompted, enter the server IP address. For local testing, use `127.0.0.1` or `localhost`.

5. Repeat the process in a separate terminal for the second player.

Once both players are connected, the game will begin, and you will see the Tic Tac Toe board in a Pygame window. Follow the on-screen prompts to make your moves by clicking within the board boundaries.

## How It Works

### Server Code Overview

- **Socket Initialization:**  
  The server creates a socket, binds to port `9999` (or another specified port), and listens for two incoming connections.

- **Player Connection:**  
  It accepts two player connections, assigns each a player number (Player 1 or Player 2), and notifies them.

- **Game Logic:**  
  The server maintains a 3x3 game matrix. It alternates between players by prompting for moves using a basic communication protocol (sending messages like `"Input"`, `"Matrix"`, and `"Over"`).
  
- **Winner Check:**  
  After each move, the server checks for a winner using row, column, and diagonal comparisons. Once a winner is determined or the board is full, it sends an end-of-game message.

### Player Code Overview

- **Socket Connection:**  
  Each client creates a socket and connects to the server at the given IP address and port.
  
- **Pygame GUI:**  
  The player script uses Pygame to create the game window, draw the Tic Tac Toe grid, and display messages. It handles mouse events to capture player moves.
  
- **Communication Protocol:**  
  The client listens for server messages (e.g., `"Input"`, `"Matrix"`, `"Error"`, `"Over"`) and responds accordingly. When a move is allowed, the player clicks on the board, and the client sends the coordinates back to the server.

- **Multithreading:**  
  The script uses a separate thread to handle incoming messages so that the main thread can focus on rendering the game window and handling user input.

## Notes and Improvements

- **Error Handling:**  
  Both server and client scripts include basic error handling. You might consider adding more robust error detection and handling for production use.

- **Input Validation:**  
  The server currently has disabled input validation to reduce latency. Consider enabling and enhancing validation for better game robustness.

- **Serialization:**  
  Although the `pickle` module is imported, it is not used in the current version. In future iterations, you might serialize complex game objects or state using `pickle` for easier transmission between server and client. _Note: Always use caution with pickle, as it can execute arbitrary code when loading untrusted data._

- **Security:**  
  This project is designed for local or controlled network environments. For public or production use, implement additional security measures.

## License

This project is provided under the [MIT License](LICENSE).

---
