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

## How the model works

The board is priced by its own peers, not by a hand-written list of names.
Every protocol, watchlist or not, is scored by the same function in
`lib/model.ts`:

1. **Peer multiple.** From the 128 live-token protocols in the sealed
   snapshot that record both a market cap and a TVL, an ordinary least
   squares fit gives log10(FDV/TVL) = 3.025 − 0.478 × log10(TVL). The
   multiple is clamped to the 0.03–0.60 range so no protocol is priced
   absurdly high or low.
2. **Growth.** The seven-day TVL change, clamped to −50%…+100%, moves the
   multiple by 0.4× the change (a 0.80–1.40 multiplier).
3. **Maturity.** Older protocols without a token score higher: a logarithmic
   age factor from 0.70 (brand new) to 1.00 (three years or more). A
   protocol with no recorded age is treated as one year old.
4. **Chains.** Each extra chain adds 2%, up to +8%.

Implied value is TVL × peer multiple × growth × maturity × chains. The fit
is weak on purpose and the dashboard says so: TVL explains only about a
sixth of the spread in peer multiples, so every implied value is an
estimate with a wide band, never a price. Per-category fits were tried and
rejected — with 8–15 protocols per category the slopes were unstable and
mostly explained less than the pooled fit.

## Farm plans

Every board row carries a seven-step farm plan written for that protocol's
own category, with a capital tier ($50/$100/$150/$250), a hold period that
depends on the protocol's age, weekly actions, a points check, and an exit
step. Costs and times are stated on each step. The plans assume a fresh
wallet that holds only the farming capital, and they never ask for a seed
phrase, a private key, or a signature you did not expect.

## Dashboard

`dashboard/` is a static page with no network. It shows the 40-protocol
watchlist plus 160 early pre-token rows, a top-10 chart by implied value,
search and category/chain/watchlist filters, a pre-token/live-token switch,
a sortable table, and a detail view for every protocol with its full model
breakdown, farm plan, and risk flags. The live-token tab shows the 24
largest live-token protocols with their FDV/TVL, the set the fit was
fitted on.

## Run it

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input ../input/snapshot.json
```

Node 22.18 or later, standard library only, no network. `main.ts` reads the
sealed snapshot, writes `board.json` (200 rows), `data.js`, copies
`dashboard/` and `screenshots/`, and writes `dossier.json`. Running it
twice writes the same bytes.

## Files

- `main.ts` — entrypoint: reads the snapshot, scores the board, writes the output.
- `lib/model.ts` — the peer-fitted model and the farm plans.
- `dashboard/` — the static page (`index.html`, `app.css`, `app.js`).
- `screenshots/` — the three dashboard screenshots the bounty asks for.
- `vendor/makefun-board.ts` — the kit's board library, unchanged.

---

Entered on [make.fun](https://make.fun/?ref=3txr3dna&utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash rewards
