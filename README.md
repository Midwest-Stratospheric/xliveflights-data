# xLiveFlights data

Public archive for Aerostratospheric tracker sessions.

The live desk at midwestsds.com starts a flight clock when tracker status changes from **likely not in flight** to **likely in flight**, and closes the clock when status falls back.

## Operation Canis Major

<img src="https://www.midwestsds.com/images/operation-canis-major-patch.png" alt="Operation Canis Major patch" width="120" align="right">

This project is part of [Operation Canis Major](https://www.midwestsds.com/operation-canis-major.html), often called Project Canis: Aerostratospheric's mission objective to provide open stratospheric and atmospheric research and data, unrestricted, to the public. Learn more: https://www.midwestsds.com/operation-canis-major.html

## Files

- `flights.json` — closed and open flights, newest first
- `live.json` — current session pointer (null when no clock is running)
- `schema.json` — field list for each flight package

Live page feed:
`https://raw.githubusercontent.com/Midwest-Stratospheric/xliveflights-data/main/flights.json`

## Flown archive and collaboration

Flown so far: the Sep 12, 2026 x1Albatross envelope check (burst 59,000 ft) and the Sep 19, 2026 X2Griffon maiden flight (burst 90,356 ft). Full records: https://www.midwestsds.com/flights.html. Launches are private science missions; the archive and data are public, and flight products also appear on xDataHub, our public open atmospheric data dashboard: https://www.midwestsds.com/msds-data-hub.html

Tracking and data folks who want to collaborate can email space@aerostratospheric.com or book a 15 minute intro at https://calendly.com/aerostratospheric/15min
