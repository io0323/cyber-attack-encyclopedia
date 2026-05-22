# コーディング規約

## 絶対に守るルール

### 技術制約
- フレームワーク（React/Vue/Angular等）使用禁止
- `npm install` が必要な依存関係禁止
- `node_modules` の生成禁止
- `localhost` サーバーが必要な構成禁止
- `eval()` 使用禁止
- `document.write()` 使用禁止

### セキュリティ
- `innerHTML` へのユーザー入力の直接挿入禁止（XSS対策）
- ユーザー入力は必ず `textContent` で挿入すること
- DOM操作は必ずnullチェックを行うこと

```js
// ✅ 正しい
const el = document.querySelector('.card');
if (el) el.textContent = attack.name;

// ❌ 禁止
document.querySelector('.card').innerHTML = userInput;
```

### モジュール設計
- 1ファイル = 1責務（複数コンポーネント混在禁止）
- グローバル変数禁止（`app` オブジェクトに集約）
- `addEventListener` を使用（インライン `onclick` 禁止）
- データとUIを必ず分離（attacks.jsのデータをDOMに直接書かない）

### スタイル
- 色・サイズのハードコード禁止 → 必ず `var(--xxx)` を使用
- `!important` の多用禁止（緊急時のみ）

### コメント・命名
- コメントはすべて日本語
- 変数名・関数名は英語（キャメルケース）
- CSSクラス名はケバブケース（`attack-card`, `detail-panel`）

## 実装の進め方

1. 対象ファイルを必ず `Read` で読んでから編集する
2. 1ファイルずつ完成させてから次へ進む
3. 既存動作を壊す変更は事前に確認する
4. attacks.js は必ず39件すべてを定義する（省略禁止）

## 完了報告フォーマット

実装完了時は必ず以下の形式で報告:

```
## 完了内容
- [完了したファイルと内容]

## 確認済み
- [テストした内容]

## 残タスク
- [次にやること]
```
