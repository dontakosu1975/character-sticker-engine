# CURRENT TASK

Status: **PLANNING / DO NOT IMPLEMENT YET**
Updated: 2026-10-07

## 目的

マスコット版うたたねちゃん（PopMate）の次プロジェクトとして、LINEスタンプ版うたたねちゃんを最初の実証キャラクターにした **Character Sticker Engine** を構築する。

ただし最終目的は「うたたねちゃんのスタンプを作ること」ではない。

**別キャラクターの Character Pack を投入しても、エンジン本体の変更なし、または最小限の設定変更だけでスタンプ企画・素材処理・検品・公開準備まで再利用できること**を完成条件とする。

## 今はまだ実装しない

このリポジトリは現在、企画・仕様を固める段階。ユーザーから実装開始の明示指示が出るまでは、コード実装・Creators Market操作・外部公開操作を行わない。

## 実装開始時に最初に読むもの

1. `README.md`
2. `docs/PROJECT_PLAN.md`
3. `docs/LINE_RESEARCH.md`
4. `specs/ENGINE_SPEC.md`
5. `specs/AUTOMATION_FLOW.md`
6. `specs/character-pack.example.json`
7. `specs/sticker-set.example.json`
8. `examples/utatane/PLAN.md`
9. `ishibashi/IMPLEMENTATION_RULES.md`

## PoC①の予定範囲

実装開始後の最初のPoCは、Creators Marketへの自動登録ではなく、ローカルで完結する生成パイプラインを優先する。

入力：
- Character Pack
- Sticker Set定義
- 正本画像素材

出力：
- LINE通常スタンプ向け画像一式
- main画像
- tab画像
- metadata
- validation report
- preview/contact sheet
- 配布・登録用成果物ディレクトリ

最初の実証キャラクターは「うたたねちゃん」。

## PoC①でやらないもの

- Creators Marketへの自動ログイン・自動申請
- 審査申請の自動確定
- 自動リリース
- AIによるキャラクター造形の勝手な変更
- アニメーションスタンプの本実装
- 大規模GUI

## 完了条件

1. うたたねちゃん16個セットを同一パイプラインで生成・検品できる。
2. LINE仕様違反を機械的に検出できる。
3. 生成結果を人間が一画面または一覧画像で確認できる。
4. キャラクター固有値がエンジンコードへ混入していない。
5. 2体目のダミーCharacter Packを差し替えて、同じパイプラインが走ることを確認する。

## 次の指示待ち

ユーザーがマスコット版うたたねちゃんを一区切りさせ、LINEスタンプ版の着手を指示するまで待機。
