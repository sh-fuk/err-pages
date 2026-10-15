# Error Pages

エラーページを作れるサイトです。

友達に送りつけるなり自分のサイトのエラーページにするなり遊んでください

ご利用は完全自己責任で、、、、、、

## 使い方

1. `index.html` をブラウザで開く（`assets.js` を同じフォルダに置いたまま）
2. 左のパネルでサービスを選ぶ
3. プリセットを押すか、「内容」の各欄を書き換える → 右のプレビューに即反映

| ボタン | 動作 |
|---|---|
| 開く | 新しいタブで全画面表示 |
| 保存 | 生成したエラーページを `.html` としてダウンロード |
| コピー | 生成した HTML をクリップボードへ |
| 共有 | 入力内容を URL の `#` 以降に埋め込んでコピー（開くと同じ状態を復元） |
| リセット | そのサービスの初期値に戻す |

保存・コピーした HTML は画像や CSS を埋め込んだ単体ファイルなので、そのまま置くだけで表示できます（Discord の Nelly の GIF のみ外部読み込み）。

## 対応サービス

| サービス | ベース | 編集できる主な項目 |
|---|---|---|
| Google | 404ページ | コード、ステータス、本文、URL パス |
| GitHub | 404ページ | 大きな数字、吹き出しの文言、検索欄のラベル |
| Cloudflare | 502ページ（timeout） | 見出し、エラーコード、どこがErrorか、What happened? / What can I do?、Ray ID |
| Discord | 404ページ | 見出し、本文、リンク |
| Microsoft | microsoft.comの404ページ | 見出し、本文 |
| IIS | go.microsoft.comの404ページ | ヘッダー、見出し、本文 |
| nginx | 組み込みのエラーページ | コード、ステータス、サーバー名 |
| Apache | Apache httpd2.4のエラーページ | 見出し、本文、署名 |

マークアップや素材は 2026 年 10 月時点の各社の実際のページから取得したものです。各社のデザイン変更により、本物と差が出ることがあります。

## ファイル構成

```
index.html          ツール本体（UI・各サービスのテンプレート）
assets.js           実際のページから抽出した素材（CSS、画像、SVG）
```

テンプレートは `index.html` の `TEMPLATES` に、次の形で定義しています。

```js
example: {
  name: "表示名",
  fields: [{ key: "code", label: "エラーコード", value: "404" }],  // 編集欄（type: "textarea" / "select" も可）
  presets: { "500": { code: "500" } },                              // ワンクリック差し替え
  render: v => `<!DOCTYPE html>...${esc(v.code)}...`,               // 値 → HTML
},
```

追加したら、`NAV`（左パネルの並び）と `LOGOS`（アイコン）にも登録してください。

## クレジット・注意

- ジョーク・個人利用向けのツールです。生成したページを公開して本物と誤認させたり、なりすましに使ったりしないでください。
- 各ロゴ・画像・商標は各社に帰属します。
- ナビのアイコン：Google（gstatic 配布の公式 G）、Cloudflare（ダッシュボードのロゴ）、Microsoft / IIS（4 色スクエア）、その他は [Simple Icons](https://simpleicons.org/)（CC0）
- Cloudflare テンプレートの HTML 構造は [donlon/cloudflare-error-page](https://github.com/donlon/cloudflare-error-page)（MIT）を参考にしています。
