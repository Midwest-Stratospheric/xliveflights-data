# Project B. Experimental: KE9CFY-11 APRS tracker data

The flight also carried a StratoTrack APRS tracker, callsign **KE9CFY-11**. Its packets were heard by amateur
radio iGates and collected through the SondeHub amateur telemetry API (APRS-IS gateway).

| File | What it is |
|---|---|
| `ke9cfy-11-sondehub-raw-2026-11-19.json` | Raw packets as returned by SondeHub (all 136 receptions, keyed by packet time), including the raw APRS packet strings |
| `ke9cfy-11-decoded-positions-2026-11-19.json` | 134 unique decoded packets with computed distance, vertical rate and flags |
| `ke9cfy-11-decoded-positions-2026-11-19.csv` | Same as CSV (identical content to `../project-bloom-experimental-KE9CFY-11-packets.csv`) |
| `stations-heard-2026-11-19.json` | Stations that heard the tracker (callsign, roles, packet counts, ranges) |

## Tracker readings (KE9CFY-11, not the Eagle)

- **Highest KE9CFY-11 packet: 98,325 ft** (tracker GPS altitude). This is the tracker's highest reported position,
  not the flight's peak. The Eagle flight computer logged the peak at **98,717 ft (30,089 m)**; see `../eagle-flight-computer/`.
- **Lowest KE9CFY-11 temperature: -54 C** (tracker's own sensor). The Eagle S2 sensor's lowest reading was -39.2 C.
  The two sensors sit in different places and are not calibrated outside-air sensors.
- The tracker comment field carries frame number, satellites, battery voltage, temperature and pressure
  (e.g. `StrTrk,27,9,1.66V,22C,98162Pa`). These are decoded into `frame`, `sats`, `batt`, `temp`, `press` (hPa).

## Decoded JSON fields

`dt` UTC time; `lat`, `lon` degrees; `alt` m; `course` deg; `spd_kt` knots; `spd_kmh` km/h; `frame`; `sats`;
`batt` V; `temp` C; `press` hPa; `comment` and `raw` as received; `igate`; `n_up` receptions; `flag` data flag;
`dist_km` from launch; `vrate` m/s from the previous packet; `gs_calc_kmh` computed ground speed; `dt_prev` s.

Callsigns are public amateur radio identifiers. License: CC BY 4.0, Aerostratospheric (SondeHub data is used under its open-data terms).
