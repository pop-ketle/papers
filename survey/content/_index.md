---
title: "調べ物まとめ"
date: 2020-09-26T23:08:59+09:00
tags: ["top-page"] 
weight: 10
# draft: true
---

#### 本読んだり、論文読んだり、調べ物したものを適当にまとめます
2020/11/2 更新

使用テーマ[hugo-thme-learn](https://themes.gohugo.io/theme/hugo-theme-learn/en/)

---

~~Hugoを使ってサイトを作ってみたけど、Notion使ってページ公開したほうがよかったんじゃないかと早くも後悔しています。~~

現在のように、Hugoを使う場合は、マークダウンで記事書いて、画像入れたかったらstaticフォルダ下に画像を配置してパスを通してなど色々考えて、さらにデプロイまでしないといけないので書くためのハードルがかなり高くなります。

そのため、Notionを使ってそのページを公開する形にした方が、手軽に数式や図表を簡単に入れられたり、入れ子構造にページを構築できたりしてかなり便利なので、そちらに移行しようと思いました。(特に論文の図表をスクショしてドラックアンドドロップして貼り付ければオーケーなのはかなり嬉しい。)しばらくこのページは置いておきますが、そのうちNotionに移行して、ポートフォリオサイトの方にでもリンクを貼っておこうと思います。

---

# how to use

## make new site
```
hugo new site $SITENAME$
```

## make chapter
チャプターを作るには
```
hugo new --kind chapter <name>/_index.md
```
weightで左のリスト表示の位置を、pre = "<b>X. </b>"で表示する文字の調整。

## make new page
新しいページを作るには
```
hugo new <name>/<name>.md
```
tags: ["tag-name"]でタグをつけれます。

---

# how to deploy
1. プロジェクトフォルダへ移動  
例:
```
cd survey
```

2. localhostで起動&テスト
```
hugo server -D
```

4. publicを作成
```
hugo
```

5. デプロイ
```
../deploy.sh
```