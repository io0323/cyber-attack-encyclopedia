---
name: add-attack
description: attacks.js に新しい攻撃手法を追加する。「攻撃を追加して」「新しいエントリを追加して」と言われたときに使う。
disable-model-invocation: true
---

# add-attack スキル

`src/data/attacks.js` に新しい攻撃手法エントリを追加する。

## 使い方

```
/add-attack
攻撃名: フォールスルー攻撃
カテゴリ: web
危険度: 3
```

## 実装手順

1. 現在の attacks.js を読んで最大の `id` 値を確認する

!`grep "id:" src/data/attacks.js | tail -5`

2. データ仕様を確認する: @.claude/rules/data-spec.md

3. 新しいエントリを追加する（既存データは絶対に変更しない）:

```js
{
  id: [最大id + 1],
  name: "[攻撃名]",
  category: "[カテゴリ]",   // data-spec.md の7種類のいずれか
  risk: [1〜5],
  layer: "[攻撃フェーズ]",
  target: "[攻撃対象]",
  mechanism: "[仕掛け方（2〜3文）]",
  flow: ["ステップ1", "ステップ2", "ステップ3"],
  countermeasure: "[対策（2〜3文）]",
  example: "[実例・ツール名]"
}
```

4. 追加後に件数を確認する:

!`grep -c "id:" src/data/attacks.js`

## 注意事項

- 既存の39件を変更・削除しない
- `id` の重複禁止
- `category` は定義済みの7種類のみ
- `flow` は必ず配列形式
