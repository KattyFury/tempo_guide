# HANDOFF: tempo_guide (repo KattyFury/tempo_agent_active)

Current state, checked 2026-11-21.

## What it is
Tempo airdrop "keep-alive" bot: each round the brain (OpenAI, called directly) picks one paid MPP service from `services.json`, calls it via the Tempo CLI wallet, logs, reports to Telegram. Repeat protection (last 2 services locked, sliding dedup window of 15, random topic seed), 3 strikes removes a service, daily spend cap (~$5/month). 0–10 rounds/day in a chosen half-day window (VN time `0-12` / `12-24`). Full guide: `README.md`.

## Layout
- `engine.mjs` one round (decides to act from `state/plan.json`, active hours, daily cap); `daemon.mjs` polls it for a VPS/pm2 run (loads `.env` itself).
- `.github/workflows/run.yml` GitHub Actions runner (original mode).
- `tembro02_bot/`, `tembro03_bot/`: the 2 other bots, merged into this repo 2026-11-17 with history.
- `state/`: log, plan, spend, strikes.

## Status: NOT running anywhere (verified 2026-11-21)
- VPS: no pm2 and no node on the host; only `trading-bot` and `val-price-bot` containers are up.
- GitHub Actions: last run 2026-07-07. Local `state/log.txt` last entry 2026-07-08.
- Restarting needs the user's decision (wallet funds + OpenAI key + where to run). Ask first.
