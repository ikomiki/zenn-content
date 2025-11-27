---
title: "GrandingDINO(オープンボキャブラリー物体検出モデル)の"
emoji: "🐙"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Python", "機械学習", "GrandingDINO"]
published: false
---

## はじめに

<!-- cSpell:ignore beautiful  -->

[GroundingDINO](https://github.com/IDEA-Research/GroundingDINO)モデルを使用した物体検出 streamlit アプリケーションを実装したうえで、得られた知見を共有します。

コードについての説明は行いません（AI 生成なので、説明できるところがないとも）。

## リポジトリ

- [ikomiki/hello-GrandingDINO](https://github.com/ikomiki/hello-GrandingDINO)

## GrandingDINO の物体検出について

### soba(蕎麦)は検出できるが、薬味のネギはほぼ検出できない。ただし food なら蕎麦も薬味も検出できている

**元の画像** 自前で撮影
![元の画像](/images/owl-vit-streamlit/soba-source.png)

**food で検索** スコア（ネギが 0.555、蕎麦が 0.675）。

![alt text](/images/grandingdino-streamlit/image-4.png)

**soba**で検索（スコア：0.647）

![alt text](/images/grandingdino-streamlit/image-5.png)

なお、**onion**は閾値を下げないと検出されず、**long onion**だとネギより蕎麦のほうがスコアが高く検出される。**green onions**、**condiment**(薬味)でも同様。
薬味のネギはほぼ学習されていない様子。

### テキストプロンプトに「a 〜」などの接頭語を付けなくても検索される

むしろ「a 〜」接頭語をつけるとスコアが下がる。OWL-ViT とは

**元の画像** [著作者：freepik](https://jp.freepik.com/free-photo/beautiful-pet-portrait-small-dog-cat_21249173.htm)
![alt text](/images/owl-vit-streamlit/dogandcat-source.png)

**dog**で検索 左の猫 0.534、右の犬: 0.870
![alt text](/images/grandingdino-streamlit/image-1.png)

**a dog**で検索 左の猫 0.311、右の犬: 0.637
![alt text](/images/grandingdino-streamlit/image.png)

## OWL-ViT に比べて、dog と cat の区別がつく

**dog, cat**で検索 左の猫（cat） 0.624、右の犬（dog）0.788
![alt text](/images/grandingdino-streamlit/image-2.png)

なお「`a dog, a cat`」の場合はよくない結果になる模様。

![alt text](/images/grandingdino-streamlit/image-3.png)

## 謝辞

サンプルコードについては[Google Antigravity](https://antigravity.google/)と [Google Gemini](https://gemini.google.com/app?hl=ja)を使用して実装しています。
