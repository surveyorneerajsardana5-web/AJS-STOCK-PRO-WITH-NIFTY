# AJS TRADING PRO — NIFTY Box-1 Test Report

## Automated checks passed
- `npm run check`: `server.js` and `public/app.js` syntax passed.
- HTML parsing: 101 IDs checked, no duplicate IDs.
- Instrument configuration: NIFTY + BANK NIFTY + all 11 selected stocks configured.
- Box-1 required elements present: CALL score, PUT score, side-labelled score-based confidence, advance/decline counts, and breakout watch.
- Advance/decline now compares live LTP against the latest completed daily candle (previous session close), not the candle before that.
- Breakout watch has blinking CSS states for watch/trigger.
- Live NIFTY 5-minute candle updates are passed into breakout-watch logic so the next candle's high/low can trigger before that candle closes, after the initial breakout/breakdown candle has closed.
- ZIP archive integrity passed.
- Local smoke test: `/` and `/app.js` returned HTTP 200; `/api/status` returned 13 configured instrument entries (2 indices, 11 stocks) with no token configured.

## Not verified
- Live Upstox login/token permissions, live ticks, option chain, actual PCR/OI, and browser behavior during market hours were not verified because the smoke test intentionally ran without a token.
- Direction confidence is a score-based heuristic, not a validated probability or guarantee.
- Paper trading only; real order execution remains disabled.

## Start
Extract the ZIP, configure your Upstox token in the app's local `.env` file or settings as documented, and run `START_AJS_TRADING.bat`. Test the breakout trigger in paper mode during market hours before relying on it.
