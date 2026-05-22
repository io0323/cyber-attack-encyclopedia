---
name: verify-app
description: アプリの動作確認を行う。「動作確認して」「テストして」「ちゃんと動くか確認して」と言われたときに使う。
disable-model-invocation: false
---

# verify-app スキル

アプリの動作を確認し、問題があれば報告・修正する。

## 事前確認（ファイル存在チェック）

!`find . -name "*.js" -o -name "*.css" -o -name "*.html" | grep -v node_modules | sort`

## チェックリスト

以下をすべて確認し、結果を報告すること。

### ファイル構成
- [ ] `index.html` が存在する
- [ ] `src/data/attacks.js` が存在する
- [ ] `src/components/AttackCard.js` が存在する
- [ ] `src/components/DetailPanel.js` が存在する
- [ ] `src/components/FilterBar.js` が存在する
- [ ] `src/styles/main.css` が存在する
- [ ] `src/app.js` が存在する

### データ整合性

!`grep -c "id:" src/data/attacks.js 2>/dev/null || echo "ファイルなし"`

- [ ] attacks.js に39件定義されている（上記コマンドの出力が `39`）

!`node -e "import('./src/data/attacks.js').then(m => { const a = m.attacks; console.log('件数:', a.length); const cats = [...new Set(a.map(x=>x.category))].sort(); console.log('カテゴリ:', cats.join(',')); const missing = a.filter(x => !x.mechanism || !x.countermeasure || !x.flow); console.log('不完全なデータ:', missing.map(x=>x.id).join(',') || 'なし'); })" 2>/dev/null || echo "Node.js確認スキップ（ブラウザで確認）"`

### HTML構造チェック
以下が `index.html` に含まれていることを確認:

!`grep -n "type=\"module\"\|id=\"grid\"\|id=\"detail\"\|id=\"search\"\|data-theme" index.html 2>/dev/null | head -20`

- [ ] `<script type="module">` でESモジュールが読み込まれている
- [ ] `id="grid"` のカードグリッドコンテナが存在する
- [ ] `id="detail"` または相当する詳細パネルが存在する
- [ ] `id="search"` または相当する検索フィールドが存在する
- [ ] `data-theme` 属性でテーマ管理している

### CSS変数チェック

!`grep -c "var(--" src/styles/main.css 2>/dev/null || echo "0"`

- [ ] CSS変数（`var(--xxx)`）が使われている（ハードコードカラーが少ない）

## 報告フォーマット

```
## 動作確認結果

### ✅ 正常
- [問題なし項目]

### ❌ 問題あり
- [問題の内容と該当ファイル]

### 🔧 修正が必要
- [修正内容の提案]
```

問題があれば、確認後すぐに修正を行うこと。
