# LIFF × FormBridge 連携 中継ページ

LINEからFormBridgeのフォームを開いたとき、**LINE IDを自動でフォームに渡す**ための中継ページです。

---

## このリポジトリについて

| 項目 | 内容 |
|------|------|
| 用途 | LINE ID（line_uid）をFormBridgeに自動入力する |
| 公開方法 | GitHub Pages |
| 使用技術 | LIFF（LINE Front-end Framework） |

---

## 仕組み

```
LINEのボタン or リッチメニュー
        ↓
LIFF URL をタップ（このページが起動）
        ↓
LINE ID を自動取得
        ↓
FormBridge に ?line_uid=Uxxxxxxxxx を付けてリダイレクト
        ↓
kintone に LINE ID が自動保存される ✅
```

---

## ファイル構成

```
liff-formbridge/
└── index.html   # 中継ページ本体（LINE IDを取得してリダイレクトする）
```

---

## 設定方法

### 1. LINE Developers の設定

1. [LINE Developers Console](https://developers.line.biz/ja/) にログイン
2. **LINEログインチャネル** を作成
3. **LIFF** タブ → LIFFアプリを追加
   - サイズ：Full
   - スコープ：`profile` にチェック
   - エンドポイントURL：`https://あなたのGitHubユーザー名.github.io/liff-formbrdge/`（スペルミスあり）
4. 発行された **LIFF ID** をメモしておく

---

### 2. index.html の編集

以下の2か所をご自身の情報に書き換えてください。

```javascript
const LIFF_ID = "ここにLIFF IDを貼り付け";
const FORMBRIDGE_URL = "ここにFormBridgeのフォームURLを貼り付け";
```

---

### 3. GitHub Pages の有効化

1. リポジトリの **Settings** → **Pages** を開く
2. **Source** を「Deploy from a branch」に設定
3. **Branch** を「main」「/(root)」に設定して保存
4. 数分後に以下のURLでページが公開される

```
https://あなたのGitHubユーザー名.github.io/liff-formbridge/
```

---

### 4. FormBridge の設定

- `line_uid` という名前の **文字列（1行）フィールド** を追加する
- フィールドコードを正確に `line_uid` にする
- 必要に応じてフィールドを **表示** に設定する

---

### 5. LINE リッチメニューの設定

- アクション：**リンク**
- URL：`https://liff.line.me/あなたのLIFF ID`

---

## 注意事項

- LIFF IDは外部に公開しないようにしてください
- LINE IDの取得・利用はプライバシーポリシーに明記することをおすすめします
- フォームを送信しない限りkintoneには保存されません

---

## 関連サービス

- [LINE Developers](https://developers.line.biz/ja/)
- [FormBridge](https://www.forbridge.cybozu.com/)
- [kintone](https://kintone.cybozu.co.jp/)
- [GitHub Pages](https://pages.github.com/)
