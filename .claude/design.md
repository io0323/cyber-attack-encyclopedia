# デザイン仕様

## CSS変数（必ずこれを使うこと）

```css
:root {
  /* 背景 */
  --color-bg-primary:   #ffffff;
  --color-bg-secondary: #f8f8f6;
  --color-bg-tertiary:  #f1efe8;

  /* テキスト */
  --color-text-primary:   #1a1a1a;
  --color-text-secondary: #5f5e5a;
  --color-text-tertiary:  #888780;

  /* ボーダー */
  --color-border:       rgba(0, 0, 0, 0.12);
  --color-border-hover: rgba(0, 0, 0, 0.30);

  /* アクセント */
  --color-accent:       #185fa5;

  /* カテゴリカラー */
  --cat-network-bg:   #e6f1fb; --cat-network-text:   #0c447c;
  --cat-malware-bg:   #fcebeb; --cat-malware-text:   #a32d2d;
  --cat-social-bg:    #faeeda; --cat-social-text:    #633806;
  --cat-web-bg:       #eaf3de; --cat-web-text:       #3b6d11;
  --cat-ddos-bg:      #fbeaf0; --cat-ddos-text:      #72243e;
  --cat-intercept-bg: #eeedfe; --cat-intercept-text: #3c3489;
  --cat-misc-bg:      #f1efe8; --cat-misc-text:      #5f5e5a;

  /* 危険度カラー */
  --risk-1: #1d9e75;
  --risk-2: #639922;
  --risk-3: #ba7517;
  --risk-4: #d85a30;
  --risk-5: #a32d2d;

  /* レイアウト */
  --radius-sm: 6px;
  --radius-md: 8px;
  --radius-lg: 12px;
  --shadow-card: none;
}

/* ダークモード */
[data-theme="dark"] {
  --color-bg-primary:   #1e1e1e;
  --color-bg-secondary: #2a2a2a;
  --color-bg-tertiary:  #333333;
  --color-text-primary:   #e8e8e8;
  --color-text-secondary: #a0a0a0;
  --color-text-tertiary:  #6a6a6a;
  --color-border:       rgba(255, 255, 255, 0.12);
  --color-border-hover: rgba(255, 255, 255, 0.30);
  --color-accent:       #85b7eb;
}
```

## レイアウト構造

```
┌─────────────────────────────────────────┐
│ HEADER: タイトル + ダーク切替ボタン       │
├─────────────────────────────────────────┤
│ SEARCH: 🔍 [テキスト入力________________] │
├─────────────────────────────────────────┤
│ FILTERS: [全て] [ネット] [マル] [ソー]... │
├─────────────────────────────────────────┤
│ COUNTER: N件を表示                       │
├─────────────────────────────────────────┤
│ DETAIL: （選択時のみ表示）               │
│ ┌───────────────────────────────────┐   │
│ │ No.X タイトル [カテゴリ]      [×] │   │
│ │ ┌─────────────┬─────────────────┐ │   │
│ │ │ 仕掛け方     │ 対策            │ │   │
│ │ ├─────────────┼─────────────────┤ │   │
│ │ │ 攻撃層/対象  │ 危険度 ████░    │ │   │
│ │ └─────────────┴─────────────────┘ │   │
│ │ フロー: [S1]→[S2]→[S3]→[S4]      │   │
│ └───────────────────────────────────┘   │
├─────────────────────────────────────────┤
│ GRID: repeat(auto-fill, minmax(200px))  │
│ ┌──────────┐ ┌──────────┐ ┌──────────┐ │
│ │ No.1     │ │ No.2     │ │ No.3     │ │
│ │ ネット.. │ │ ポート.. │ │ バッフ.. │ │
│ │[ネットワ]│ │[ネットワ]│ │[その他]  │ │
│ └──────────┘ └──────────┘ └──────────┘ │
└─────────────────────────────────────────┘
```

## カードスタイル

```css
.attack-card {
  background: var(--color-bg-primary);
  border: 0.5px solid var(--color-border);
  border-radius: var(--radius-lg);
  padding: 12px 14px;
  cursor: pointer;
  transition: border-color 0.15s;
}
.attack-card:hover        { border-color: var(--color-border-hover); }
.attack-card.is-active    { border: 1.5px solid var(--color-accent); }
.attack-card.is-risk-high { border-left: 3px solid var(--risk-5); } /* risk=5 のみ */
```

## カテゴリバッジ

```css
.badge {
  display: inline-block;
  font-size: 10px;
  padding: 2px 7px;
  border-radius: 10px;
  font-weight: 500;
}
.badge-network  { background: var(--cat-network-bg);   color: var(--cat-network-text); }
.badge-malware  { background: var(--cat-malware-bg);   color: var(--cat-malware-text); }
.badge-social   { background: var(--cat-social-bg);    color: var(--cat-social-text); }
.badge-web      { background: var(--cat-web-bg);       color: var(--cat-web-text); }
.badge-ddos     { background: var(--cat-ddos-bg);      color: var(--cat-ddos-text); }
.badge-intercept{ background: var(--cat-intercept-bg); color: var(--cat-intercept-text); }
.badge-misc     { background: var(--cat-misc-bg);      color: var(--cat-misc-text); }
```

## アクセシビリティ

- ボタンには `aria-label` を付与
- カードには `role="button"` と `tabindex="0"` を付与
- 詳細パネルには `role="region"` と `aria-label` を付与
- キーボード操作:
  - `Enter` / `Space`: カード選択
  - `Escape`: 詳細パネルを閉じる
  - `←` `→`: 前後のカードへ移動

## レスポンシブ対応

```css
/* モバイル（375px〜） */
@media (max-width: 600px) {
  .detail-body { grid-template-columns: 1fr; }
  .filter-tabs { gap: 4px; }
  .tab         { font-size: 11px; padding: 3px 8px; }
}
```
