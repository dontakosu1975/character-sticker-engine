# 自動化・公開フロー v0.1

## 基本方針

完全無人で販売公開すること自体を目的にしない。

**人間が創作上・権利上・公開上の責任を持つべき地点だけ止め、それ以外を自動化する。**

## Pipeline

```text
[1] Character Pack登録
        ↓
[2] 商品Strategy選択
        ↓
[3] 8/16/24...件の企画生成
        ↓
[4] 人間: 企画承認
        ↓
[5] 画像素材生成/制作
        ↓
[6] 自動画像処理
        ↓
[7] 自動validator
        ↓
[8] Character Consistency Review
        ↓
[9] main/tab/metadata/package生成
        ↓
[10] Creators Market下書き登録支援
        ↓
[11] 人間: 最終プレビュー・権利確認
        ↓
[12] 審査申請
        ↓
[13] 審査結果取得
        ↓
[14] 承認なら人間確認後リリース
     差戻しならrevision loop
```

## Human Gate

### Gate A — 企画承認
16個の台詞、用途、ポーズを一覧確認。不要な表現やキャラに合わない台詞をここで止める。

### Gate B — Character Approval
生成画像を一覧化し、顔・体格・色・輪郭・性格が正本から逸脱していないか確認。

### Gate C — Submission Approval
Creators Marketへ審査申請する直前。商品名、説明、販売地域、権利情報、画像を確認。

### Gate D — Release Approval
審査承認後、販売開始前の最終確認。

## Browser Automationの扱い

Creators Marketの画面操作はPublisher Adapterへ隔離する。

理由:
- UI変更で壊れやすい
- ログイン/二要素認証等が絡む
- bot対策の影響を受ける可能性がある
- 審査・販売開始は外部への確定操作

そのため、最初の実装目標は **アップロード可能な完成パッケージ + 入力用metadata + プレビュー** とする。

ブラウザ自動化を追加する場合も、以下を守る。
- CAPTCHA等を回避しない
- 認証情報をGitへ保存しない
- 申請/公開直前で停止可能にする
- UI selectorをエンジン本体へ混ぜない
- 操作ログを残す

## Revision Loop

審査差戻しを単なる失敗にせず、構造化して保存する。

```text
review-result
  ├ reason
  ├ affectedStickerIds
  ├ guidelineCategory
  ├ humanNote
  ├ revisionAction
  └ resolvedAt
```

将来的には蓄積した差戻し理由をpreflight validatorへ反映する。

## 自動化レベル

- Level 0: ドキュメント/手作業
- Level 1: 画像規格化・validator
- Level 2: 商品企画・metadata・package自動生成
- Level 3: Asset Provider連携
- Level 4: Creators Market下書き登録支援
- Level 5: Human Gate付きワンクリック出版

PoCはLevel 2を最初の完成点とする。
