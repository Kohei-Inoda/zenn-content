---
title: "Chrome拡張自作して自動でSlackに共有"
emoji: "📰"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["JavaScript","Chrome","chromeextension","chrome拡張", "tech"]
published: true
---
# 目的

- ウェブ上でSlackに共有したい技術ブログやニュースを見つけた際にコピーしてSlackに移動して貼る工程が面倒
- Chrome拡張機能を自作したことがないため、作ってみたかった

# 作成物の説明
今回実際に作成した拡張機能は一言でうと、現在のタブのURLをSlackに共有するものです．
①拡張機能を実行すると、下図のようなポップアップ画面が表示されます．
②ボタンを押すとあらかじめSlackアプリで取得するWebhook URL先のチャンネルに現在閲覧しているURLが共有されます．
また、メッセージボックスに入力することで文章も一緒に共有できます．
次に、実際の画面を紹介します．

# 実際の画面

![](https://storage.googleapis.com/zenn-user-upload/67550fc91f76-20241108.png)
![](https://storage.googleapis.com/zenn-user-upload/b5258e5d4e80-20241108.png)

# 実際のコード
https://github.com/Kohei-Inoda/chrome-extension-slack-share

# 技術選定
* JavaScript

# 事前準備

### 1. SlackのWebhook URLの取得
Webhook URLの取得方法については以下の記事で紹介しています！
取得方法を知らない方はぜひ見て取得してから本記事の続きを見てください．
https://zenn.dev/kohei0215/articles/slack-get-webhook_url

### 2. Chromeブラウザとエディタ
Chrome拡張を実装するために、Googleアカウントにログイン済みのChromeブラウザと、プログラム作成用のエディタを準備してください．

# 作り方
まずは、作り方を説明する前に今回作成した拡張機能のファイルディレクトリとそれぞれのファイルの簡単な説明を載せます．

```bash
.
├── manifest.json (作成するchrome拡張の設定全般ファイル)
├── background.js (実際に動作するスクリプト)
├── config.js     (今回はSlackのWebhook URLをここに宣言しました)
├── popup.html    (拡張時に表示される画面のhtml)
├── popup.js      (表示される画面の挙動を制御するスクリプト)
├── icons         (chrome拡張のアイコン画像ファイル)
    ├── icon128.png
    ├── icon16.png
    └── icon48.png

```
ここで、Chrome拡張を作る上で重要なファイルは、**manifest.json**と**background.js**の２つだけです．
### manifest.json
このファイルは言わば拡張機能の「説明書」のようなものです．拡張機能の設定や構成情報を定義しているファイルです．拡張機能の名前や、持つ権限、実際に動くスクリプトのファイルの指定をします．
実際に今回作成したmanifest.jsonはこちらです．(分かりやすいためにコメントをつけてますが、コピペする際はjsonでエラーが出るので注意してください)

**./manifest.json**
```json
{
    "manifest_version": 3,
    "name": "URLをSlackに送信",
    "version": "1.0",
    "description": "現在のタブのURLを特定のSlackチャンネルに送信します．",
    "permissions": ["activeTab", "scripting", "storage"],
    "host_permissions": ["https://hooks.slack.com/*"], //Slackへのアクセス権限を付与
    "background": {
      "service_worker": "background.js", //実際に動くJavaScriptファイルを指定
      "type": "module" //基本なくても大丈夫だが、今回なくてつまづいたのであとで説明します．

    },
    "action": {
      "default_popup": "popup.html",
      "default_icon": {
        "16": "icons/icon16.png",
        "48": "icons/icon48.png",
        "128": "icons/icon128.png"
      }
    },
    "icons": {
      "16": "icons/icon16.png",
      "48": "icons/icon48.png",
      "128": "icons/icon128.png"
    }
  }

```
### background.js
次に実際に動く動作をJavaScriptで書きます．下が実際のコードで、簡単な説明だけしときます．
1. chrome.runtime.sendMessageを受け取った際に処理開始(今回はpopup.jsから受け取る) 
2. fetch関数で、受け取ったURLとメッセージをWebhook URLにPOSTリクエストを送信し、メッセージを送信
3. popup.jsに処理結果をレスポンス

**./background.js**
```javascript
import config from './config.js';
//Chrome拡張機能が呼び出された際に動く．
chrome.runtime.onMessage.addListener(async (request, sender, sendResponse) => {
    const webhookUrl = config.Slack_webhookUrl; //config.jsからWebhook URLを読み込む
    const payload = {
      text: `${request.message || ''}\n${request.url}`
    };
  
    try {
      const response = await fetch(webhookUrl, {
        method: "POST",
        headers: {
          "Content-Type": "application/json; charset=utf-8"
        },
        body: JSON.stringify(payload)
      });
  
      if (response.ok) {
        console.log("Slackにメッセージを送信しました！");
        sendResponse({ success: true });
      } else {
        console.error("Slackへのメッセージ送信に失敗しました:", response.statusText);
        sendResponse({ success: false });
      }
    } catch (error) {
      console.error("Slackへのメッセージ送信エラー:", error);
      sendResponse({ success: false });
    }
  
    return true;  // 非同期のsendResponseをサポートするため
  });
```

### popup.htmlとpopup.js
あとは、拡張機能の画面を実装するだけです．下が実際のコードです
**./popup.html**
今回はとりあえずChrome拡張機能の実装がメインなので、無機質なデザインですが、カッコよくしたいなど好みに合わせてcss追加してもいいと思います
```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <title>Slackに送信</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 10px; }
    #sendButton {
      padding: 8px 16px;
      font-size: 16px;
      cursor: pointer;
      position: relative;
    }

  </style>
</head>
<body>
  <h3>SlackにURLを送信</h3>  <!--見出し-->
  <textarea id="message" placeholder="オプションのメッセージ"></textarea>  <!--ユーザのテキスト入力エリア-->
  <button id="sendButton">Slackに送信</button><!--メッセージ送信ボタン-->
  <script src="popup.js"></script><!--popup.jsを読み込む-->
</body>
</html>
```

**./popup.js**
何気にbackground.jsと同じくらい重要な役割をしてるのがpopup.jsです．
popup.htmlからの送信ボタンによって、メッセージと現在のタブを取得し、background.jsに送信します．
また、送信できたか確認するために、成功のレスポンスを受け取ると、ボタンの表示を「送信完了」に変更するように実装しました．
```javascript
document.getElementById("sendButton").addEventListener("click", async () => {
    const sendButton = document.getElementById("sendButton");
    const [tab] = await chrome.tabs.query({ active: true, currentWindow: true });//現在アクティブなタブの取得
    const message = document.getElementById("message").value;//ユーザ入力のテキスト内容を取得
    const url = tab.url;//タブのurlを取得
  
    // 送信ボタンをクリック時に無効化して送信中の状態に
    sendButton.disabled = true;
    sendButton.innerText = "送信中...";
  
    try {
      // メッセージとURLをbackground.jsに送信
      chrome.runtime.sendMessage({ url, message }, (response) => {
        // Slackへの送信が完了したら「送信完了」に変更
        sendButton.innerText = "送信完了";
      });
    } catch (error) {
      console.error("メッセージ送信エラー:", error);
      sendButton.innerText = "送信エラー"; // エラー時のテキスト変更
    } finally {
      // 一定時間後に元の「Slackに送信」に戻す
      setTimeout(() => {
        sendButton.innerText = "Slackに送信";
        sendButton.disabled = false;
      }, 2000);
    }
  });
```
これでchrome拡張機能のプログラムは完成したので、次は実際にChromeブラウザの方で登録します．
### Chromeブラウザに拡張機能を登録
1. まずはChrome拡張機能の管理画面に進み、右上のデベロッパーモードをオンにします．
2. そして、「パッケージ化されていない拡張機能を読み込む」を選択し、作成したプログラムのフォルダを選択します

![](https://storage.googleapis.com/zenn-user-upload/31edc17d97a8-20241110.png)

3. すると、下の画像のように拡張機能が追加されてるので有効にすることで、使うことができます．
![](https://storage.googleapis.com/zenn-user-upload/4b0a3078fabd-20241110.png)

以上が、Chrome拡張機能の作り方と、今回実際に作成したSlackにURLを自動で送信する拡張機能の実装でした．

# つまづいた点
今回、拡張機能を作成している中で、SlackのWebhook URLを外部から見れなくするために、config.jsに宣言し、background.jsにimportする処理を行いました．
#### 問題
すると、Chromeブラウザで拡張機能追加時に以下のエラーが出ました．
```
Uncaught SyntaxError: Cannot use import statement outside a module
```
#### 原因
これは、Chrome拡張機能の標準設定でimport文を使用することができないことによるものです．
import文はJavaScriptのモジュールシステム(ESモジュール)で、ファイル間でコードを再利用する目的で作られたもので、これがChromeの標準設定では使えないようになっているのが原因でした．

#### 解決方法
manifest.jsonにおいて、動作するスクリプトを**モジュール形式**として設定します．具体的にはmanifest.jsonに以下のコードを追加します．
```json
{
    "manifest_version": 3,
    .
    .
    .
    "background": {
      "service_worker": "background.js", //実際に動くJavaScriptファイルを指定
      "type": "module" //←これを記述

    },
  }
```
type: "module"を指定することで、background.jsがESモジュールとして認識されて、import文を使用できるようになります．
*また、manifestの**バージョン2ではこの設定ができない**ので、ESモジュールを使う際は**バージョン3が必要**です．

# まとめ
今回初めて、Chromeの拡張機能を作成してみました．
拡張機能独特のmanifest.jsonの作成など初めてのこともありましたが、URLをSlackに共有する程度の機能は比較的簡単に作成できたと思います．
今後も身の回りの作業を便利にするツールを自作できるように精進していきたいです．

また、今回初めてしっかり記事を書いてみました．
長くなってしまいましたが、今後の執筆のため見にくい点や改善箇所ありましたら指摘いただけると嬉しいです．