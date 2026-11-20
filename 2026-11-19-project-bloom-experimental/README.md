# Project Bloom Experimental — 19 November 2026

Open flight data from **Aerostratospheric** for the Project Bloom Experimental high-altitude balloon flight.

The balloon was launched from the Old Settlers Park RC field in Round Rock, Texas, on 19 November 2026. The APRS callsign was **KE9CFY-11**. The payload was a Bloom Sparkling Energy Crisp Apple can.

Mission page: https://www.midwestsds.com/project-bloom-experimental.html

This release is flight data. It is not a sponsorship, endorsement, or partnership statement.

## Flight at a glance

Times are in America/Chicago (CT). On this date CT was CST (UTC-6). UTC timestamps are included in the data files.

| | CT | UTC | Position | Altitude |
| --- | --- | --- | --- | --- |
| Launch (estimated) | 4:16:15 PM CT | 2026-11-19T22:16:15Z | 30.53201, -97.62884 | pad ~200 m |
| Burst | 6:11:02 PM CT | 2026-11-20T00:11:02Z | 30.65400, -96.74933 | **98,325 ft** |
| Last APRS packet | 6:41:09 PM CT | 2026-11-20T00:41:09Z | 30.68533, -96.53817 | 2,185 ft |
| SPOT Trace STOP | 6:42:28 PM CT | 2026-11-20T00:42:28Z | 30.67436, -96.58609 | — |

- **Flight time:** 2 h 25 m 42 s (launch estimate to estimated touchdown)
- **Stations that heard the flight:** 18
- **Unique APRS packets in this CSV:** 134 (136 raw, 2 duplicates removed)

## Files

| File | Description |
| --- | --- |
| `project-bloom-experimental-KE9CFY-11-packets.csv` | Unique APRS / SondeHub amateur telemetry packets for KE9CFY-11 |
| `stations-heard.csv` | Stations that heard the flight, with packet counts and ranges |
| `spot-trace-fixes.csv` | SPOT Trace fixes. The source archive contained only the STOP / recovery fix, not a full breadcrumb trace |
| `flight-summary.json` | Machine-readable flight summary, including computed rates, gaps, flags, and a cross-check of the headline numbers |
| `flight-summary.md` | The same summary in readable form |
| `tawhiri-prediction-summary.json` | Compact pre-flight Tawhiri / GFS prediction summary and comparison to the actual flight |
| `tawhiri-ensemble-table.csv` | Ten Tawhiri ensemble scenarios (launch-time, burst, and rate offsets) |
| `charts/` | SVG charts generated from the packet CSV and the nominal Tawhiri track |

## Packet CSV columns

`project-bloom-experimental-KE9CFY-11-packets.csv`

| Column | Description |
| --- | --- |
| `time_utc` | Packet time in UTC (ISO-8601, `Z`) |
| `time_ct` | Same instant in America/Chicago (CT), 12-hour clock |
| `lat`, `lon` | Packet position, decimal degrees, WGS84 |
| `alt_m`, `alt_ft` | Altitude in metres and feet |
| `vertical_rate_mps` | Climb or descent rate from the previous unique packet, metres per second (empty on the first row) |
| `speed_kt`, `speed_kmh` | Ground speed reported in the APRS packet, knots and km/h |
| `course_deg` | Course reported in the APRS packet, degrees |
| `dist_from_launch_km` | Great-circle distance from the RC field (30.5320062, -97.6288426), kilometres |
| `temp_c` | Tracker temperature, °C |
| `batt_v` | Tracker battery voltage |
| `pressure_hpa` | External pressure, hPa (from the pascal field in the APRS comment) |
| `sats` | Satellite count reported by the tracker |
| `frame` | Tracker frame counter (this counter reset during descent: frame 145 then 9) |
| `igate` | iGate / uploader callsign on this packet |
| `data_flag` | Quality flag, when present (low-sat fix or pressure inconsistent with altitude) |
| `comment` | APRS comment body |
| `raw_packet` | Raw APRS packet text |

## Stations-heard CSV columns

`stations-heard.csv`

| Column | Description |
| --- | --- |
| `callsign` | Station callsign |
| `roles` | How the station appears in the record (SondeHub uploader, iGate, digipeater, and/or heard on aprs.fi) |
| `packets` | Packets associated with that station |
| `first_heard_ct`, `last_heard_ct` | First and last times the station is in the record, CT |
| `station_lat`, `station_lon` | Station position when known |
| `dist_from_launch_mi` | Station distance from the launch field, miles |
| `bearing_from_launch` | Station bearing from the launch field |
| `max_range_to_balloon_mi` | Maximum range from the station to the balloon, miles |
| `source` | Source of the hearing record |

Eighteen unique callsigns are listed. The `igates` list in `flight-summary.json` has 13 callsigns because it counts only the iGate column on the packet CSV, not digipeaters or stations recorded only as heard on aprs.fi.

## SPOT Trace fixes

`spot-trace-fixes.csv` has one row: the SPOT Trace STOP fix at 6:42:28 PM CT (2026-11-20T00:42:28Z), 30.67436, -96.58609, near Caldwell, Texas (ZIP 77836). Extra columns give distance and bearing from the last APRS packet, the estimated touchdown, the predicted landing, and the launch field.

A full SPOT breadcrumb trace was not in the local source folder, so it is not invented here.

## Tawhiri prediction

Pre-flight predictions used the [SondeHub Tawhiri](https://api.v2.sondehub.org/tawhiri) API with the **GFS 19 November 2026 12:00 UTC** cycle. Earlier and later GFS cycles were requested and were not available from Tawhiri at run time.

The nominal run assumed a **4:30 PM CT** launch, a **30 km** burst, and **5 m/s** ascent and sea-level descent. Under those assumptions Tawhiri put burst at 6:09:20 PM CT near 30.59557, -96.87440 and landing at 6:55:00 PM CT near 30.62312, -96.64098 (about 59 miles east of launch, near FM 1362, Caldwell, Burleson County).

The flight launched about 14 minutes earlier than that assumption, rose more slowly than 5 m/s, and descended much faster than 5 m/s. Burst altitude was close to 30 km (29,969 m). Burst and landing were on the order of 12–14 km from the nominal predicted points. Details are in `tawhiri-prediction-summary.json` and `tawhiri-ensemble-table.csv`.

## Charts

SVG charts in `charts/` were generated from the packet CSV, with the nominal Tawhiri track overlaid where it helps. They are:

- `altitude-time.svg` — altitude versus time, CT
- `altitude-distance.svg` — altitude versus distance from launch
- `distance-time.svg` — distance from launch versus time
- `ground-speed.svg` — ground speed versus time
- `vertical-rate.svg` — climb and descent rate versus time
- `temp-altitude.svg` — tracker temperature versus altitude
- `telemetry.svg` — temperature, battery, and pressure versus time
- `track-map.svg` — geographic track (ascent, descent, predicted track, burst, last packet, and the SPOT STOP fix)

Shaded vertical bands on the time charts mark packet gaps.

## Data notes

- Launch time 4:16:15 PM CT is an estimate: the first two packets were extrapolated down to pad elevation (200.4 m) at the RC field. The first received packet is 4:17:03 PM CT at 1,177 ft.
- Touchdown 6:41:57 PM CT is an estimate: the last two packets were extrapolated down to ground elevation near the last APRS point. The last received packet is 6:41:09 PM CT at 2,185 ft. The SPOT STOP fix is 6:42:28 PM CT, about 4.7 km west-southwest of that last packet.
- Packet gaps: 5:59:02–6:01:02 PM CT (120 s); 6:15:02–6:25:09 PM CT (607 s); 6:37:09–6:39:09 PM CT (120 s).
- Some descent packets are flagged for a low satellite count and/or a pressure reading inconsistent with altitude. See `data_flag` in the packet CSV and the `flagged` list in `flight-summary.json`.
- The headline numbers in this README were checked against the CSVs and source JSON. Mismatches, if any, are recorded in `flight-summary.json` under `cross_check` rather than by changing the data files. All headline figures matched.

## License

This dataset is released under the [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/) license.

Please attribute **Aerostratospheric**.

## Source

APRS telemetry was collected via the SondeHub amateur telemetry API. The pre-flight track is a Tawhiri run on the GFS 19 November 2026 12:00 UTC cycle. The recovery position is a SPOT Trace STOP fix.
