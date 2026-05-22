# データ仕様

## attacks.js のデータ構造

```js
export const attacks = [
  {
    id: 1,                            // 通し番号 1〜39（必須・一意）
    name: "ネットワークスキャン",       // 攻撃手法名（必須）
    category: "network",              // カテゴリ（必須・下記の値のみ）
    risk: 2,                          // 危険度 1(低)〜5(最高)（必須）
    layer: "偵察フェーズ",             // 攻撃フェーズ・レイヤー（必須）
    target: "ネットワーク全体",         // 攻撃対象（必須）
    mechanism: "ICMPやTCPパケットを...", // 仕掛け方（必須・2〜3文）
    flow: [                           // 攻撃フロー（必須・3〜5ステップ）
      "スキャンパケット送信",
      "応答収集",
      "ホスト・ポート一覧作成",
      "脆弱性調査へ"
    ],
    countermeasure: "ファイアウォール...", // 対策（必須・2〜3文）
    example: "nmapによる..."             // 実例・ツール名（必須）
  }
];
```

## カテゴリ定義（category フィールドの値）

| 値 | 表示名 | 対象ID |
|----|--------|--------|
| `network` | ネットワーク | 1, 2, 11, 12, 13, 15, 20 |
| `malware` | マルウェア | 7, 8, 19, 34 |
| `social` | ソーシャル | 9, 10, 29 |
| `web` | Web攻撃 | 21, 30, 31, 33, 35, 37, 38 |
| `ddos` | DoS/DDoS | 22, 23, 24, 25, 26, 27, 28 |
| `intercept` | 傍受・盗聴 | 14, 16, 17, 18 |
| `misc` | その他 | 3, 4, 5, 6, 32, 36, 39 |

## 39種の攻撃手法（全リスト）

```
No.01 ネットワークスキャン        category=network    risk=2
No.02 ポートスキャン              category=network    risk=2
No.03 バッファオーバフロー攻撃    category=misc       risk=5
No.04 ブルートフォース攻撃        category=misc       risk=3
No.05 辞書攻撃                    category=misc       risk=3
No.06 パスワードリスト攻撃        category=misc       risk=4
No.07 マルウェア感染              category=malware    risk=5
No.08 ランサムウェア              category=malware    risk=5
No.09 フィッシング                category=social     risk=4
No.10 標的型攻撃（APT）           category=social     risk=5
No.11 IPスプーフィング            category=network    risk=3
No.12 踏み台攻撃                  category=network    risk=3
No.13 ARPスプーフィング           category=network    risk=4
No.14 セッションハイジャック      category=intercept  risk=4
No.15 リプレイ攻撃                category=network    risk=3
No.16 MITB攻撃                    category=intercept  risk=5
No.17 スニファ                    category=intercept  risk=3
No.18 電波傍受                    category=intercept  risk=3
No.19 キーボードロギング          category=malware    risk=4
No.20 DNSキャッシュポイズニング   category=network    risk=4
No.21 ディレクトリトラバーサル    category=web        risk=4
No.22 DDoS攻撃                    category=ddos       risk=4
No.23 F5アタック                  category=ddos       risk=2
No.24 TCP SYNフラッド             category=ddos       risk=4
No.25 Ping of Death               category=ddos       risk=3
No.26 ランダムサブドメイン攻撃    category=ddos       risk=3
No.27 ICMPフラッド                category=ddos       risk=3
No.28 Smurf攻撃                   category=ddos       risk=3
No.29 スパムメール                category=social     risk=2
No.30 クロスサイトスクリプティング（XSS） category=web risk=4
No.31 SQLインジェクション         category=web        risk=5
No.32 ゼロデイ攻撃                category=misc       risk=5
No.33 セッションID固定化攻撃      category=web        risk=3
No.34 ルートキット攻撃            category=malware    risk=5
No.35 フォームジャッキング攻撃    category=web        risk=4
No.36 ドメイン名ハイジャック攻撃  category=misc       risk=4
No.37 OSコマンド・インジェクション category=web       risk=5
No.38 クロスサイトリクエストフォージェリ（CSRF） category=web risk=3
No.39 サプライチェーン攻撃        category=misc       risk=5
```

## 定数定義（app.js で使用）

```js
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
  1: '低',
  2: 'やや低',
  3: '中',
  4: '高',
  5: '最高'
};
```
