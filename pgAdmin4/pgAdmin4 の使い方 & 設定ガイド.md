# pgAdmin4 の使い方 & 設定ガイド

## 📌 目次

1. pgAdmin4 の基本構造
2. データベースの確認方法
3. テーブルデータの表示方法
4. タブ名を短くする設定
5. SQL クエリの実行方法
---
1. **pgAdmin4 の基本構造**
pgAdmin4 は PostgreSQL のデータベース管理ツールで、以下のような構成になっています。

- Databases（データベース一覧）
  - craftlink_development（開発環境）
  - craftlink_production（本番環境）
- Schemas（スキーマ）
  - public（デフォルトのスキーマ）
- Tables（テーブル）
  - users（ユーザー情報）
  - job_posts（作業員募集）
  - applications（応募情報）
  - schema_migrations（マイグレーション管理）
---
## 2. **データベースの確認方法**
データベースが正しく作成されているか確認する
```bash
SELECT table_name FROM information_schema.tables WHERE table_schema = 'public';
```
---
## 3. **テーブルデータの表示方法**
### ✅ __GUI でデータを表示する方法__
  1. 左メニューで「Tables」→ users を右クリック
  2. 「View/Edit Data」→「All Rows」 を選択
  3. 右側のウィンドウに users テーブルのデータが表示される

✅ __SQL クエリでデータを取得する方法__
```bash
SELECT * FROM users;
```
---
## 4. **タブ名を短くする設定**
pgAdmin4 のタブ名が長すぎる場合、以下の手順で短縮できます。

1. 「File（ファイル）」→「Preferences（設定）」を開く
2. 「Browser（ブラウザ）」→「Tab settings（タブ設定）」を選択
3. 「View/Edit Data tab title」の値を変更
   - 変更前: %SCHEMA%.%TABLE%/%DATABASE%/%USERNAME%@%SERVER%
   - 変更後: %TABLE%
4. 「Save」を押して設定を保存
5. pgAdmin4 を再起動し、タブ名が短くなったか確認
---
## 5. **SQL クエリの実行方法**
job_posts のデータを取得する
```bash
SELECT * FROM job_posts;
```
