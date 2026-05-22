---
name: init-attacks
description: src/data/attacks.js を作成・初期化する。「攻撃データを作って」「attacks.jsを初期化して」「39件のデータを定義して」と言われたときに使う。
disable-model-invocation: false
---

# init-attacks スキル

`src/data/attacks.js` を作成し、39種の攻撃手法データをすべて定義する。

## データ仕様の参照

@.claude/rules/data-spec.md を読んでデータ構造・カテゴリ・全39件リストを確認すること。

## 実装手順

1. `src/data/` ディレクトリが存在しない場合は作成する
2. `src/data/attacks.js` を新規作成する
3. 以下の構造で **39件すべて** を定義する（省略・`...` は絶対に禁止）

```js
// src/data/attacks.js
// サイバー攻撃手法データ定義（39件）

export const CATEGORY_LABELS = {
  all:       'すべて',
  network:   'ネットワーク',
  malware:   'マルウェア',
  social:    'ソーシャル',
  web:       'Web攻撃',
  ddos:      'DoS/DDoS',
  intercept: '傍受・盗聴',
  misc:      'その他'
};

export const RISK_LABELS = {
  1: '低', 2: 'やや低', 3: '中', 4: '高', 5: '最高'
};

export const attacks = [
  // ここに39件をすべて定義する
];
```

4. 作成後、件数を確認する:

!`grep -c "id:" src/data/attacks.js`

件数が `39` であることを確認する。39でなければ不足分を追加する。

## 完了確認

- [ ] `src/data/attacks.js` が存在する
- [ ] `attacks` 配列に39件含まれる
- [ ] すべてのオブジェクトに `id, name, category, risk, layer, target, mechanism, flow, countermeasure, example` フィールドがある
- [ ] `category` の値が定義済みの7種類のいずれかである
- [ ] `risk` が 1〜5 の数値である
- [ ] `flow` が配列（3〜5要素）である
