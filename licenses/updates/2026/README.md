# pg_hint_plan upstream 2026 license notices

These are byte-for-byte copies of the license notices from the pinned upstream commits.

| Packaging file | Upstream path | Pinned commit or series |
| --- | --- | --- |
| `licenses/updates/2026/COPYRIGHT` | `COPYRIGHT` | PG14–19 (identical blob) |
| `licenses/updates/2026/pg14/COPYRIGHT.postgresql` | `COPYRIGHT.postgresql` | PG14 `cf003edac10606703308209f749b761f9ac39ad0` |
| `licenses/updates/2026/pg15_16/COPYRIGHT.postgresql` | `COPYRIGHT.postgresql` | PG15 `f31082502dee329228f227fd20fc492d259ff41e` / PG16 `6b3c57fe2ac12e5f6f1fb3cbb4873e28125248ae` |
| `licenses/updates/2026/pg17_18/COPYRIGHT.postgresql` | `COPYRIGHT.postgresql` | PG17 `05d080bf80d7b97bf5401a865d9fefd15b7b4c16` / PG18 `9a3f851e1993d6728a9707956dabfcf22cc35b38` |
| `licenses/updates/2026/pg19/COPYRIGHT.postgresql` | `COPYRIGHT.postgresql` | PG19 `4d3e9164dc2dc1b10dfe0c5e7a3cfe7983a8688d` |

`config/extension.json` maps the shared `COPYRIGHT` and the matching `COPYRIGHT.postgresql` for each maintained major (PG15–19) through `license.perPostgresql`. With `verifyAgainstUpstream` enabled, the build verifies both notices against the pinned upstream source. The PG14 entry in the table documents the archived packages. The root notices and earlier copies under `licenses/pg14`, `licenses/pg15`, and `licenses/pg16` also record historical sources.
