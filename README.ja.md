# ECHO TYPOGRAPHY

**引き算のタイポグラフィ。** キーボード駆動・モノクローム・HTML 1ファイル。

🇬🇧 [English version](./README.md)

---

## コンセプト

キャンバスは最初から「満ちている」。
あなたは置くのではなく、**削る**。
余白こそが媒体であり、キーを押すたびに空間が彫られていく。

Constraint Systems の実験的ツール群に影響を受けた作品。
UI・装飾を徹底的に削ぎ落とし、機能だけで美を成立させる。

## 起動

ビルド不要。`index.html` を直接開く：

```bash
open index.html                   # macOS
# あるいはローカルサーバー：
python3 -m http.server 8080
```

初回アクセスのみ React・Tailwind・Space Mono を CDN から取得するためオンラインが必要。

## 操作

| キー      | 動作                                   |
| --------- | -------------------------------------- |
| `H J K L` | カーソル移動（Vim 流）                 |
| `SPACE`   | セルを削除／復元（トグル）             |
| `ENTER`   | 全面充填・字源を循環                   |
| `S` / `B` | フォントサイズ − / +                   |
| `I`       | 白黒反転                               |
| `P`       | 現在の状態を SVG として書き出し        |
| `?`       | ヘルプの表示／非表示                   |
| `ESC`     | ヘルプを閉じる                         |

起動時にヘルプが中央に出ます。何か操作キーを押すと自動で消え、`?` で再表示できます。

## 構成

```
echo_typography/
├── index.html       — アプリ本体（自己完結、約390行）
├── README.md        — 英語版
└── README.ja.md     — 本ファイル
```

## 技術スタック

- **React 18** — import map + `esm.sh` 経由で CDN ロード
- **Babel Standalone** — `data-type="module"` でブラウザ内 JSX → ESM 変換
- **Tailwind CSS** — Play CDN、JIT（任意値対応）
- **lucide-react** — タイトル横の装飾アイコン 1 個だけ
- **Space Mono 700** — Google Fonts

バンドラー・`npm install` 不要のランタイム完結型。

## 改変ポイント

`index.html` 冒頭に意図的に露出させた場所：

- `SOURCES` — `ENTER` で循環する字源ワード配列
- `SIZE_MIN` / `SIZE_MAX` / `SIZE_STEP` — サイズ境界
- グレインの `opacity` — 唯一の非本質な視覚要素。控えめに調整
- `exportSVG` — ベクター書き出し。PNG 追加も Canvas 経由で容易

ステートは `{ ch, hid }` の 2D 配列 1 本のみ。自由に fork 可能。

## 設計メモ

- **1 行 = 1 テキストラン** — 各グリッド行を単一 `<div>` の pre 整形テキストとして描画。数千セル規模でも軽快
- **カーソル `mix-blend-mode: difference`** — 黒背景・白字・反転モードいずれでも常時可視
- **レイアウト保存リサイズ** — `S` / `B` でサイズを変えても `(行, 列)` 座標一致で彫刻パターンが保存される
- **フィルムグレイン** — 静的 SVG `feTurbulence`、脱色、opacity 11%、overlay 合成

## ブラウザ要件

ネイティブ import map 対応ブラウザ：Chrome 89+ / Safari 16.4+ / Firefox 108+。

## 思想

> 余計な装飾を削ぎ落とし、機能そのものが美しさを定義する。

—

© kinoshita studio
