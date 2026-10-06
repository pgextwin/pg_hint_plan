# pg_hint_plan Windows binaries

[日本語](README_ja.md) | **English**

This repository provides **unofficial Windows x64 binaries** of [pg_hint_plan](https://github.com/ossc-db/pg_hint_plan).

pg_hint_plan is maintained upstream by the pg_hint_plan community. Its behavior, hint syntax, configuration, and limitations are defined by the upstream project. This repository focuses on reproducible Windows packaging for ordinary PostgreSQL Windows installations.

## Upstream release mapping

pg_hint_plan maintains a separate stable release series for each PostgreSQL major version.

| PostgreSQL | Upstream ref | pg_hint_plan version | Tested PostgreSQL |
|---:|---|---:|---:|
| 14 | `REL14_1_4_4` | 1.4.4 | 14.24 |
| 15 | `REL15_1_5_3` | 1.5.3 | 15.19 |
| 16 | `REL16_1_6_2` | 1.6.2 | 16.15 |
| 17 | `REL17_1_7_1` | 1.7.1 | 17.11 |
| 18 | `REL18_1_8_0` | 1.8.0 | 18.6 |

PostgreSQL lifecycle metadata is maintained centrally in **pgextwin/build**. PostgreSQL 14 remains included only while it is still within the configured community maintenance window.

## Download

The first pgextwin package set uses release tag:

~~~text
v1.8.0-windows.1
~~~

The tag is anchored to the newest supported pg_hint_plan series. Each ZIP still records and uses the exact upstream release corresponding to its PostgreSQL major.

Asset names are explicit:

~~~text
pg_hint_plan-REL14_1_4_4-pg14-windows-x64.zip
pg_hint_plan-REL15_1_5_3-pg15-windows-x64.zip
pg_hint_plan-REL16_1_6_2-pg16-windows-x64.zip
pg_hint_plan-REL17_1_7_1-pg17-windows-x64.zip
pg_hint_plan-REL18_1_8_0-pg18-windows-x64.zip
~~~

Each package contains:

~~~text
lib/
  pg_hint_plan.dll
share/
  extension/
    pg_hint_plan.control
    pg_hint_plan--*.sql
COPYRIGHT
COPYRIGHT.postgresql
UPSTREAM-README.md
PACKAGE-INFO.txt
~~~

## Installation

1. Stop PostgreSQL before replacing extension binaries.
2. Use the ZIP matching the PostgreSQL major version.
3. Copy `lib/pg_hint_plan.dll` to PostgreSQL's `lib` directory.
4. Copy `share/extension/*` to PostgreSQL's `share/extension` directory.
5. Add `pg_hint_plan` to `shared_preload_libraries` when using the extension globally.
6. Restart PostgreSQL.
7. Run:

~~~sql
CREATE EXTENSION pg_hint_plan;
~~~

See [docs/windows_ja.md](docs/windows_ja.md) and the upstream documentation for details.

## Windows build strategy

The Windows build uses MSVC x64 and a generated DEF file for module entry points.

For PostgreSQL 17 and 18, the upstream scanner source is generated from `query_scan.l` with win_flex and compiled directly.

For PostgreSQL 14–16, pg_hint_plan also calls PostgreSQL query-jumble code that is not exported from the standard Windows PostgreSQL DLL. pgextwin therefore downloads the **exact official PostgreSQL source release**, verifies its SHA-256, rebuilds only the required query-jumble object with the same target PostgreSQL headers, and links that object into pg_hint_plan.

No opaque precompiled compatibility object is stored in this repository.

The validated source archives are:

| PostgreSQL | Source archive SHA-256 |
|---:|---|
| 14.24 | `a7fa7ed3d558172355f51406097a7bd4f6b473be80f311ef7cda96bf383d8897` |
| 15.19 | `e1a64a87a46b825b88c082e4518161a47aab53c45694964f8ba1df28f7859f89` |
| 16.15 | `c1575341fa7bd40f5274ea465b34390f4dc64cdd0770af327005caaeb9f6b7ed` |

## Functional CI

Every supported PostgreSQL major must pass:

1. upstream source checkout,
2. exact upstream copyright/license-file verification,
3. Windows x64 build,
4. PostgreSQL startup with `shared_preload_libraries=pg_hint_plan`,
5. `CREATE EXTENSION pg_hint_plan`,
6. a forced `SeqScan(...)` hint and verification of the actual EXPLAIN plan,
7. a forced `IndexScan(...)` hint and verification of the actual EXPLAIN plan,
8. for PostgreSQL 14–16, explicit execution of the hint-table/query-id compatibility path,
9. package creation.

Pull requests and `main` run validation only. A branch named `release/<tag>` triggers the release path after the full matrix passes.

## Licensing

pg_hint_plan redistribution requires the upstream copyright terms in `COPYRIGHT` and the PostgreSQL-derived-code notice in `COPYRIGHT.postgresql`.

The PostgreSQL-derived notice differs across older pg_hint_plan release series, so this repository also stores exact copies under `licenses/pg14`, `licenses/pg15`, and `licenses/pg16` solely for CI verification against each pinned upstream checkout.

Release ZIPs copy the copyright files directly from the exact upstream checkout used for that PostgreSQL package.

These binaries are unofficial pgextwin builds and are not official binary releases from the upstream pg_hint_plan project.
