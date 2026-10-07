# 石橋くん作業窓口

このディレクトリは、ChatGPT（チャッピー）側で整理した企画・仕様を、実装担当の石橋くん（Codex）へ安全に引き渡すための作業窓口です。

## 基本運用

1. 石橋くんは作業開始時に `ishibashi/CURRENT_TASK.md` を最初に読む。
2. `CURRENT_TASK.md` から参照指定された `docs/`、`specs/`、`examples/` を読む。
3. 不明点・仕様矛盾があれば推測で大きく実装せず、`ishibashi/REPORT.md` に記録する。
4. 作業完了時は `ishibashi/REPORT.md` を更新する。
5. 次の作業指示は原則 `CURRENT_TASK.md` の差し替えで行う。

## 役割分担

- `docs/` : 企画・背景・調査結果。人間とAIが読む。
- `specs/` : エンジンが守る仕様・データ構造。
- `examples/` : うたたねちゃん等の具体例。エンジン本体とは分離する。
- `ishibashi/` : 実装担当への入口・現在タスク・作業報告。

## 重要原則

- Character Sticker Engine は、うたたねちゃん専用にしない。
- キャラクター固有情報は Character Pack / Sticker Set 側へ置き、エンジンへハードコードしない。
- キャラクターの造形をコードで再解釈・再描画しない。確定した正本素材を使う。
- LINE等の外部サービス仕様は変更され得るため、検証可能な設定・プロファイルとして分離する。
- 審査申請・公開など不可逆または外部影響の大きい操作には Human-in-the-loop を残す。
- PoCでは最短経路を優先し、巨大な汎用基盤を先回りして作らない。

## 石橋くんへ共有するとき

原則として、このURLだけを渡せば開始できる状態を維持する。

`https://github.com/dontakosu1975/character-sticker-engine/tree/main/ishibashi`
