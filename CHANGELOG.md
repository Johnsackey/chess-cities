# Chess Cities — changelog

## R36 (2026-10-22): Motif School — four attacking ideas
- **Tactics Motif School grows from 16 to 20 motifs.** A new "Attacking ideas" section (marked New) sits under "Core motifs" and "Advanced ideas":
  - **🎯 Attacking f2 / f7**: early in the game only the king guards f7 (f2 for White). Source: Wikipedia "Fried Liver Attack", with a history note: 6.Nxf7 was already played in Polerio vs. Domenico, Rome, about 1610.
  - **👑 Exposed King**: chase a king with no pawn shelter with checks until a fork, skewer or mating net appears. Source: Wikipedia "Chess strategy" (king safety).
  - **♛ Promotion**: clear the path or decoy the one piece that stops the pawn; includes an underpromotion to a knight with a fork. Source: Wikipedia "Promotion (chess)", with a history note on promotion in chaturanga.
  - **💥 Sacrifice**: give up material for mate or more material back, then follow with forcing moves. Source: Wikipedia "Sacrifice (chess)".
- Each has a lesson (the idea, how to spot it, a mini-board, a "Read more" source link) and **8 real Lichess puzzles (CC0)**, ordered from about 770 to about 1400 (Lichess themes `attackingF2F7`, `exposedKing`, `promotion`, `sacrifice`; popularity ≥85, ≥300 plays).
- **Verification:** every solver move re-checked with Stockfish at depth 14, using the same rule as R15 and R31 (best move or within 0.6 pawn, still ≥2 pawns up or mate). All 32 puzzles are new to the app: no puzzle id or position is shared with the daily set, any city, Pattern Academy or the 16 earlier motifs, and no two new puzzles share a position. Only the Promotion set uses promotion puzzles. Data tools are in `/workspace/cc36` (`cand.py`, `sel.py`).
- The "New" tag moved from "Advanced ideas" to "Attacking ideas". New cards are keyboard-focusable like the rest.
- **Storage unchanged:** progress reuses `ST.acad.mot[id]` inside `cc2_state`. There are no new keys or fields. An R35 save writes exactly what R35 itself writes after browsing the school, and an R36 save with new-motif progress still opens in R35 (R35 shows its 16 motifs and keeps the extra progress).
- **Other trainers unchanged:** the new puzzles live in `MOTPUZ36`, so the position pool used by the Calculation and Pawn/Plans quizzes is identical to R35.
- **Shadow mode and gate unchanged:** `ST.prefs.shadow !== false` by default; gate stays `passed: false`; R28 freezes intact (new-motif stars are logged as would-have awards in shadow mode).
- The Settings label reads "build R36"; `window.CC_BUILD='R36'`. New files: `v15data.js`, `v15.js` (build order: `… v14data.js v14.js v15data.js v15.js`). New test: `cc-test/t36.js` (8 checks); the R31 test copy now expects 20 motifs in 3 sections.

## R35 (2026-10-21): Visualization Gym — Knight Maze, plus a tap-the-square fix
- **New Gym drill: 🐴 Knight Maze** (marked New), with 12 mazes that unlock in order. Your white knight must capture every black pawn in as few hops as possible, without ever landing on a square a pawn guards. Black pawns capture one square diagonally down the board, so a pawn protected by another pawn can only be taken once its guard is gone. Mazes grow from 1 pawn (par 2) to 5 pawns (par 9).
- **Par is exact:** each maze's fewest-hops count was worked out by a breadth-first search in Python (`/workspace/cc35/gen.py`), and the test re-checks it with a separate search inside the app.
- **Help without spoilers:** a wrong tap explains why (not a knight hop, or guarded by the pawn on g5). Hint lights a square on a fewest-hops route, Undo takes back a hop, and Restart starts over. Guarded squares are marked with ✕ on Mazes 1-3, and a button shows or hides them on any maze. The result card shows one route at par.
- **Stars and XP:** ★★ for a clean run at par (no hint, no undo), ★ for any other solve. XP is 10 for a first ★★, 5 for a first ★ or an upgrade, and 2 for a repeat. XP is live in shadow mode as before. Nothing here touches stamps, stars, SRS, accuracy, the gate or assessment.
- **History note** on the maze page: Rudrata's 9th-century knight's-path verse, Euler's 1759 study of the knight's tour, and Anand's 13 knight moves in a row in game 6 of the 2010 World Championship (source: Wikipedia, "Knight's tour").
- **Bug fix:** on tap-the-square boards (the Blindfold tracker and the Pawn and Plans quiz schools), the keyboard hint under the board stretched the invisible tap layer, so taps on the lower rows could land on the square above (off by up to 36px on a phone and 21px on a desktop). The tap layer now stays exactly board-sized, and the hint is hidden there. The Coordinate Sprint was already correct.
- **Storage unchanged:** results live in `ST.acad.viz.maze = {d,st,runs}` inside `cc2_state`, written only when a maze is finished. There are no new keys. An R34 save stays byte-identical when you browse the Gym and the mazes, and an R35 save with maze results opens in R34 and keeps them.
- **Accessibility:** maze levels and all 64 board squares are real buttons with labels (for example "e3, your knight"), messages are aria-live, control buttons are at least 40px tall, and there is no horizontal overflow at 390px or 1280px.
- **Shadow mode and gate unchanged:** `ST.prefs.shadow !== false` by default; gate stays `passed: false`; R28 freezes intact.
- The Settings label reads "build R35"; `window.CC_BUILD='R35'`. New files: `v14data.js` and `v14.js` (build order: `… v13data.js v13.js v14data.js v14.js`); CSS appended to `app.css`. New test: `cc-test/t35.js` (11 checks). The Gym-card count in the R32 test copy moves from 4 to 5.

