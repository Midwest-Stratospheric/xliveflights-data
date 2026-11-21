# Project B. Experimental: Eagle flight computer log (Nov 19-20, 2026 UTC)

Onboard log from the Project B. Experimental high-altitude balloon flight of November 19, 2026 (UTC),
launched near Round Rock, Texas and recovered west of Bryan, Texas.

## Files

| File | What it is |
|---|---|
| `pbe-eagle-flight-computer-2026-11-19.txt` | Raw log as written by the flight computer. Content is unchanged; see the line-ending note below. |
| `pbe-eagle-flight-computer-2026-11-19-clean.csv` | Cleaned CSV (see "Cleaning" below). |
| `eagle-altitude-time.svg` | GPS altitude vs time chart (fresh GPS fixes only). |

Line-ending note: the original file from the flight computer uses Windows CRLF line endings (129,693 bytes,
SHA-256 `d9296edbbd7ceda90dd08f73e9910be433f110e9d6ba9415408e771433be68c2`). The upload tool used for this
commit stored it with LF line endings (128,104 bytes, SHA-256
`4698317ed34c8c5405ee20ecc17bab91b7e7b9091e940ef02aade974fd406f18`). Every character other than the
carriage returns is identical.

## Sensor notes

- Flight computer: High Altitude Science Eagle, firmware version 1.6.
- S1 data port: no sensor. S2 data port: temperature / pressure sensor.
- Logging interval: 6 seconds. GPS position, heading, ground speed and GPS altitude come from the Eagle's GPS receiver.
- **Pressure:** the pressure sensor bottoms out at about **17,780 Pa** (lowest logged value, 23:06:54 UTC, about 13 km).
  Above that point the logged pressure values are not physical (they climb again while the balloon keeps rising),
  so **GPS altitude is the reference altitude** for this flight. Do not derive altitude from `pressure_pa`.
- **GPS lock:** lock code `3` = fresh GPS fix; lock code `1` = no fresh fix, and the logger repeats the last
  known position/altitude. 368 of the kept rows have lock code 1, mostly 23:08-23:31 UTC on the ascent and
  00:13-00:26 UTC on the descent. Use `gps_fix_fresh = 1` rows for position and altitude work.
- Temperature is the S2 sensor reading inside/near the payload, not a calibrated outside-air value.

## Cleaning (raw -> CSV)

- Raw file: 1,574 data rows (plus a banner, firmware/sensor lines and one GPS warning block).
- Dropped 2 rows dated `06/28/12` (logger clock before GPS time was set).
- Dropped 2 pre-GPS-fix rows (11/19/26 21:50:42 and 21:50:48) with zero latitude, longitude and altitude.
- Kept 1,570 rows. No values were changed, except one date: the row at 00:00:00 is stamped `11/19/26`
  in the raw log; the CSV writes it as 2026-11-20T00:00:00Z.
- Gaps in the log (no rows written): 23:02:00-23:02:24, 23:06:54-23:07:18, and 00:19:00-00:25:24 UTC
  (the logger printed a "GPS is taking longer than expected to lock" message during the last gap).

## Columns (cleaned CSV)

All times are UTC.

| Column | Units | Description |
|---|---|---|
| `utc_time` | ISO 8601, UTC | Timestamp, e.g. `2026-11-19T22:16:24Z` |
| `latitude_deg` | degrees | GPS latitude (positive = north) |
| `longitude_deg` | degrees | GPS longitude (negative = west) |
| `heading_deg` | degrees | GPS course over ground |
| `ground_speed_kmh` | km/h | GPS ground speed |
| `gps_altitude_m` | m | GPS altitude above mean sea level (reference altitude) |
| `gps_lock_code` | code | Raw Eagle lock field: 3 = fresh fix, 1 = no fresh fix (last fix repeated) |
| `gps_fix_fresh` | 0/1 | 1 when `gps_lock_code` is 3 |
| `temperature_c` | deg C | S2 sensor temperature |
| `pressure_pa` | Pa | S2 sensor pressure (unreliable below ~17,780 Pa; see notes) |
| `raw_line` | line no. | Line number of this row in the raw .txt file |

## Summary (computed from the cleaned CSV)

| Item | Value |
|---|---|
| Log span (kept rows) | 2026-11-19 21:50:54 to 2026-11-20 00:34:42 UTC (2 h 43 m 48 s) |
| Launch (first climb, pressure drop) | 2026-11-19 22:16:24 UTC, GPS altitude about 196-199 m |
| Peak GPS altitude | **30,089 m (98,717 ft)** at 2026-11-20 00:11:24 UTC (30.65468, -96.74027), fresh fix |
| Launch to peak | 1 h 55 m 00 s |
| Last logged row | 2026-11-20 00:34:42 UTC, 150 m GPS altitude, still descending (30.67441, -96.58593) |
| Flight time (launch to last logged row) | 2 h 18 m 18 s |
| Lowest temperature | **-39.2 C**, 23:08:36-23:09:00 UTC (no fresh GPS fix then; last fix about 13 km) |
| Highest temperature | 25.8 C (on the ground before launch) |
| Lowest pressure logged | 17,780 Pa at 23:06:54 UTC (sensor floor) |

## License

Released under the [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/) license, same as the rest of this flight folder.
