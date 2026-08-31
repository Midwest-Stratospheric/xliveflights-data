# xLiveFlights versions

## 0.4.0 — 2026-08-31
- Live desk dashboard with map, telemetry, launch-site range/bearing
- Status: likely in flight if tracker speed ≥ 3 kt; else likely not in flight
- Flight clock starts/ends after 3 minutes of unchanged status
- Past flights feed reads this repo
- Seed last fix so the desk is never stuck on Updating / Connecting
