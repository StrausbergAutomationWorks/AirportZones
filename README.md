# AirportZones

Every airport in [OurAirports](https://ourairports.com), with its IANA time zone,
its name and city, as one SQLite file. Built for the Live Track Home Assistant
integrations, which need to turn an airport code such as `KORD` into a place, a
position and a local clock. Anyone may use it under the licence below.

## Download

The current file is always at the same address:

```
https://github.com/StrausbergAutomationWorks/AirportZones/releases/download/data/saw_airport_zones.sqlite.gz
https://github.com/StrausbergAutomationWorks/AirportZones/releases/download/data/SHA256SUMS
```

Release `data` holds the latest build only. It is rebuilt **weekly** from that
week's OurAirports data. Check `SHA256SUMS` (a few bytes) and download the file
only when the hash has changed.

## What is in it

Gzipped SQLite, about 5 MB compressed and 12 MB unpacked. Three tables:

| Table | Columns |
|---|---|
| `zones` | `ident` (primary key), `tz`, `lat`, `lon`, `cross_check`, `name`, `municipality`, `iata_code`, `iso_country`, `type` |
| `aliases` | `code` (primary key), `ident`, `field` |
| `meta` | `k`, `v`: format, build time, sources, licence, attribution, row count |

* **`ident`** is the OurAirports identifier. Resolve a code against `zones.ident`
  first, then `aliases.code`, which holds codes that match an airport on its
  `icao_code`, `gps_code`, `local_code` or `iata_code` instead. A `local_code`
  shared by more than one airport is left out rather than guessed.
* **`tz`** is the IANA zone name for the airport's coordinates, computed with
  [timezonefinder](https://github.com/jannikmi/timezonefinder). The file stores zone
  names, not offsets, so daylight saving is handled by your own time zone database.
* **`lat`, `lon`** are the coordinates the zone was computed from.
* **`cross_check`** compares the zone with a second, independent implementation,
  [GeoTimeZone](https://github.com/mattjohnsonpint/GeoTimeZone):
  `same_name`, `same_clock` (a different name with the same offsets), or
  `DIFFERS:<zone>`. Rows marked `DIFFERS` lie on a zone border and have not been
  reviewed yet. Both libraries use the same boundary data, so agreement is a
  check on the code, not on the boundaries.
* **`name`, `municipality`, `iata_code`, `iso_country`, `type`** are OurAirports'
  own values, `NULL` where OurAirports has none. `municipality` is the city.
  `type` includes `closed`: closed airports are kept, because a flight plan can
  still name one, and should not be presented as open.

`meta.format` is `saw_airport_zones/1`. A change to the columns changes that value.

## Licence and attribution

The time zones are derived from
[Timezone Boundary Builder](https://github.com/evansiroky/timezone-boundary-builder)
data, which is © OpenStreetMap contributors and available under the
[Open Database License (ODbL) v1.0](https://opendatacommons.org/licenses/odbl/1-0/).
This database is therefore made available under the **ODbL v1.0** as well. See
[`DATA_LICENSE.md`](DATA_LICENSE.md).

Airport data is from OurAirports ([davidmegginson/ourairports-data](https://github.com/davidmegginson/ourairports-data)),
released into the public domain.

If you use or share this database, keep the attribution with it. The file
carries it in its own `meta` table under `attribution`.

## Not affiliated

Not affiliated with or endorsed by OurAirports, OpenStreetMap or the Timezone
Boundary Builder project. No warranty: check a zone or a name against an
authoritative source before relying on it for anything that matters.
