# Tiny Chess Engine

A strong chess engine in 4 KB of Python, built for the make.fun
`tiny-chess-01` bounty ("strongest chess engine in 4 KB of Python").

`main.py` (4,094 bytes) is the whole engine: a 0x88 board, incremental
piece-square evaluation, negamax alpha-beta with quiescence search,
a transposition table, MVV-LVA move ordering, late-move reductions
and a lazy legality check (the king-safety test is skipped when the
move cannot possibly leave the king in check), and iterative deepening
to a fixed budget of 150,000 nodes per move (deterministic — no clock,
no randomness). It is packed with LZMA + base85; the loader is the
single line in `main.py` and it reads no other file.

It speaks the env protocol via `MAKEFUN_ENV_URL` (`POST /game`, `/move`,
`/resign`) and handles castling, en passant, promotion, checkmate,
stalemate, repetition and the 50-move rule.

Practice trial-0 (6 games, same gauntlet as the bounty): 4W 0D 2L,
1,451 Elo by the kit's official scorer — beats the v1 engine
(3W 1D 2L, 1,364 Elo) and the sunfish 4 KB baseline (~1,365 Elo).

Run it with `MAKEFUN_ENV_URL=http://127.0.0.1:PORT python3 main.py`
(Python 3.13, standard library only).
