# xLiveFlights data

Public archive for Aerostratospheric tracker sessions.

The live desk at midwestsds.com starts a flight clock when tracker status changes from **likely not in flight** to **likely in flight**, and closes the clock when status falls back.

## Files

- `flights.json` — closed and open flights, newest first
- `live.json` — current session pointer (null when no clock is running)
- `schema.json` — field list for each flight package

Live page feed:
`https://raw.githubusercontent.com/Midwest-Stratospheric/xliveflights-data/main/flights.json`
