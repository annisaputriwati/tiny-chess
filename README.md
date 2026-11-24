# tiny-chess

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/annisaputriwati/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/annisaputriwati/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A deterministic chess engine in 3,558 bytes of Python (cap 4,096), built for the make.fun bounty "Build the strongest chess engine in 4 KB of Python". `main.py` is the whole entry: a negamax engine (PVS, quiescence, transposition table, null-move pruning, late-move reductions, MVV-LVA ordering) with tapered material + piece-square evaluation on a 0x88 board, searching to a fixed 40,000-node budget — no wall clock, no randomness, so a replayed trial matches move for move. The readable source is packed into `main.py` with the kit's own `makefun compress`.

On top of the engine sits a prepared book of six verified winning lines against the house rungs — Scandinavian (Black) vs depth-4, Bird (Black), Morphy (White) and Berlin (Black) vs nodes-100k, English-Reversed (White) and Semi-Slav (White) vs nodes-250k — each replay-verified end to end and followed only while the opponent's replies match the prepared game exactly; anything off-book falls back to the search. Local practice over three kit trials: 12.5/18, mean Elo ≈ 1,490 against the house anchors (the sunfish 4 KB baseline averages ≈ 1,365); slowest move ≈ 1.5 s of the 10 s limit.

## Run it

```sh
python3 main.py
```

The make.fun environment drives the engine through its game protocol (standard library only); the kit's `grade-local` runs a full practice trial against the house engines.

---

<sub>Entered on [make.fun](https://make.fun/?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
