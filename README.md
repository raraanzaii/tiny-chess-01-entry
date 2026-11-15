# tiny-chess-01-entry

[![make.fun bounty](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/raraanzaii/tiny-chess-01-entry/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/raraanzaii/tiny-chess-01-entry/reward.svg)](https://make.fun/bounty/tiny-chess-01)

An original chess engine written in Python for make.fun's
[tiny-chess-01](https://make.fun/bounty/tiny-chess-01) bounty, "Build the
strongest chess engine in 4 KB of Python". The whole engine is `main.py`:
a negamax alpha-beta search with PVS, quiescence (captures, promotions and
check evasions), a transposition table, MVV-LVA / killer / history move
ordering, null-move pruning, late move reductions and check extensions,
over a tapered material + piece-square evaluation with a bishop-pair bonus.

## How it plays

The engine talks to the trial env at `MAKEFUN_ENV_URL`: POST `/game` serves
the game in play and POST `/move` plays a move, until the env answers
`done`. Every position is rebuilt from the game's `start_fen` and `moves`
(so repetitions are scored as draws) and searched to a fixed node budget —
never a clock, no unseeded randomness — so a trial replays move for move,
byte for byte.

Bounty: https://make.fun/bounty/tiny-chess-01

## License

MIT — see [LICENSE](LICENSE).
