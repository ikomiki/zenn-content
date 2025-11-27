---
title: "OWL-ViT(オープンボキャブラリー物体検出モデル)のプロンプトの癖"
emoji: "📷"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Python", "機械学習", "OWLViT"]
published: false
---

## はじめに

<!-- cSpell:ignore beautiful  -->

[OWL-ViT](https://huggingface.co/docs/transformers/model_doc/owlvit)モデルを使用した物体検出 streamlit アプリケーションを実装したうえで、得られた知見を共有します。

コードについての説明は行いません（AI 生成なので、説明できるところがないとも）。

## リポジトリ

- [ikomiki/owl-vit-streamlit: owl-vit で画像認識を行うサンプルコード。streamlit で実装](https://github.com/ikomiki/owl-vit-streamlit)

## OWL-ViT の物体検出について

### テキストプロンプトは「a 〜」などの接頭語を付けないとまず検索されない

例えば、`dog`では検出されないが、`a dog`では検出される。
OWL-ViT の学習データの癖のようです。

### テキストによっては具体的な名詞よりも一般的な名詞のほうがスコアが高いことがある

とくに日本食などで、`a onion`や`a soba`ではスコアが低く、`a food`で検索した場合に最もスコアが高い。

**元の画像** 自前で撮影
![元の画像](/images/owl-vit-streamlit/soba-source.png)

**`a food`で検索（スコア:ネギが 0.52，そばが 0.36）**
![`a food`で検索](/images/owl-vit-streamlit/soba-food.png)

**`a onion`(ネギ)で検索（スコア:0.05〜0.11）** ※ `a long onion`(長ネギ) だと 0.05〜0.09 に下がる
![`a soba`で検索](/images/owl-vit-streamlit/soba-onion.png)

**`a soba`で検索（スコア:そばが 0.10、ざるを含めた矩形が 0.13）**
![`a soba`で検索](/images/owl-vit-streamlit/soba-soba.png)

### 閾値を工夫しても、誤検出が起こりうる

例えば上記の`a soba`での検索時、蕎麦よりも、**ざるを含めた**蕎麦のほうがスコアが高い。
この場合、閾値をどういじっても蕎麦のみを取り出すことができない。

また、犬と猫なども取り違えが起きやすい。

**元の画像** [著作者：freepik](https://jp.freepik.com/free-photo/beautiful-pet-portrait-small-dog-cat_21249173.htm)
![alt text](/images/owl-vit-streamlit/dogandcat-source.png)

**`a cat`で検索** 左の猫が 0.70、右の犬が 0.43
![alt text](/images/owl-vit-streamlit/dogandcat-cat.png)

**`a dog`で検索** 右の犬が 0.30
![alt text](/images/owl-vit-streamlit/dogandcat-dog.png)

**`a dog, a cat`で検索**　どうやっても犬が`a cat`で検索されてしまう
![alt text](/images/owl-vit-streamlit/dogandcat-dog-cat.png)

## 謝辞

サンプルコードについては[Google Antigravity](https://antigravity.google/)と [Google Gemini](https://gemini.google.com/app?hl=ja)を使用して実装しています。
