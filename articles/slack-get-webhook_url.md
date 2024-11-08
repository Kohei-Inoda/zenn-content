---
title: "Slack Webhook URLの取得方法"
emoji: "🔗"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Slack","WebhookURL","application","tech"]
published: true
---
# 目的
* Slackのアプリ作成するにあたりWebhook URLが必要になった．

# SlackのWebhook URLの取得
以下の公式urlをもとに取得しましたが、英語なので簡単にステップを紹介します．
https://api.slack.com/messaging/webhooks

### 1. Slack APIの公式サイトから「Your apps」を選択
![](https://storage.googleapis.com/zenn-user-upload/e1e9bdff0712-20241108.png)

### 2. 「Create New App」を選択
![](https://storage.googleapis.com/zenn-user-upload/cecb2f1acc46-20241108.png)

### 3. 「From scratch」を選択
![](https://storage.googleapis.com/zenn-user-upload/61b4c913ac46-20241108.png)

### 4. ①に作成するアプリ名を入力、②にアプリを作成するワークスペースを選択
![](https://storage.googleapis.com/zenn-user-upload/134395562a77-20241108.png)

### 5. 入力後、「Create App」を選択すると以下の画面に遷移する
#### 「Incoming Webhooks」を選択
![](https://storage.googleapis.com/zenn-user-upload/93514f4cf792-20241108.png)

### 6. 「Activate Incoming Webhooks」をオンにする
![](https://storage.googleapis.com/zenn-user-upload/5bce681568dd-20241108.png)

### 7. すると、下の方に「Add New Webhook to Workspace」が出てくるので選択
![](https://storage.googleapis.com/zenn-user-upload/3b785dd62459-20241108.png)

### 8. 作成するアプリがアクセスする先のチャンネルを選択し、許可する
![](https://storage.googleapis.com/zenn-user-upload/00d41e39aca4-20241108.png)

### 9. すると、Webhook URLが取得できる
また、URLの上のコマンドをコピーし、ターミナルなどで実行すると、アプリのテストメッセージを送信することができる．
![](https://storage.googleapis.com/zenn-user-upload/f4f13b980d70-20241108.png)

# 結論
今回、自身の開発の中でWebhook URLが必要になったため取得した．
また、Slack関連のアプリを作る際に、送信先のアドレス取得のために必要になることが多くなるのでこれから作る人の参考になると嬉しいです．