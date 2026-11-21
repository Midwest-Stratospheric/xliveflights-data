# Project B. Experimental: derived products

Built from the Eagle flight computer cleaned CSV (`../eagle-flight-computer/`) and the KE9CFY-11 APRS packets (`../aprs-tracker/`).

| File | What it is |
|---|---|
| `pbe-eagle-vertical-rates-2026-11-19.csv` | Ascent and descent rates between consecutive fresh Eagle GPS fixes |
| `pbe-eagle-ground-track-2026-11-19.geojson` | Eagle ground track (fresh GPS fixes), ascent and descent lines, launch / peak / last-row points |
| `pbe-eagle-ground-track-2026-11-19.kml` | Same track for Google Earth (absolute altitude) |
| `pbe-aprs-ke9cfy-11-ground-track-2026-11-19.geojson` | KE9CFY-11 APRS tracker ground track, ascent and descent |
| `pbe-aprs-ke9cfy-11-ground-track-2026-11-19.kml` | Same, as KML |

## Vertical rates columns

| Column | Units | Description |
|---|---|---|
| `utc_start`, `utc_end` | ISO 8601 UTC | Start and end of the interval (two consecutive fresh fixes) |
| `phase` | text | `ascent` or `descent` (split at the peak fix, 2026-11-20T00:11:24Z) |
| `interval_s` | s | Interval length (6 s normally; longer across stale-GPS or logging gaps) |
| `gps_altitude_start_m`, `gps_altitude_end_m` | m MSL | Eagle GPS altitude at each end |
| `vertical_rate_mps` | m/s | (end - start) / interval; negative = descending |
| `vertical_rate_ftmin` | ft/min | Same in ft/min |
| `gap_note` | text | Set when the interval spans a stale-GPS or logging gap |

Time-weighted means: ascent 4.33 m/s (841 intervals), descent -21.42 m/s (105 intervals).
Single 6 s intervals are noisy (GPS altitude resolution 1 m); smooth before using them for rate studies.

## Ground tracks

- Eagle: only rows with `gps_fix_fresh = 1`. Coordinates are [longitude, latitude, GPS altitude m].
  The launch point is the Old Settlers Park RC field, Round Rock, Texas; the last logged row is west of Bryan, Texas.
- APRS: the 134 unique KE9CFY-11 packets; altitude is the tracker's own GPS altitude.

License: CC BY 4.0, Aerostratospheric.
