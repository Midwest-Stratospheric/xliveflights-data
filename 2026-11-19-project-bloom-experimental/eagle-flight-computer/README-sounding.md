# Project B. Experimental: Eagle flight computer sounding

Altitude against temperature and pressure from the onboard High Altitude Science Eagle flight computer
(firmware 1.6, S2 temperature / pressure sensor), built from `pbe-eagle-flight-computer-2026-11-19-clean.csv`.
Ascent and descent are labelled separately. The viewer page is
https://www.midwestsds.com/soundings/2026-11-19-project-b-experimental.html

| File | What it is |
|---|---|
| `pbe-eagle-sounding-2026-11-19.csv` | One row per logged row from launch (22:16:24 UTC) to the last logged row, with phase and flags |
| `pbe-eagle-sounding-2026-11-19.json` | Same rows plus the flag rules and metadata |

## Pressure sensor floor (read this first)

The S2 pressure sensor bottoms out at about **17,780 Pa** (lowest reading 23:06:54 UTC, last fresh GPS fix
12,938 m). Above that point the logged pressure is not physical: it climbs back toward surface values while the
balloon keeps rising. `pressure_flag` is `sensor floor` when:

- `pressure_pa` is at or below 18,700 Pa (within about 5% of the floor), or
- the row is between the floor reading (2026-11-19T23:06:54Z) and the first fresh descent GPS fix below
  12,938 m (2026-11-20T00:26:36Z), or
- a fresh GPS altitude is at or above 12,938 m.

Flagged pressure values are kept so nothing is hidden, but they are **not** real atmospheric pressure.
Use GPS altitude as the altitude reference.

## Columns

| Column | Units | Description |
|---|---|---|
| `utc_time` | ISO 8601 UTC | Timestamp |
| `phase` | text | `ascent` (launch to the peak fix at 2026-11-20T00:11:24Z) or `descent` |
| `gps_altitude_m` | m MSL | Eagle GPS altitude |
| `gps_altitude_ft` | ft MSL | Same, in feet |
| `gps_fix_fresh` | 0/1 | 1 = fresh GPS fix; 0 = the logger repeated the last fix |
| `altitude_flag` | text | `ok`, or `stale (last GPS fix repeated)` when `gps_fix_fresh` = 0 |
| `temperature_c` | deg C | S2 sensor temperature (at the payload, not calibrated outside air) |
| `pressure_pa` | Pa | S2 sensor pressure as logged |
| `pressure_hpa` | hPa | Same, in hPa |
| `pressure_flag` | text | `ok` or `sensor floor` (see above) |
| `raw_line` | line no. | Line in the raw .txt log |

## Fields the log does and does not have

- Has: UTC date/time, latitude, longitude, heading, ground speed, GPS altitude, GPS lock code, S2 temperature, S2 pressure.
- Does **not** have: humidity, dew point, wind (only the GPS ground track), satellite count, battery voltage.
  The S1 data port had no sensor, so the raw log's S1 column is empty. No humidity or dew point is derived or estimated here.
- The KE9CFY-11 APRS tracker reported its own satellites, battery, temperature and pressure; see `../aprs-tracker/`.

License: CC BY 4.0, Aerostratospheric.
