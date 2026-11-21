# pg_hint_plan — Windows x64 バイナリ

[English](README.md) | 日本語

[pg_hint_plan](https://github.com/ossc-db/pg_hint_plan)の**非公式Windows x64バイナリ**です。SQLの実行計画にヒントを指定する拡張機能です。

## ダウンロードと対応環境

現在のWindowsビルド対象はPostgreSQL **15〜19**です。[pgextwinカタログ](https://pgextwin.github.io/website/ja/)で公開状況を確認し、利用中のメジャーバージョンに合うZIPを選んでください。

PostgreSQL 14のコミュニティサポートは2026年11月12日に終了しました。PostgreSQL 14向けのパッケージは[過去のReleases](https://github.com/pgextwin/pg_hint_plan/releases)から入手できます。

## インストール

1. バックアップを取り、[上流ドキュメント](https://github.com/ossc-db/pg_hint_plan)で導入要件を確認します。
2. 既存ファイルを置き換える前にPostgreSQLを停止します。対応するZIP内のlib/とshare/extension/のファイルを、PostgreSQLの同名ディレクトリへ配置します。
3. PostgreSQLメジャーバージョンごとに対応する上流バージョンが異なります。pg_hint_planのロード方法やCREATE EXTENSIONの要否は利用方法によって異なるため、上流ドキュメントに従って設定してください。
4. 設定の反映後にPostgreSQLを起動し、検証環境で動作を確認してください。

ZIPの整合性は、Releaseに掲載された`SHA256SUMS.txt`で確認できます。SPDX形式のSBOM、脆弱性レポート、署名付き証明の有無もReleaseで確認できます。

## ライセンス

機能、設定、制限事項は[上流のpg_hint_plan](https://github.com/ossc-db/pg_hint_plan)を参照してください。本配布は上流公式のWindows版ではありません。ライセンスは同梱の表記に従います。
