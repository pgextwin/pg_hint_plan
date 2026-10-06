# pg_hint_plan Windows バイナリ

[English](README.md) | **日本語**

このリポジトリでは、[pg_hint_plan](https://github.com/ossc-db/pg_hint_plan) の **非公式 Windows x64 バイナリ**を提供します。

pg_hint_plan本体のHint構文、設定、機能仕様、制限事項はupstreamの公式ドキュメントを正規の情報源としてください。このリポジトリは一般的なWindows版PostgreSQL向けの再現可能なbuildと配布を担当します。

## PostgreSQL別upstream

pg_hint_planはPostgreSQLメジャーバージョンごとに別のstable release系列を持ちます。

| PostgreSQL | upstream ref | pg_hint_plan | 検証PostgreSQL |
|---:|---|---:|---:|
| 14 | `REL14_1_4_4` | 1.4.4 | 14.24 |
| 15 | `REL15_1_5_3` | 1.5.3 | 15.19 |
| 16 | `REL16_1_6_2` | 1.6.2 | 16.15 |
| 17 | `REL17_1_7_1` | 1.7.1 | 17.11 |
| 18 | `REL18_1_8_0` | 1.8.0 | 18.6 |

初回pgextwin Release tagは最新系列を代表して:

~~~text
v1.8.0-windows.1
~~~

とします。ただし各ZIPは必ず、そのPostgreSQLメジャーに対応する表記上のupstream refからbuildします。

## インストール

1. PostgreSQLを停止します。
2. 使用中のPostgreSQLメジャーと一致するZIPを展開します。
3. `lib/pg_hint_plan.dll` をPostgreSQLの `lib` へコピーします。
4. `share/extension/*` をPostgreSQLの `share/extension` へコピーします。
5. 必要に応じて `shared_preload_libraries = 'pg_hint_plan'` を設定します。
6. PostgreSQLを再起動します。
7. 対象databaseで次を実行します。

~~~sql
CREATE EXTENSION pg_hint_plan;
~~~

詳しいWindows手順は [docs/windows_ja.md](docs/windows_ja.md) を参照してください。

## Windows互換処理

PG17/18ではupstreamの `query_scan.l` からwin_flexでscanner sourceを生成してMSVCでcompileします。

PG14〜16では、pg_hint_planがWindows版PostgreSQL DLLからexportされていないquery-jumble実装にも依存します。このためpgextwinは対象minorと完全一致する**PostgreSQL公式source archive**を取得し、SHA-256を照合してから必要なquery-jumble objectだけを再buildしてlinkします。

不透明なprecompiled objectはrepositoryに保存しません。

CIではPG14〜18すべてについて:

- PostgreSQL起動
- `CREATE EXTENSION pg_hint_plan`
- `SeqScan(...)` Hintの実適用
- `IndexScan(...)` Hintの実適用
- PG14〜16ではhint-table/query-id互換経路

まで確認しています。

## ライセンス

upstreamの `COPYRIGHT` と `COPYRIGHT.postgresql` を保持します。

PG14〜16系列では `COPYRIGHT.postgresql` の本文が異なるため、CI照合用に各系列の正確なcopyを `licenses/` 以下へ保持しています。Release ZIPには実際にbuildしたupstream checkoutのcopyright fileを直接収録します。

このWindowsバイナリはpgextwinによる非公式配布であり、upstream pg_hint_planの公式Windowsバイナリではありません。
