# Data licence

**AirportZones** (`saw_airport_zones.sqlite`) is made available under the
[Open Database License (ODbL) v1.0](https://opendatacommons.org/licenses/odbl/1-0/).
Any rights in individual contents of the database are licensed under the
[Database Contents License (DbCL) v1.0](https://opendatacommons.org/licenses/dbcl/1-0/).

## Why this licence

The `tz` and `cross_check` columns are derived from
[Timezone Boundary Builder](https://github.com/evansiroky/timezone-boundary-builder)
data, © OpenStreetMap contributors, which is available under the ODbL v1.0.
A database derived from ODbL data and shared publicly is shared under the same
licence.

## Attribution

Keep this notice with the database and with anything derived from it:

> Time zone boundaries: Timezone Boundary Builder
> (github.com/evansiroky/timezone-boundary-builder), data © OpenStreetMap
> contributors, available under the Open Database License (ODbL).
> Airports: OurAirports (ourairports.com), public domain.

The same text is stored in the file's `meta` table under the key `attribution`.

## Sources

| Part | Source | Terms |
|---|---|---|
| airports, names, codes, coordinates | OurAirports, [davidmegginson/ourairports-data](https://github.com/davidmegginson/ourairports-data) | public domain (The Unlicense) |
| time zones | Timezone Boundary Builder, through timezonefinder | ODbL v1.0 |
| cross-check | Timezone Boundary Builder, through GeoTimeZone | ODbL v1.0 |
