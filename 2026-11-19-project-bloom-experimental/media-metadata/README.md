# Project B. Experimental: photo and video metadata

Technical metadata for the flight photos and videos kept with the tracking data (the files themselves are on the flight page).

Only an allow-list of fields is published: file name, type, size, SHA-256, pixel size, duration, frame rate,
video codec, creation date, camera make, and image GPS (none of these files carry a non-zero GPS position).
Device serial numbers, owner / artist / copyright text, software strings and ICC profile creator fields were not copied.

| File | What it is |
|---|---|
| `media-metadata-2026-11-19.csv` | One row per file |
| `media-metadata-2026-11-19.json` | Same as JSON |

License: CC BY 4.0, Aerostratospheric.
