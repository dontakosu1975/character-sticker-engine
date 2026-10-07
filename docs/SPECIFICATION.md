# Character Sticker Engine 仕様書 v0.1

更新日: 2026-10-07

## 1. アーキテクチャ

エンジンはキャラクター固有情報とプラットフォーム固有情報を分離する。

```text
Character Pack
     ↓
Set Planner
     ↓
Motion / Expression Planner
     ↓
Asset Provider Adapter
     ↓
Asset Processor
     ↓
Platform Validator
     ↓
Preview / Package Builder
     ↓
Publisher Adapter
     ↓
Human Approval
```

### Character Pack
キャラクターの正本。名前、外見、禁止変更点、Reference画像、表情、既存モーション、性格、台詞トーンなどを保持する。

### Set Planner
用途タグとStrategyからセット全体の役割配分を決める。キャラクター固有ロジックを持たない。

### Motion / Expression Planner
各スタンプについて `message + communicationTag + emotion + motion + intensity` を定義する。

### Asset Provider Adapter
Canva等の制作サービス、人間制作、既存素材のいずれでも同じ入力形式へ揃える。エンジンを特定生成AIへ固定しない。

### Asset Processor
透過、クロップ、余白、リサイズ、色空間、容量、命名等を処理する。

### Platform Validator
LINE公式仕様など、対象プラットフォームの規則を検査する。仕様値はprofile化する。

### Preview / Package Builder
一覧プレビュー、main、tab、個別画像、メタデータ、アップロード用成果物を生成する。

### Publisher Adapter
Creators Market等への登録支援を担当する。UI変更に弱いブラウザ自動化はエンジン本体から隔離する。

## 2. Character Pack 最低要件

必須:
- `characterId`
- `displayName`
- `version`
- `referenceAssets`
- `visualRules`
- `personality`
- `speechStyle`
- `allowedMotions`
- `forbiddenChanges`

推奨:
- front / side / back reference
- expression samples
- color palette
- proportions
- silhouette notes
- approved motion assets

重要原則: **コードでキャラクターを描き直さない。**

## 3. Sticker Set Definition

各スタンプは最低限次を持つ。

```json
{
  "id": "acknowledge_01",
  "text": "了解！",
  "communicationTag": "acknowledge",
  "emotion": "positive",
  "motion": "nod",
  "intensity": 0.7,
  "assetStatus": "planned"
}
```

`communicationTag` 初期候補:
- acknowledge
- thanks
- greeting
- apology
- positive
- encouragement
- surprise
- affection
- question
- waiting
- character

## 4. Strategy

初期Strategy `daily-balanced-v1`:
- daily/acknowledge/greeting/thanks/apology: 50%
- emotion/positive/encouragement/surprise: 25%
- character-specific: 25%

同一台詞、同一ポーズ、同一感情の過剰重複を避ける。

## 5. LINE Static Profile（2026-10-07確認時点）

通常スタンプ:
- 個数: 8 / 16 / 24 / 32 / 40
- スタンプ画像: 最大 370 × 320 px
- メイン画像: 240 × 240 px
- トークルームタブ画像: 96 × 74 px
- PNG
- RGB
- 画像ごと1MB以下
- 縦横は偶数px
- 72dpi以上
- 背景透過を基本とする

これらをソースコードへ直接埋め込まず `platforms/line-static.json` 相当のprofileへ分離する。

## 6. Animated Profile 将来対応

アニメーションスタンプ:
- 個数: 8 / 16 / 24
- 最大 320 × 270 px
- APNG
- main: 240 × 240 APNG
- tab: 96 × 74 PNG

静止画版と同じ Character Pack を利用し、Motion定義から派生できる構造にする。

## 7. 自動検品

### 機械検査
- ファイル存在
- PNG/APNG形式
- 寸法
- 偶数寸法
- RGB
- alpha/transparency
- 容量
- 必要個数
- 重複画像候補
- 極端に小さい描画領域
- main/tab生成済み
- メタデータ必須項目

### ヒューリスティック検査
- 台詞の用途重複
- 同一ポーズ過多
- 日常利用カテゴリ不足
- キャラクター固有要素不足
- 文字が小さすぎる可能性
- キャラの顔・輪郭・色の逸脱候補

### 人間確認必須
- キャラクター同一性
- 著作権/商標/肖像等の権利
- 台詞のニュアンス
- 公序良俗・文化的問題
- 最終商品品質
- 審査申請
- 公開

## 8. Asset Status

`planned` → `generated` → `validated` → `approved` → `packaged`

差戻し:
`rejected` / `needs_revision`

生成済みであっても人間承認前は正本扱いしない。

## 9. ディレクトリ案

```text
characters/
  <character-id>/
    character.json
    reference/
    motions/
    generated/
sets/
  <set-id>/
    set.json
    source/
    output/
platforms/
  line-static.json
  line-animated.json
schemas/
docs/
tools/
```

## 10. 非機能要件

- 再実行可能: 同じ入力から工程を再生成できる。
- 追跡可能: どのReference/Prompt/設定から生成したか記録する。
- 非破壊: 正本素材を自動処理で上書きしない。
- 差し替え可能: Canva等の外部サービスをadapterとして交換できる。
- 仕様更新可能: LINE側変更時にplatform profileを差し替えられる。
- 秘密情報分離: ログイン情報/APIキーをCharacter PackやGitへ保存しない。

## 11. 完成判定

1. うたたねちゃんで16個の静止画セットを生成できる。
2. validatorがLINE規格違反を検出できる。
3. 人間が一覧で最終確認できる。
4. 別キャラクターをCharacter Pack化する。
5. エンジン本体を変更せず2体目の16個セットを生成できる。

5まで通過してv1候補とする。
