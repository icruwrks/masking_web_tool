# masking_web_tool
テキストをマスキングするツール

# 概要

## SQLのテーブルやカラムの変換ツール

- テキストを入力できるフォームがあり、SQL文を入れて、変換ボタンを押すと、カラム名やテーブル名を一般化したものを出力する
- 目的としてはAIや検索等でSQLを調べる際に、セキュリティ的にカラムやテーブルなどの情報を入れたくないからである
- 変換はセキュリティ的にアウトなものにできれば良い

### 入力例
```sql
SELECT employee_id, first_name, last_name, salary
FROM employees
WHERE department_id = 10;
```

### 出力例
```sql
SELECT column1, column2, column3, column4
FROM table1
WHERE column5 = 10;
```

## 使用方法

1. `index.html` をブラウザで開く
2. 入力フォームにSQLを入力
3. 「変換実行」ボタンをクリック
4. マスキングされたSQLが出力される

## 機能

### 基本機能
- **SQLマスキング**: テーブル名とカラム名を一般化された名前に変換
- **リアルタイム変換**: ブラウザ上で即座に処理
- **クリア機能**: 入力と出力の内容をリセット

### 変換ロジック
- **テーブル名識別**: `FROM`、`JOIN`キーワード後の識別子をテーブル名として認識
- **カラム名識別**: SQLキーワード、数値以外の識別子をカラム名として認識
- **順次命名**: テーブル名は`table1`, `table2`...、カラム名は`column1`, `column2`...に変換
- **大文字小文字対応**: SQLの特性に合わせて柔軟に処理

### セキュリティ考慮
- 機密情報の漏洩防止を目的とした設計
- 変換後の内容確認を促すUI
- ローカル処理のため、外部への情報送信なし

## ファイル構成

```
masking_web_tool/
├── README.md       # このファイル
└── index.html      # SQLマスキングツール本体
```

## 対応SQL
- 基本的なSELECT、INSERT、UPDATE、DELETE文
- JOIN構文（INNER、LEFT、RIGHT、FULL OUTER JOIN）
- WHERE、GROUP BY、ORDER BY、HAVING句
- サブクエリやCTEにも対応

## 注意事項
- このツールは機密情報を含むSQLを安全に共有するためのものです
- 変換後も十分に内容を確認してから使用してください
- 複雑なSQL文では完全にマスキングできない場合があります