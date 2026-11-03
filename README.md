# pg_hint_plan — Windows x64

[日本語](README_ja.md) | English

This repository distributes **unofficial Windows x64 binaries** of [pg_hint_plan](https://github.com/ossc-db/pg_hint_plan). provides optimizer hints for PostgreSQL execution plans.

## Download

Use the [latest published Release](https://github.com/pgextwin/pg_hint_plan/releases/latest) or [all Releases](https://github.com/pgextwin/pg_hint_plan/releases). Published PostgreSQL **14–18** packages are listed in the [pgextwin catalog](https://pgextwin.github.io/website/en/). Select the ZIP for your PostgreSQL major. PostgreSQL 14 community support ends November 12, 2026.

## Installation

1. Back up your environment and review the [upstream setup guide](https://github.com/ossc-db/pg_hint_plan).
2. Stop PostgreSQL before replacing files. Copy the files in the matching ZIP's lib/ and share/extension/ directories to your PostgreSQL installation, where present.
3. Upstream versions differ by PostgreSQL major. Configure loading of pg_hint_plan according to upstream instructions for the features you use; session and shared preload choices, and whether CREATE EXTENSION is needed, depend on the usage.
4. Start or restart PostgreSQL after applying the configuration. Confirm operation in a test environment.

Use SHA256SUMS.txt attached to the Release to verify your downloaded ZIP. Other available materials may include SPDX SBOMs, vulnerability reports, and signed attestations.

## License

The upstream project documents audit/SQL behavior, settings, and limitations. This is an independent Windows package, not an official upstream distribution. See the included license notices.
