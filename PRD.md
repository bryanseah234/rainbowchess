# PRD: rainbowchess

## Overview
A browser-based two-player chess game built with Python (Flask) and served as a web app. Features full chess move validation, pawn promotion, undo (up to 10 moves), move history display, and a rainbow-cycling background animation. Also known as "Skittles Chess Game." Originally deployed on Heroku.

## Goals
- Implement all standard chess piece move rules (King, Queen, Rook, Bishop, Knight, Pawn)
- Validate moves server-side before applying them
- Track and display move history
- Support undo up to 10 previous moves
- Implement pawn promotion (user selects promotion piece)
- Serve via Flask with a rainbow background CSS animation
- Two-player local play (no AI, no networking)

## Non-Goals
- AI opponent
- Online multiplayer
- Time controls / chess clocks
- Opening book or endgame tablebase
- ELO or rating system
- Mobile app

## User Stories
- As two players, we want to play chess in a browser without installing anything.
- As a player, I want to undo my last move if I made a mistake.
- As a new player, I want to see the move history to review the game.

## Tech Stack
- **Language**: Python 3.x
- **Framework**: Flask
- **Frontend**: HTML/CSS/JavaScript (Jinja2 templates)
- **Libraries**: none beyond Flask
- **Deployment**: Heroku (Procfile) / local

## Architecture
```
rainbowchess/
├── main.py          # Flask routes + game session management
├── chess.py         # Chess logic: pieces, board, move validation
├── interface.py     # WebInterface class (UI state object)
├── MoveHistory.py   # Move history tracker + undo stack
├── Procfile         # Heroku deployment
├── requirements.txt
├── pyproject.toml
└── static/          # CSS, JS, images
```

**Classes in chess.py:**
- `BasePiece` — base class with `vector()` helper
- `King`, `Queen`, `Rook`, `Bishop`, `Knight`, `Pawn` — each with `isvalid(start, end)` method
- `WebInterface` — holds UI state (labels, board, winner, error msg)
- `MoveError` — custom exception for invalid moves

**Game flow:**
1. Flask session holds board state as dict
2. Player submits start/end coordinates via form
3. Server validates move via `piece.isvalid()` + capture rules
4. If valid: update board, switch turns, append to history
5. Check win condition (King captured)
6. Return updated board render

## Features (detailed)

### Move Validation
- Each piece class implements `isvalid(start, end)` checking vector geometry
- Blocking check: path must be clear for sliding pieces (Rook, Bishop, Queen)
- Capture rules: can't capture own pieces
- Custom `MoveError` raised on invalid moves

### Pawn Promotion
- On reaching rank 8 (white) or rank 1 (black), user prompted to choose promotion piece
- Defaults or user-selected: Queen, Rook, Bishop, Knight

### Undo
- `MoveHistory.py` maintains a stack of up to 10 board states
- "Undo" route pops last state and restores board
- Clears corresponding history entry

### Move History Display
- Displays algebraic-style notation or coordinate pairs for each move
- Shown alongside the board in UI

### Rainbow Background
- CSS animation cycles hue across background
- Pure CSS, no JS required for the animation

## Data / Config
- Board state stored in Flask session (server-side)
- No database — game resets on session clear or server restart

## Deployment / Run
```bash
pip install flask gunicorn
python main.py          # local dev
gunicorn main:app       # production (Heroku)
```

## Constraints & Notes
- **Local multiplayer only**: no WebSocket or networking — two players share one browser
- **Session-based**: board state in Flask session; refreshing clears the game
- **No check detection**: does not validate whether a move leaves the King in check (simplified rules)
- **Heroku**: Procfile targets `gunicorn` for production; may need platform update for current Heroku stack
