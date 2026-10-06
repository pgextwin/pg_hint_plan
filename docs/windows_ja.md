# pg_hint_plan Windows x64 バイナリ利用ガイド

この文書は、pgextwinが配布する非公式pg_hint_plan Windows x64バイナリの補足ガイドです。

## 対応するZIPを選ぶ

PostgreSQLのメジャーごとにupstream pg_hint_plan releaseが異なります。必ずPostgreSQLメジャーと一致するZIPを使用してください。

~~~text
PG14 -> pg_hint_plan-REL14_1_4_4-pg14-windows-x64.zip
PG15 -> pg_hint_plan-REL15_1_5_3-pg15-windows-x64.zip
PG16 -> pg_hint_plan-REL16_1_6_2-pg16-windows-x64.zip
PG17 -> pg_hint_plan-REL17_1_7_1-pg17-windows-x64.zip
PG18 -> pg_hint_plan-REL18_1_8_0-pg18-windows-x64.zip
~~~

## 配置

一般的なEDB PostgreSQL InstallerでPG18を使用している例:

~~~text
C:\Program Files\PostgreSQL\18\
~~~

配置先:

~~~text
ZIP\lib\pg_hint_plan.dll
  -> <PostgreSQL>\lib\pg_hint_plan.dll

ZIP\share\extension\*
  -> <PostgreSQL>\share\extension\
~~~

## preload

pg_hint_planを常時利用する場合は `postgresql.conf` に:

~~~conf
shared_preload_libraries = 'pg_hint_plan'
~~~

を設定してPostgreSQLを再起動します。

既存のpreload対象がある場合はカンマ区切りで追加してください。

## Extension作成

~~~sql
CREATE EXTENSION pg_hint_plan;
~~~

確認:

~~~text
\dx pg_hint_plan
~~~

## 基本確認

Index Scanを指定する例:

~~~sql
/*+ IndexScan(my_table my_table_pkey) */
SELECT *
FROM my_table
WHERE id = 1;
~~~

実際にHintが使われたかは `EXPLAIN` で確認してください。

~~~sql
/*+ SeqScan(my_table) */
EXPLAIN (COSTS OFF)
SELECT *
FROM my_table
WHERE id = 1;
~~~

Hint構文、利用可能なHint、hint table、query-idの仕様はupstreamドキュメントを参照してください。

## PG14〜16のWindows互換処理

PG14〜16ではpg_hint_planがPostgreSQL coreのquery-jumble処理を直接利用しますが、その実装は通常のWindows PostgreSQL DLLからexportされません。

pgextwinはpackage作成時に対象PostgreSQLの公式source archiveを取得し、SHA-256を検証してから必要objectを再compileします。

対象:

- PostgreSQL 14.24
- PostgreSQL 15.19
- PostgreSQL 16.15

PostgreSQL minor更新時には、共通metadataの更新と同時にsource archive SHA-256およびcompatibility buildを再検証する必要があります。

## 更新時の注意

PostgreSQL majorを更新するときは新major向けZIPへ入れ替えてください。例えばPG17用DLLをPG18で流用してはいけません。

pg_hint_plan自体もPostgreSQL majorごとにstable系列が異なるため、単純に「同じpg_hint_plan versionを全PostgreSQLで使用する」構成ではありません。

## 公式情報

- upstream repository: https://github.com/ossc-db/pg_hint_plan
- 各releaseのREADME/ドキュメントは使用するPostgreSQL majorに対応したupstream tagを参照してください。

本体仕様についてこの文書とupstreamに差異がある場合は、upstreamを優先してください。
