---
title: "調べ物まとめ"
date: 2020-09-26T23:08:59+09:00
tags: ["top-page"] 
weight: 10
# draft: true
---

#### 本読んだり、論文読んだり、調べ物したものを適当にまとめます
2020/10/20 更新

使用テーマ[hugo-thme-learn](https://themes.gohugo.io/theme/hugo-theme-learn/en/)

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