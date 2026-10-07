# Character Sticker Engine

キャラクターの正本資料から、LINEスタンプの商品企画・素材制作・規格化・検品・公開準備までを再利用可能なパイプラインとして扱うためのプロジェクトです。

## 最初の実証キャラクター

**うたたねちゃん**をPoCキャラクターとして使用します。

ただし、本リポジトリの目的は「うたたねちゃん専用スタンプ制作ツール」を作ることではありません。キャラクター固有情報を Character Pack に分離し、別キャラクターへ差し替えても同じ工程を再利用できる **Character Sticker Engine** を目標とします。

## ゴール

`Character Reference → Character Pack → 商品企画 → 台詞・表情・ポーズ設計 → 画像制作 → LINE規格化 → 自動検品 → Creators Market登録支援 → 人間確認 → 審査申請・公開`

最終目標は完全無人公開ではなく、公開直前までを自動化し、外部への確定操作だけ人間が承認する **ワンクリック出版** です。

## 設計原則

- キャラクターの造形をコード側で再解釈しない。正本画像を基準にする。
- キャラクター固有データと、LINE向け生成・検品エンジンを分離する。
- LINEの現行仕様値をコードへ散在させず、platform profile として管理する。
- 画像生成は自由生成ではなく Character Reference に拘束する。
- 「かわいい」だけでなく「実際に会話で使える」セットを自動設計する。
- 審査申請・公開など不可逆性の高い外部操作は Human-in-the-loop とする。
- うたたねちゃんで成立したルールを、2キャラクター目で再検証してから汎用仕様として固定する。

## 初期ドキュメント

- `docs/PROJECT_PLAN.md` — 企画書
- `docs/SPECIFICATION.md` — エンジン仕様書
- `docs/UTATANE_POC.md` — うたたねちゃん第1弾PoC
- `docs/AUTOMATION.md` — 自動化・公開フロー
- `docs/RESEARCH.md` — LINE公式仕様・利用傾向の調査メモ
- `schemas/character-pack.example.json` — Character Packの初期案
- `schemas/sticker-set.example.json` — スタンプセット定義の初期案

## Status

Planning / PoC preparation — 2026-10-07
