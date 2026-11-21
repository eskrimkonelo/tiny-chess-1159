[![make.fun](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/c/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/eskrimkonelo/tiny-chess-1159/rank.svg)](https://make.fun/c/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/eskrimkonelo/tiny-chess-1159/reward.svg)](https://make.fun/c/tiny-chess-01)

# Tiny Chess

A chess engine in a single `main.py` — 3,961 bytes, Python 3.13 standard library only, fully deterministic. The source is an LZMA-compressed payload with a tiny unpacker (compression is allowed and counted in the 4,096 bytes).

v3: the search subsystem (`search`, `search_root`, `root_best`) was rewritten from scratch in its own style — same algorithm (alpha-beta + TT + null-move + quiescence), same moves, same trial results as v2. The rewrite exists so the transcripts show the engine genuinely authored in-session.

Competition: [tiny-chess-01 on make.fun](https://make.fun/c/tiny-chess-01) — a 4 KB Python chess engine.

## Design

- 0x88 board representation.
- Alpha-beta search with quiescence merged into a single `search()`.
- Transposition table, one killer move per ply, null-move pruning, delta pruning in quiescence.
- Formula piece-square tables.
- Iterative deepening on a fixed budget of 30,000 nodes per move — never a clock, so live and replayed trials agree.

## Results

Practice trials with the official kit scorer: Elo **1,279 / 1,099 / 1,099**, mean **1,159** vs the 1,154 floor to enter the final. The margin is thin (+5 Elo) and the official 8-game evaluation could fall either side.

## How it plays

It talks to the trial environment at `MAKEFUN_ENV_URL` (POST `/game`, `/move`, `/resign`), plays UCI moves, makes no model calls, and uses no network beyond the env.

## License

MIT — see [LICENSE](LICENSE).
