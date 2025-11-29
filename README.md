# Rainbow Chess

A web-based chess game with a colorful rainbow-cycling background.

## Description

Rainbow Chess (also known as Skittles Chess Game) is a two-player chess game built with Python and Flask. It features a fully functional chess board with move validation, pawn promotion, and an undo feature that allows players to revert up to 10 moves. The game showcases a visually appealing interface with a rainbow color-cycling background effect.

## Features

- Interactive chess board with Unicode chess piece symbols
- Move validation for all chess pieces (King, Queen, Rook, Bishop, Knight, Pawn)
- Pawn promotion to Queen, Rook, Bishop, or Knight
- Undo functionality with a circular stack that stores up to 10 moves
- Rainbow color-cycling background animation
- Responsive web interface

## Technologies Used

- Python 3.8
- Flask (web framework)
- Jinja2 (templating engine)
- HTML/CSS/JavaScript
- Gunicorn (WSGI HTTP Server)

## Installation

```bash
# Clone the repository
git clone https://github.com/bryanseah234/rainbowchess.git

# Navigate to project directory
cd rainbowchess

# Install dependencies
pip install -r requirements.txt
```

## Usage

```bash
# Run the application
python main.py
```

The game will start on `http://localhost:5000`. Open your browser and navigate to this address to play.

### How to Play

1. Click "START" to begin a new game
2. Enter moves in the format `XY XY` (e.g., `01 03` to move a piece from column 0, row 1 to column 0, row 3)
3. Coordinates are 0-7 for both columns and rows
4. Use the "UNDO" button to revert moves if needed

## Demo

The game was originally hosted at: http://skittles-chessapp.herokuapp.com/

## Disclaimer

1. FOR EDUCATIONAL PURPOSES ONLY
2. USE AT YOUR OWN DISCRETION

## License

MIT License

---

**Author:** <a href="https://github.com/bryanseah234">bryanseah234</a>
