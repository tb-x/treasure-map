# Treasure Map

A printable maths treasure hunt for young kids (around age 5). The page makes a riddle sheet: a grid board
with a start dot in one corner, and a row of arrow cards. Each card has a small sum; its answer says how many
squares to move in the arrow's direction. Follow every card and you land on the treasure. The sheet has no
words, so it works for kids who can't read yet. The answer is hidden in a QR code: scan it with a phone camera
and a page shows the way to the treasure.

Live at **https://tb-x.github.io/treasure-map/**

## How it plays

- Print a sheet (one riddle per A4 page). Each sheet is a different riddle.
- Start on the green dot.
- Take the cards in reading order: left to right, then the next row.
- Solve the sum on the card, write the answer in the empty box, and move that many squares the way the arrow points.
- When the cards run out, the square you're on hides the treasure. Mark it, or say its letter and number (like F3).
- Scan the QR code next to the chest. Tap the green play button and a marker walks the path square by
  square (with a little beep for each one), then the chest appears with its square's name.

Every move stays on the board and goes at least one square. The path can cross itself and can double back,
but never just undoes the move before.

## The maker page

- **Board size**: 5 to 15 squares a side. Columns are lettered from A, rows are numbered from 1 at the top.
- **Moves**: 3 to 16 arrow cards. With 8 or fewer the cards print bigger.
- **Biggest number**: no number in a sum, and no running total along the way, goes above this (5 to 50).
  A single move is never longer than the board allows, so on a 10×10 board every answer is 1 to 9.
- **Longer sums**: Never, Sometimes (about 1 in 4) or Often (about 1 in 2) a sum has 3 or 4 numbers,
  like 5 + 4 − 3 + 1.
- **Start corner**: a fixed corner, or any corner.
- **Sheets**: how many different riddles to print at once (up to 20).
- **New maps** makes new riddles for all sheets, ↻ on a sheet makes a new one for that sheet only, and
  **Print** prints them. The settings are remembered in this browser.
- Clicking a sheet's QR code on screen opens its answer page.

The QR code holds the whole riddle in the link (board size, start and moves, e.g.
`#n=10&s=0.9&m=U2R4U4L3D2R6U3L2`). Nothing is stored anywhere, so a printed sheet keeps working for as long
as this page is online. The QR always points at the published page on GitHub Pages, even when the maker runs
on a local server.

## Running it

It's a single `index.html` with no build step. Serve the folder and open it:

```bash
python -m http.server 5213
```

Then go to http://localhost:5213/. Opening `index.html` straight from disk works too. The QR codes are made
by [qrcode-generator](https://github.com/kazuhikoarase/qrcode-generator) 1.4.4 (MIT), loaded from cdnjs.

After the first visit the page also works offline and can be added to a phone's Home Screen.

## Tuning knobs

Named constants at the top of the script in `index.html`:

| Constant | Default | What it does |
| --- | --- | --- |
| `DEFAULTS` | 10×10, 8 moves, numbers to 20, longer sums sometimes, any corner, 1 sheet | Starting settings |
| `SIZE_MIN` / `SIZE_MAX` | 5 / 15 | Allowed board sizes |
| `MOVES_MIN` / `MOVES_MAX` | 3 / 16 | Allowed number of arrow cards (16 is what fits on A4) |
| `MAXNUM_MIN` / `MAXNUM_MAX` | 5 / 50 | Allowed range for the biggest number |
| `LONG_CHANCE` | 0, 0.25, 0.5 | Share of 3- and 4-number sums for Never / Sometimes / Often |
| `SAME_DIR_WEIGHT` | 0.35 | How likely an arrow repeats the one before (1 = as likely as turning) |
| `BACK_DIR_WEIGHT` | 0.6 | How likely an arrow points straight back |
| `MIN_TREASURE_DIST` | 3 | Squares between the start and the treasure, at least |
| `PUBLIC_URL` | `https://tb-x.github.io/treasure-map/` | Where the QR codes point |
| `WALK_MS` / `STEP_PAUSE_MS` | 260 / 350 | Answer page: time per square and pause between arrows |
