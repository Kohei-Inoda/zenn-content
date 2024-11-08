---
title: "Chrome拡張自作して自動でSlackに共有"
emoji: "🔗"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: []
published: false
---
# 目的

- ウェブ上でSlackに共有したい技術ブログやニュースを見つけた際にコピーしてSlackに移動して貼る工程が面倒
- Chrome拡張機能を自作したことがないため、作ってみたかった

# 実際の画面
![](https://storage.googleapis.com/zenn-user-upload/67550fc91f76-20241108.png)
![](https://storage.googleapis.com/zenn-user-upload/b5258e5d4e80-20241108.png)

# 実際のコード
https://github.com/Kohei-Inoda/chrome-extension-slack-share

# 技術選定
* JavaScript

# 事前準備

### SlackのWebhook URLの取得
以下の公式urlをもとに取得しましたが、英語なので簡単にステップを紹介します。
https://api.slack.com/messaging/webhooks

1. Slack APIの公式サイトから「Your apps」を選択