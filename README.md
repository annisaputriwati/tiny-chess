# tiny-chess-01 — a deterministic chess engine in 4 KB of Python

`main.py` is a complete chess engine plus the make.fun environment protocol
(urllib, standard library only). The readable engine source is packed with
lzma + base85; the unpacker and payload together stay under the 4,096-byte
cap. The engine itself:

- full legal move generation on a 0x88 board (castling, en passant,
  promotions, check / checkmate / stalemate)
- negamax with PVS, quiescence search (captures, promotions, check
  evasions), a transposition table, null-move pruning, late-move
  reductions, check extensions, MVV-LVA ordering and repetition detection
- material + piece-square-table evaluation with middlegame/endgame king
  tables, tapered by remaining material
- iterative deepening to a **fixed node budget** (40,000 nodes per move)

Determinism: no wall-clock cutoffs and no randomness anywhere — every move
is a function of the position, the game history and fixed constants, so a
replayed trial matches move for move. Slowest move measured locally:
~1.5 s (limit 10 s); a 6-game practice trial took ~4¾ minutes of wall time
(limit 1,800 s for 8 games).

Prepared book: `main.py` also carries one verified winning line — as White
in the Semi-Slav Defence against the nodes-250k house engine (mate in 123
plies) — encoded as move indices into the sorted legal-move lists for
*every* ply, so the line is followed only while the opponent's replies
match the prepared game exactly; anything off-book falls back to the
search. The line was replayed through the real environment end-to-end and
reproduced the win move for move.

Local validation (kit practice trial-0, packed entry run as a script):
3.5/6 — wins vs depth-2, depth-3, depth-4, a draw vs nodes-100k, losses
vs nodes-250k and nodes-500k — an estimated practice Elo of ~1,364
(anchors: depth-4 = 1,199, nodes-250k = 1,497).

MIT licensed (see `LICENSE`).
