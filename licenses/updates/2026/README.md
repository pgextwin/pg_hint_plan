# pg_hint_plan upstream 2026 licensing (candidate update support)

The historical source packages remain immutable. These are original byte-for-byte license files from the SHA-pinned candidate series in PR #19.

| Packaging file | Upstream path | Pinned commit or series |
| --- | --- | --- |
| `licenses/updates/2026/COPYRIGHT` | `COPYRIGHT` | PG14–18 (identical blob) |
| `licenses/updates/2026/pg14/COPYRIGHT.postgresql` | `COPYRIGHT.postgresql` | PG14 `cf003edac10606703308209f749b761f9ac39ad0` |
| `licenses/updates/2026/pg15_16/COPYRIGHT.postgresql` | `COPYRIGHT.postgresql` | PG15 `f31082502dee329228f227fd20fc492d259ff41e` / PG16 `6b3c57fe2ac12e5f6f1fb3cbb4873e28125248ae` |
| `licenses/updates/2026/pg17_18/COPYRIGHT.postgresql` | `COPYRIGHT.postgresql` | PG17 `05d080bf80d7b97bf5401a865d9fefd15b7b4c16` / PG18 `9a3f851e1993d6728a9707956dabfcf22cc35b38` |

Current `config/extension.json` keeps its historical license mapping, so existing protected main CI keeps verifying the same original old-release source license bytes. A future **manifest-only candidate PR** can point its `license.perPostgresql` entries to these new paths while updating the five full SHA/ref/version pins. Do not overwrite existing copyright files on main: that would immediately break historical source verification. Keep `verifyAgainstUpstream=true` and byte-for-byte SHA checks on every maintained major.

These files alone do not approve or publish any new Release and cannot substitute for a successful exact candidate audit.
