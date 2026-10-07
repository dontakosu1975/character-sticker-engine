# 石橋くん作業窓口

このディレクトリは、ChatGPT（チャッピー）側で整理した企画・仕様を、実装担当の石橋くん（Codex）へ安全に引き渡すための作業窓口です。

## 最初に読む順番

1. `ishibashi/CIRCULAR.md` の末尾を確認する（時系列上の正史）。
2. `ishibashi/CURRENT_TASK.md` を読む（現在の正式指示）。
3. `CURRENT_TASK.md` から参照指定された `docs/`、`specs/`、`examples/` を読む。
4. 実装時は `ishibashi/IMPLEMENTATION_RULES.md` を守る。
5. 作業中の詳細は `ishibashi/REPORT.md` に記録する。
6. 作業完了・質問・回答・重要な決定は `CIRCULAR.md` の末尾へ追記する。

## 回覧板ルール

`CIRCULAR.md` は追記専用です。

- 過去の本文を削除・変更・並べ替えしない。
- 訂正も新規項目として追記する。
- `CSE-001` のような連番IDを使う。
- FROM / TO / 種別 / 関連ID / 状態を残す。
- 回覧板は経緯と応答を残す場所であり、仕様書そのものの代用にはしない。

これにより、Gitのコミット履歴を開かなくても、人間とAIの双方がプロジェクトの経緯を時系列で追える状態を維持する。

## 役割分担

- `docs/` : 企画・背景・調査結果。人間とAIが読む。
- `specs/` : エンジンが守る仕様・データ構造。
- `examples/` : うたたねちゃん等の具体例。エンジン本体とは分離する。
- `ishibashi/CIRCULAR.md` : AI間の時系列上の正史。追記専用。
- `ishibashi/CURRENT_TASK.md` : 現在の正式指示。更新可。
- `ishibashi/IMPLEMENTATION_RULES.md` : 現在の固定実装ルール。更新可。
- `ishibashi/REPORT.md` : 作業中の詳細報告・一時作業メモ。更新可。

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
