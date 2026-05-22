# Cyber Attack Encyclopedia

## プロジェクト概要

サイバー攻撃手法39種を解説するインタラクティブWebアプリ。
SC試験（情報処理安全確保支援士）の学習支援を目的とする。

## ディレクトリ構成

```
cyber-attack-encyclopedia/
├── CLAUDE.md
├── index.html              ← エントリーポイント
├── src/
│   ├── data/attacks.js     ← 39件の攻撃データ（ESモジュール）
│   ├── components/
│   │   ├── AttackCard.js
│   │   ├── DetailPanel.js
│   │   └── FilterBar.js
│   ├── styles/main.css
│   └── app.js
└── .claude/
    ├── settings.json
    ├── rules/
    └── skills/
```

## 技術スタック

- **言語**: Vanilla JS（ESモジュール） + HTML + CSS
- **フレームワーク**: なし（ビルドツール不要）
- **アイコン**: Tabler Icons CDN のみ許可
- **動作条件**: index.html をブラウザで直接開いて完全動作すること

## 参照ドキュメント

詳細なルール・データ構造は `.claude/rules/` を参照:
- コーディング規約: @.claude/rules/coding.md
- データ仕様: @.claude/rules/data-spec.md
- デザイン仕様: @.claude/rules/design.md

## よく使うコマンド

```bash
# プレビュー（Antigravityの内蔵ブラウザ推奨）
open index.html

# ファイル構成確認
find src -type f | sort
```
