# IMPLEMENTATION RULES

Character Sticker Engine を実装する際の固定ルール。

## 1. キャラクターとエンジンを分離する

エンジンは「うたたねちゃん」を知らない構造にする。

禁止例：
- `if character == "utatane"`
- ペンギン固有の色・翼・体型を処理コードに持つ
- 固有セリフをエンジンへ直書きする

Character Pack / Sticker Set / assets の交換で別キャラクターへ切り替えられること。

## 2. コードはキャラクターを描かない

正本画像・承認済み生成素材を入力として扱う。

コードの責務：
- リサイズ
- 透過確認
- 余白調整
- canvas配置
- ファイル命名
- 容量確認
- 規格検証
- preview生成
- package生成

コードの責務ではないもの：
- キャラクターの顔を描き直す
- 手足や輪郭を推測して再造形する
- 「似た感じ」のベクターへ置換する

## 3. 外部仕様をハードコードしすぎない

LINEの画像サイズ・枚数・容量・フォーマット等は platform profile として分離する。仕様変更時にエンジン本体を書き換えず更新できる構造を優先する。

## 4. 生成と公開を分離する

`generate -> validate -> review -> package -> submit -> release`

を独立した段階として扱う。

特に `submit` と `release` は Human-in-the-loop を基本とし、PoC①では実装対象外。

## 5. 検品を成果物にする

成功/失敗だけでなく、人間とAIの双方が読める validation report を生成する。

最低限：
- 対象ファイル
- pixel dimensions
- file size
- format
- alpha/transparency
- naming
- set count
- error/warning

## 6. 目視レビューを軽くする

全スタンプを一覧できる contact sheet / preview を自動生成する。1枚ずつ開かなくても、作画崩壊・文字切れ・余白異常・キャラ不一致を見つけられること。

## 7. AI生成は差し替え可能なadapterとして扱う

Canva等の画像生成・編集サービスを利用する場合も、エンジン本体と密結合させない。

将来、別の画像生成手段へ変更しても、Character Pack以降の処理が再利用できること。

## 8. 小さく検証する

PoC①で必要なのは「出版プラットフォーム」ではなく「1セットを正しく作れるパイプライン」。

先回りしてWebサービス、アカウント管理、課金、巨大GUI、複雑なプラグインシステムを作らない。

## 9. 変更時の報告

作業終了時は `ishibashi/REPORT.md` に以下を記録する。

- 実施内容
- 変更ファイル
- 動作確認
- 未解決事項
- 次に判断が必要なこと

仕様を独断で変更した場合は、その理由を必ず記載する。
