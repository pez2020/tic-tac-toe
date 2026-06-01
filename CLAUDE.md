# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the Game

Open `tictactoe.html` directly in any browser — no build step, no server, no dependencies. On Windows: `start tictactoe.html`.

## Architecture

Everything lives in a single file (`tictactoe.html`) with inline CSS and JS — no frameworks, no modules, no bundler.

**Game state** (module-level globals):
- `board` — flat 9-element array (`null | 'X' | 'O'`), indexed 0–8 left-to-right, top-to-bottom
- `current` — whose turn it is (`'X'` or `'O'`)
- `gameOver` — boolean gate; blocks clicks after a result
- `scores` — `{ X, O, tie }` object, persists across `init()` calls
- `vsComputer` — toggles AI mode; O is always the AI player

**Key functions:**
- `init()` — resets board/state, preserves scores
- `checkWinner(b)` — checks `WINS` (8 hard-coded winning triples) against board array; returns `{ winner, line }` or `null`
- `applyMove(index, player)` — writes to `board[]` and updates the DOM cell
- `minimax(b, isMax)` — recursive minimax; O maximises (+10), X minimises (−10), tie = 0
- `bestMove()` — iterates empty cells, calls `minimax`, picks highest-scored move for O
- `handleClick(e)` — entry point for all user interaction; triggers AI move via `setTimeout(300ms)` after player move

**DOM binding:** cells use `data-i` attributes (0–8) as the bridge between board array and DOM. `.taken` class blocks re-clicks; `.win` class triggers the pulse animation on winning cells.

## GitHub

Commit and push to GitHub regularly with clean, descriptive commit messages so no progress is ever lost. The remote is `https://github.com/pez2020/tic-tac-toe`.

```
git add <files>
git commit -m "Short description of what changed and why"
git push
```

Commit after every meaningful change — new feature, bug fix, or significant edit — not just at the end of a session.
