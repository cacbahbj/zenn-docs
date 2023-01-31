---
title: "10分DDDまとめ"
emoji: "🐥"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["勉強会","DDD", "アジャイル", "スクラム"]
published: true
---

# 10分DDD

@little_hand_s さんのYouTubeチャンネルにあるこちらの再生リストと公開資料のリンク及び内容のメモです
　https://www.youtube.com/watch?v=HgtCKlOzRiQ&list=PLXMIJq1G-_66F9woQpidJfe4HHCFxdXaA

## 1. ドメインモデリング

https://www.youtube.com/watch?v=HgtCKlOzRiQ

https://little-hand-s.notion.site/10-f79853f8e1e54f429e14ad9cecc87f35

- DDDとは
- モデリングってどうやるの？
  - sudoモデリングとは
    - システム関連図 (s)
    - ユースケース図 (u)
    - ドメインモデル図 (d)
    - オブジェクト図 (o)

参考記事
https://little-hands.hatenablog.com/entry/2022/06/01/ddd-modeling

## 2. 設計のツボ 高凝集/低結合

https://www.youtube.com/watch?v=hX9kCwdR8dc

https://www.notion.so/10-d85b38b1846048cea37a015a52636d53

- どうしたら設計をよくできるのか
  - 原則、パターン等
  - 色々あるが、これ一つ抑えるだけで複数の利点を得られる
- 「高凝集/低結合」
  - クラスの責務を明確・単一に、モジュール菅野依存度を低く

良い設計のための参考書籍
https://www.amazon.co.jp/dp/4798046140
https://www.amazon.co.jp/dp/4048930591

その他参考資料
@[speakerdeck](87050fae114d4f60b66eebfc89e57a1e)
https://note.com/cyberz_cto/n/n26f535d6c575

## 3. ドメインモデルをコードに落とす方法

https://www.youtube.com/watch?v=Upeg6cNOirc

https://www.notion.so/b97c1a305aa24040a63a61b3cd863e55

- モデルをコードで表現するために重要なこと
  - こまめなフィードバックサイクルと改善
  - 保守性の高い実装パターンの使用
    - エンティティ、値オブジェクト、リポジトリ、、、
- コーディング時の重要方針
  - ドメインモデルの知識を対応するオブジェクトに書く
  - 常に正しいインスタンスしか存在させない

## 4. 集約って一体なんなんだ

https://www.youtube.com/watch?v=Hn4EAXYBl8c

https://www.notion.so/91dec09e1416416bb87594d79e06f592

- 集約とは？
  - リポジトリに入出力する範囲
  - 適切な範囲は実装しないとわからないのでモデリング時に決め切らない
- クエリモデル
  - 集約は更新処理の整合性確保に特化しているので、参照処理で課題がある場合はクエリモデルを検討する

参考記事
https://little-hands.hatenablog.com/entry/2021/03/08/aggregation
https://little-hands.hatenablog.com/entry/2019/12/02/cqrs

その他参考資料
https://qiita.com/mikesorae/items/ff8192fb9cf106262dbf

## 5. ドメイン駆動設計のアーキテクチャ(オニオンアーキテクチャ)

https://www.youtube.com/watch?v=80NeuPXs2J0

https://www.notion.so/8a666e49641248fa810ef382715cfe0f

- おすすめのアーキテクチャは？
  - オニオンアーキテクチャ
    - クリーンアーキテクチャなどと比べてシンプル

参考記事
https://little-hands.hatenablog.com/entry/2017/10/04/231743

こちらには比較対象となる以下4つについての記載があります
- レイヤードアーキテクチャ
- ヘキサゴナルアーキテクチャ
- オニオンアーキテクチャ
- クリーンアーキテクチャ

## 6. アジャイルとは何なのか DDDとはどうつながるのか

https://www.youtube.com/watch?v=XXLbkYndAJ4

https://www.notion.so/5456e287d09044ed999eff20714687fe

- アジャイルとはマインドセット（思想、考え方）である
  - 下記アジャイルマニュフェスト参照
- アジャイル開発の本質
アジャイルとは
  - 予測的ではなく、適応的である
  - プロセス思考ではなく、人思考である
- DDDもアジャイルの思想に沿った開発手法の一つ

参考記事
https://little-hands.hatenablog.com/entry/2022/06/27/essence-of-agile

アジャイルマニュフェスト
https://agilemanifesto.org/iso/ja/manifesto.html
IPA アジャイルソフトウェア開発宣言の読みとき方
https://www.ipa.go.jp/files/000065601.pdf

## 7. コードレビューで必ず気をつけること

https://www.youtube.com/watch?v=Xp9Wz4M2LyY

https://www.notion.so/96aaf637cc9a4139aee9fc3e69ee32e8

- 合言葉は「責務！テスト！」
- 責務
  - レイヤーの責務違反の実装がないか
  - クラスが高凝集/低結合になっているか
  - メソッドの責務を表現できているか
- テスト
  - ユニットテストを書きやすいか
    - テストが書きにくい場合は設計に問題がある可能性がある

## 8. ベロシティを使った中期計画どうやるの

https://www.youtube.com/watch?v=kt6zFawrmjg

※公開資料なし？

- スクラムだと中期（1ヶ月以上）の計画について明確に定義されていない
- 中期計画の立て方
  - 前提
    - SPの粒度がある程度安定
    - ベロシティがある程度安定
  - 計画の流れ
    - 中期開発のストーリーポイント(SP)を出す
    - ベロシティを出す
    - 合計SP * (100% + 統計的バッファ率) / ベロシティ = かかるプリント数と計算する
      - ~~合計SP / ベロシティ = かかるプリント数~~ とすると炎上する
  - 統計的バッファ率の考え方
    - 内訳を明示する（例
      - SP自然増（見積もり誤差）
      - 要件追加
      - 結合テスト
    - 内訳を明治することで納得できるし調整しやすくなる
    - 統計的に判断することが重要
      - 各SP増加内訳を記録して、次回に活かす

## 9. スクラム再入門

https://www.youtube.com/watch?v=-YcblVrRzGU

https://www.notion.so/c692f3b226c74240a296af0db46aae75

- スクラムの進め方の全体像
- スクラムの解決しようとする課題
  - スクラムはフレームワークであり、方法論ではない
- スクラムが基づく理論

スクラムガイド 2020/11
https://scrumguides.org/docs/scrumguide/v2020/2020-Scrum-Guide-Japanese.pdf

- スクラムとは
- スクラムにおける開発の進め方
- スクラムとはどういうものなのか
- スクラムの解決しようとする課題
- スクラムが基づく理論
- スクラムにおける開発の進め方
- スクラムを実践する上で大切なこと


# その他メモ

2023/02/09にこちらのイベントがある模様です
https://flexy.connpass.com/event/273071/
