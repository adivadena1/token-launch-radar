# token-launch-radar

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/adivadena1/token-launch-radar/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/adivadena1/token-launch-radar/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

Token Radar: a pre-token protocol board ranked by implied value. The multiple
is fitted from the snapshot's own live-token protocols (log-log fit of
FDV/TVL against TVL, n=128, R²=0.168, median 0.21x, leave-one-out error about
x4.9), then adjusted by each protocol's seven-day growth, its age with no
token, and its chain count. The dashboard shows the board, a detail view for
every protocol with its model breakdown and farm plan, and the live-token set
the fit was fitted on. Implied value is a model, not a promise, and never a
prediction that a token will launch.

## Run it

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input ../input/snapshot.json
```

Node 22.18 or later, standard library only, no network. `main.ts` reads the
sealed snapshot, writes `board.json` (200 rows), `data.js`, copies
`dashboard/` and `screenshots/`, and writes `dossier.json`.

---

Entered on [make.fun](https://make.fun/?ref=3txr3dna&utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash rewards
