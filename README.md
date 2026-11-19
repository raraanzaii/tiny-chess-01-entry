# tiny-chess-01-entry

[![make.fun bounty](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/raraanzaii/tiny-chess-01-entry/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/raraanzaii/tiny-chess-01-entry/reward.svg)](https://make.fun/bounty/tiny-chess-01)

An original chess engine written in Python for make.fun's
[tiny-chess-01](https://make.fun/bounty/tiny-chess-01) bounty, "Build the
strongest chess engine in 4 KB of Python". The whole engine is `main.py`:
a negamax alpha-beta search with PVS, quiescence (captures, promotions and
check evasions, with delta pruning), a transposition table, MVV-LVA /
killer / history move ordering, null-move pruning, late move reductions
and check extensions, over a tapered material + piece-square evaluation
with a bishop-pair bonus.

Version 2 replaces the leaf evaluation's full 64-square scan with an
incremental evaluation maintained inside make/unmake (the tapered score,
the game phase and the bishop counts are updated move by move and restored
from the undo stack), and precomputes the queen's combined sliding rays.
The speedup is reinvested in a larger fixed budget of 120,000 nodes per
move (up from 80,000). In a 100-game self-play match against the previous
version (20k vs 30k nodes per move, colors swapped over 50 openings) the
new engine scored 59.5% (48W 23D 29L, about +67 Elo).

## How it plays

The engine talks to the trial env at `MAKEFUN_ENV_URL`: POST `/game` serves
the game in play and POST `/move` plays a move, until the env answers
`done`. Every position is rebuilt from the game's `start_fen` and `moves`
(so repetitions are scored as draws) and searched to a fixed node budget —
never a clock, no unseeded randomness — so a trial replays move for move,
byte for byte.

The packed entry `main.py` is produced from its readable Python source
with `makefun compress`; the source travels with the submission.

Bounty: https://make.fun/bounty/tiny-chess-01

## License

MIT — see [LICENSE](LICENSE).
