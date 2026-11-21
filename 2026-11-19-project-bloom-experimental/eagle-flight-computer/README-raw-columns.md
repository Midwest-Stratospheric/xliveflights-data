# Project B. Experimental: Eagle raw log columns

The raw log `pbe-eagle-flight-computer-2026-11-19.txt` (High Altitude Science Eagle, firmware 1.6) has this header:

`UTC Date,UTC Time,Latitude  ,Longitude ,Head,Km/h,Alt-m  ,Lock,  ,Temp C,Pa    ,`

| Raw column | Example | Units | Cleaned CSV column | Notes |
|---|---|---|---|---|
| `UTC Date` | `11/19/26` | MM/DD/YY, UTC | part of `utc_time` | Rows dated `06/28/12` are from before the logger got GPS time and were dropped |
| `UTC Time` | `22:16:24` | HH:MM:SS, UTC | part of `utc_time` | |
| `Latitude` | `+030.53214` | degrees | `latitude_deg` | Signed, zero-padded |
| `Longitude` | `-097.62891` | degrees | `longitude_deg` | Signed, zero-padded |
| `Head` | `0337` | degrees | `heading_deg` | GPS course over ground |
| `Km/h` | `0012` | km/h | `ground_speed_kmh` | GPS ground speed |
| `Alt-m` | `+012938` | m MSL | `gps_altitude_m` | GPS altitude |
| `Lock` | `0003` | code | `gps_lock_code`, `gps_fix_fresh` | 3 = fresh fix, 1 = last fix repeated |
| (blank) | | | not carried | S1 data port: no sensor detected, so this column is always empty |
| `Temp C` | `+025.7` | deg C | `temperature_c` | S2 sensor |
| `Pa` | `100015` | Pa | `pressure_pa` | S2 sensor; floors at about 17,780 Pa (see `README-sounding.md`) |

The raw file also contains a banner line, the firmware line, the S1/S2 sensor detection lines and one
"GPS is taking longer than expected to lock" message. The log has no satellite count, battery voltage,
humidity or dew point fields.
