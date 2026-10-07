# LINEスタンプ調査メモ

確認日: 2026-10-07

> 実装時には必ずLINE Creators Market公式の最新仕様を再確認すること。この文書の数値は2026-10-07時点の設計基準。

## 1. 通常スタンプ公式仕様

LINE Creators Market公式制作ガイドラインより。

- スタンプ画像: 8 / 16 / 24 / 32 / 40個
- 最大 370 × 320 px
- メイン画像: 240 × 240 px
- トークルームタブ画像: 96 × 74 px
- PNG
- RGB
- 画像1個につき1MB以下
- 縦横は偶数px
- 72dpi以上

公式は「日常会話、コミュニケーションで使いやすいもの」「表情、メッセージ、イラストが分かりやすくシンプルなもの」を推奨している。

Source:
https://creator.line.me/ja/guideline/sticker/

## 2. よく使われる表現

LINE Creators Market公式のタグ別送信傾向では、全年代・性別を問わず最も使われている表現は「OK/了解」。love / happy / good などポジティブな感情表現も人気とされている。

このため初期Strategyでは `acknowledge` を必須カテゴリとし、ポジティブ表現を一定数含める。

Source:
https://creator.line.me/ja/stickermaker/tips/expression/

## 3. 商品設計への反映

公式傾向から、エンジンでは以下を仮説として採用する。

- キャラクター芸だけで全枠を埋めない。
- OK/了解、ありがとう、挨拶、謝罪など用途が明確なものを優先する。
- ポジティブ感情を一定割合入れる。
- 小画面でも用途が即座に理解できる構図を優先する。
- 同じポーズや似た表現ばかりにしない。
- キャラクター固有表現は「商品として使える基本表現」に混ぜる。

これらはLINEの公式数値そのものではなく、本プロジェクトの設計ヒューリスティック。

## 4. 審査

販売できるのはLINE Creators Marketの審査で適切と判断されたもの。フォーマット違反、日常会話で使いにくいもの等は却下または販売中止となる場合がある。

エンジンのvalidatorは審査を保証するものではない。機械的に確認できる項目と、既知のリスク候補を事前警告するpreflight checkと位置付ける。

Source:
https://creator.line.me/ja/review_guideline/

## 5. アニメーションスタンプ

将来profileとして対応する。

2026-10-07確認時点:
- 8 / 16 / 24個
- 最大 320 × 270 px
- APNG
- main: 240 × 240 APNG
- tab: 96 × 74 PNG

Source:
https://creator.line.me/ja/guideline/animationsticker/

## 6. 更新ポリシー

LINE仕様は変更され得るため、実装では:

1. 仕様値をplatform profileへ集約する。
2. profileに`checkedAt`と公式URLを持たせる。
3. 公開パッケージ生成時に古いprofileなら警告する。
4. ブラウザ自動化は画面仕様変更の影響を受ける前提で分離する。
