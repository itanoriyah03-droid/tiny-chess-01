# Tiny Chess v1

[![make.fun](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/itanoriyah03-droid/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard)
[![reward](https://make.fun/badge/tiny-chess-01/itanoriyah03-droid/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01)

The strongest chess engine in 4 KB of Python. Built from scratch for the
[make.fun tiny-chess-01 bounty](https://make.fun/bounty/tiny-chess-01).

## Engine

- `main.py` — 3,857 bytes. A self-contained packed engine: LZMA-compressed
  source with a tiny Latin-1 unpacker (own code, no dependencies).
- 0x88 board, alpha-beta + transposition table + quiescence (captures and
  check evasions), MVV-LVA + TT-move ordering, tapered piece-square eval
  (calibrated pawn advance, centralisation, bishop pair, king safety).
- Fixed deterministic node budget (120,000 nodes/move, ~4 s/move, well under
  the 10 s limit). No wall clock in the search, no randomness — every move
  is a pure function of the position, so replays are byte-identical.
- Plays the env protocol: `MAKEFUN_ENV_URL`, `POST /game`, `POST /move`,
  `POST /resign` (never resigns — plays every game to mate/adjudication).

## Verify

- Perft: startpos depth 4 = 197,281; Kiwipete depth 3 = 97,862;
  position 3 depth 4 = 43,238; position 4 depth 3 = 9,467;
  position 5 depth 3 = 62,379. Make/unmake restores state exactly.
- Mate in 1 (Qxf7#) found instantly.

## License

MIT. See `LICENSE`.
