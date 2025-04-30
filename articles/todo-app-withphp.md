---
title: "PHPでToDoアプリを作ってみよう！！"
emoji: "☑︎"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["PHP","ToDo"]
published: true
---
## はじめに

この教材では、Webシステム開発の基礎から始まり、PHPの基本文法やデータベース連携を学び、最終的にMVCアーキテクチャを使ったToDoアプリを作成できることをゴールとします。

---

## 0. Webシステムでできること(具体例)

### ECサイト（ネットショップ）

Amazonなどのように、商品をWeb上で売買できる仕組みです。商品の検索、カート、購入履歴など、たくさんの便利な機能がWebシステムで作れます。

### オークション・フリマサイト

ユーザーが出品し、他のユーザーが購入や落札できるサイトです。身近な例としてメルカリなどがあります。

### SNS（ソーシャルネットワーキングサービス）

X（旧Twitter）やInstagramなど、自分の投稿や他人の情報をリアルタイムで見たり、やり取りができるWebサービスです。

📌 **演習問題**

- 自分が普段使っているWebサービスを1つ選び、どのような機能がWebシステムで実現されているかを考えてみよう

---

## 1. WEBシステムの技術の基礎を学ぶ

### クライアント・サーバーモデルとは？

Webシステムは基本的に「クライアント（ユーザー）」と「サーバー（サービス提供側）」のやり取りで成り立っています。ユーザーがブラウザから情報を要求すると、そのリクエストがWebサーバーに届き、適切なレスポンスが返されます。

### HTTPリクエストとレスポンスの仕組み

- クライアントがWebページを要求 → HTTPリクエスト
- サーバーがHTMLを返す → HTTPレスポンス

### 基本的な流れ

![image.png](attachment:4c2e705b-b9ab-4d3c-a503-1bd29f17c785:image.png)

1. ユーザーがWebページを見たいと思い、ブラウザでURLを入力して開く
    
    <aside>
    💡
    
    - 例： https://example.com/index.php
    </aside>
    
2. ブラウザはURLに基づいてHTTPリクエストを作成し、Webサーバーに送信する
    
    <aside>
    💡
    
    - 例： HTTPリクエスト → GET /index.php
    </aside>
    
3. サーバーは受け取ったHTMLをもとに、ページを画面に表示します(HTTPレスポンス)
    
    ```html
    HTTP/1.1 200 OK
    Content-Type: text/html; charset=UTF-8
    Content-Length: 137
    
    <!DOCTYPE html>
    <html>
      <head>
        <title>Example Page</title>
      </head>
      <body>
        <h1>ようこそ！</h1>
        <p>これはサンプルのページです。</p>
      </body>
    </html>
    ```
    
4. ブラウザは受け取ったHTMLをもとに、ページを画面に表示します
    
    ![](https://storage.googleapis.com/zenn-user-upload/7a3ab1072d2d-20250430.png)
    

📌 **演習問題**

- クライアントとサーバーの役割を一文で説明してみよう
- GETとPOSTの違いをまとめよう

---

## 2. WEBの基礎知識

### HTML・CSS・JavaScriptの役割

- **HTML** は、Webページの「中身と構造」を作ります。
    
    例：見出し、文章、画像、リンクなどを配置。
    
- **CSS** は、そのページの「見た目やデザイン」を整えます。
    
    例：文字の色・サイズ・余白・背景など。
    
- **JavaScript** は、ページに「動きや反応」をつけます。
    
    例：クリックでメッセージが変わる、メニューが開く、フォームをチェックするなど。
    

📌 **例：**

```html
<h1>こんにちは</h1>
<p style="color:red">これは赤い文字です</p>

```

- `<h1>` は見出し（HTML）
- `style="color: red;"` は文字を赤くするCSS

### 🌐 Webブラウザがページを表示するしくみ

1. **HTMLを読み込む**
    
    → ページの「構造」を理解（見出し・段落など）
    
2. **DOMツリーに変換**
    
    → Webページの骨組みをツリー状に整理する
    
3. **CSSやJavaScriptを適用**
    
    → デザインや動きを反映
    
4. **画面に表示（レンダリング）**
    
    → ユーザーが見られる形に完成
    

📌 **チェックリスト**

- HTMLの基本タグ（`h1`, `p`, `a`, `img`など）を使ったことがある
- CSSで色や文字サイズを変えたことがある
- JavaScriptでボタンを押したときに動く仕組みを試したことがある

---

## 3. PHPの開発環境を準備しよう（Windows編）

### ① MAMPをダウンロードする

1. 以下のリンクから公式サイトを開きます
    
    👉 https://www.mamp.info/en/windows/
    
2. **「Download」ボタン**をクリックしてダウンロードを開始します

![](https://storage.googleapis.com/zenn-user-upload/e6c05df30551-20250430.png)

### ② インストーラーを実行しよう

1. ダウンロードしたインストーラーを開きます。
2. **「MAMP PRO」,「Apple Bonjour」は使わない**ので、チェックを外して「Next」を押します

![](https://storage.googleapis.com/zenn-user-upload/c249191002f7-20250430.png)

3.ライセンスに同意する画面が出たら、一番下までスクロールして

 「I accept the agreement」を選んで「Next」

### ③ インストールの設定はそのままでOK

1. インストール先は**そのままでOK**

![](https://storage.googleapis.com/zenn-user-upload/6d0d3f6fdf8f-20250430.png)
1. 他の設定もそのままで進めてOK

![](https://storage.googleapis.com/zenn-user-upload/c4ee8d1c28ea-20250430.png)
1. デスクトップアイコンの作成はどちらでもよい
    
![](https://storage.googleapis.com/zenn-user-upload/127e7d3a2b63-20250430.png)    
2. 最後に「Install」ボタンを押してインストールを開始します
    
![](https://storage.googleapis.com/zenn-user-upload/2175e702908f-20250430.png)    
3. 終了したら「Finish」をクリックします

    
![](https://storage.googleapis.com/zenn-user-upload/816f71fa4b55-20250430.png)    

### ④ MAMPを起動して初期設定

1. Windowsキーを押して「MAMP」と検索 → MAMPアプリを開きます

![](https://storage.googleapis.com/zenn-user-upload/f1909e079255-20250430.png)
1. アプリを開いたら、**MAMPタブ →「Preferences」**を選択
2. 「Ports」タブを開いて、**「Set MAMP default」ボタン**を押します

    
![](https://storage.googleapis.com/zenn-user-upload/cc5cf2c69447-20250430.png)    
3. 他の設定も以下のようになっているのか確認しておく(すべてデフォルト設定でOK）

![](https://storage.googleapis.com/zenn-user-upload/a3ab0c748dfe-20250430.png)
![](https://storage.googleapis.com/zenn-user-upload/ffb07a1b840e-20250430.png)
![](https://storage.googleapis.com/zenn-user-upload/f50798b7c7d7-20250430.png)

### ⑤ サーバーを起動しよう！

1. 「Start Servers」ボタンを押してサーバーを起動します
    - ApacheとMySQLが**緑色のランプ**で表示されていればOK

![](https://storage.googleapis.com/zenn-user-upload/0f6b4f77bb18-20250430.png)
### ⑥ PHPファイルを配置して動かしてみよう

1. MAMPがインストールされたフォルダの中にある
    
    `htdocs` フォルダにPHPファイルを入れます
    
2. ブラウザで以下のようにアクセスすれば、PHPが動作しているか確認できます：
    
    `http://localhost/ファイル名.php`
    
    でアクセス
    
    ---
    

## 4. PHPの基本的な文法

PHPは、サーバー側で動く**プログラミング言語**です。

HTMLだけではできない「計算」や「条件分岐」「繰り返し」などを実行できます。

**PHPの公式マニュアルは以下にあります：**

https://www.php.net/manual/ja/index.php

### 実行の前に

PHPコードを動かすには、**PHPが動作する環境（例：XAMPPやMAMPなど）**が必要です。以下のコードを `.php` ファイルとして保存し、ブラウザで開くことで、実際にどのような結果が表示されるか確認できます。

### はじめてのPHP（Hello World）

PHPファイルは `.php` という拡張子で保存し、PHPでプログラミングする場合、以下のように`「<?PHP」`と`「?>」`で囲む必要があります。

```php
<?php
echo 'こんにちは、PHP！';
?>
```

### 変数と演算

変数は「情報を入れておく箱」です。`$`マークを使って書きます。

```php
<?php
$name = 'Epsilon';  // 文字列を代入
echo "こんにちは、$name";
?>
```

### 条件分岐（if文）

「もし〜だったら○○をする」といった判断をするときに使います。

```php
<?php
$score = 85;

if ($score >= 80) {
  echo '合格です';
} else {
  echo '不合格です';
}
?>
```

### 繰り返し（for文）

同じ処理を何回も繰り返したいときに使います。

```php
<?php
for ($i = 0; $i < 5; $i++) {
  echo $i;
}
?>
```

### 配列（Indexed Array）

配列とは、**複数の値をまとめて管理できる変数**のようなものです。番号（インデックス）で要素を管理します。

```php
php
コピーする編集する
<?php
$fruits = ['りんご', 'バナナ', 'ぶどう'];

echo $fruits[0];  // りんご
echo $fruits[1];  // バナナ
echo $fruits[2];  // ぶどう
?>

```

### ✅ 解説

- `$fruits[0]` のように、**0から始まる番号**で値にアクセスします。
- 配列の中身をすべて表示したいときは、**繰り返し（for / foreach）**を使います。

```php
php
コピーする編集する
<?php
foreach ($fruits as $fruit) {
  echo $fruit . '<br>';
}
?>

```

### 連想配列（Associative Array）

連想配列は、**番号ではなく名前（キー）で値を管理する配列**です。

```php
php
コピーする編集する
<?php
$user = [
  'name' => 'Epsilon',
  'age' => 21,
  'job' => 'engineer'
];

echo $user['name'];  // Epsilon
echo $user['age'];   // 21
echo $user['job'];   // engineer
?>

```

### ✅ 解説

- `'キー' => 値` の形式で定義します。
- `$user['name']` のように、**キーの名前でアクセス**します。
- こちらも `foreach` でまとめて取り出せます：

```php
php
コピーする編集する
<?php
foreach ($user as $key => $value) {
  echo $key . ': ' . $value . '<br>';
}
?>

```

---

📌 **演習問題**

- 変数`$age`が18以上なら「成人」、それ以外なら「未成年」と表示するコードを書いてみよう
- 配列 `$colors = ['赤', '青', '緑']` を作成し、`foreach` を使ってすべて表示するコードを書いてみよう。
- 連想配列 `$book = ['title' => 'PHP入門', 'author' => '山田太郎']` を作って、`タイトル: PHP入門` のように表示するコードを書いてみよう。

---

## 5. 正規表現の使い方

### 正規表現とは？

**正規表現（せいきひょうげん）は、文字列のルールやパターン**を使って、

特定の形式に合っているかどうかを調べたり、文字を探したりする方法です。

たとえば：

- 「メールアドレスの形式になっているかチェックしたい」
- 「電話番号や郵便番号を確認したい」
- 「特定の文字列だけを取り出したい」

というときに使います。

例：メール形式チェック

```php
<?php
$email = 'test@example.com';

// preg_match() は、文字列が正規表現にマッチするかを調べる関数です
if (preg_match('/^[\w.-]+@[\w.-]+\.\w+$/', $email)) {
    echo '有効なメールアドレス';
} else {
    echo '無効なメールアドレス';
}
?>
```

### ここで使っている正規表現の意味

| 記号 | 意味 |
| --- | --- |
| `^` | 文字列の先頭 |
| `[\w.-]+` | 英数字・アンダースコア・ピリオド・ハイフンを1文字以上 |
| `@` | 「@」記号そのもの |
| `\.` | 「.」ピリオド（ドット） |
| `\w+` | 英数字を1文字以上 |
| `$` | 文字列の末尾 |

`preg_match()` は「一致すれば `1` を返す」、一致しなければ `0` を返します。

📌 **演習問題**

- 郵便番号（例: 123-4567）を判定する正規表現を試してみよう

---

## 6. PHPの名前空間、クラス

### クラスとは？

クラスは、**変数（プロパティ）**や**関数（メソッド）**をまとめた「設計図」のようなものです。

このクラスから実際に作られたものを**オブジェクト（インスタンス）**と呼びます。

### クラスを使う理由

プログラム内で**同じような処理や構造を何度も繰り返すのは面倒**です。

クラスを使うことで、**一度だけ設計図を作っておけば、何回でも呼び出して使える**ようになります。

### クラスとオブジェクト

```php
class Task {
    public $title;

    public function __construct($title) {
        $this->title = $title;
    }

    public function show() {
        echo $this->title;
    }
}
$task = new Task("掃除をする");
$task->show();

```

### ✅ コードのポイント解説

- `class Task`：タスクを表すクラスの定義です。
- `$title`：タスクのタイトルを保持する**プロパティ（変数）**。
- `__construct()`：オブジェクトが作られた時に自動で呼び出される**コンストラクタ**。
- `$this->title = $title;`：外部から受け取った値をクラス内の変数にセットします。
- `show()`：タスクのタイトルを画面に出力する**メソッド（関数）**。
- `new Task("掃除をする")`：クラスからインスタンス（オブジェクト）を生成しています。

### 名前空間の使い方（大規模開発で便利

名前空間（namespace）は、**クラス名や関数名の重複を防ぐための仕組み**です。特に複数のファイルやライブラリを使う大規模開発では必須の概念です。
な

### 名前空間

```php
<?php
namespace App\Models;

class Task {
    // クラスの中身
}
?>
```

### ✅ 説明

- `namespace App\Models;`
    
    → このクラスは「App\Models」という**名前空間の中に属している**と宣言しています。
    
- 別ファイルでこのクラスを使うときは、以下のように完全修飾名（フルパス)で指定します：

```php
$task = new \App\Models\Task("掃除をする");
```

または`use` キーワードで簡略化も可能です。

```php
use App\Models\Task;

$task = new Task("掃除をする");
```

📌 **演習問題**

- Taskクラスに`isDone`プロパティを追加し、完了かどうかを判定するメソッドを追加してみよう

---

## 7. データベースの設計手法

Webアプリや業務システムでは、多くの情報(ユーザー、商品、投稿など)を**効率的に保存・検索・管理**する必要があります。

そのために使われるのがデータベース(Database)です。

### データベースとは？

データベース(DB)とは、**大量のデータを整理して保存・操作するためのシステム**です。

特に多く使われるのが **リレーショナルデータベース（RDB：Relational Database）** です。

RDBでは、**データを表（テーブル）の形式で管理**します。エクセルのようなイメージで、1行が1件のデータ、1列が項目（カラム）です。

### RDBとテーブル設計

RDBを使うには、まず「どんな情報をどんな形で保存するか」を決める**テーブル設計**が必要です。

以下は、タスクを管理する `tasks` テーブルの例です：

| カラム名 | 型 | 説明 |
| --- | --- | --- |
| id | INT | タスクを識別するための番号（主キー） |
| title | VARCHAR | タスクの内容（文字列） |
| is_done | BOOLEAN | タスクが完了しているかどうか（true/false） |
| created_at | DATETIME | 作成日時 |

### ✅ 用語解説

- **カラム名（列名）**：保存する項目の名前
- **型（データ型）**：保存する値の種類（数値・文字列・日付など）
- **主キー（PRIMARY KEY）**：データを一意に識別するカラム（通常は `id`）

📌 **チェックリスト**

- テーブルにどんな情報が必要か洗い出せる
- 主キー・外部キーの意味を理解している

---

## 8. SQL操作方法

Webアプリでデータベースを使うには、**SQL（Structured Query Language）**という言語で操作します。ここでは、基本的なSQL文と、それをPHPから実行する方法（PDO）**を紹介します。

**PHPでのSQL操作リファレンスは以下にあります：**

https://www.php.net/manual/ja/book.pdo.php

### 基本SQL

### データをすべて取得（SELECT）

```sql
SELECT * FROM tasks;
```

- `SELECT`：データを取り出す
- ：すべてのカラム（列）を意味します
- `FROM tasks`：`tasks` テーブルから取得する

### データを追加（INSERT）

```sql

INSERT INTO tasks (title) VALUES ('買い物');
```

- `INSERT INTO`：データを追加する命令
- `(title)`：追加するカラム（列）を指定
- `VALUES ('買い物')`：追加する値を指定

### PHPでの実行（PDO）

PHPでは、**PDO（PHP Data Objects）**を使って、SQLを安全に実行することができます。

### ✅ INSERT文のPHPコード例

```php

<?php
$pdo = new PDO('mysql:host=localhost;dbname=todo', 'root', '');

// SQLを準備（:title はプレースホルダ）
$stmt = $pdo->prepare("INSERT INTO tasks (title) VALUES (:title)");

// プレースホルダに値を渡して実行
$stmt->execute([':title' => '勉強する']);
?>

```

### ✅ コード解説

| 部分 | 意味 |
| --- | --- |
| `new PDO(...)` | データベースに接続します（MySQLの場合） |
| `prepare()` | SQL文を準備（セキュリティ上、安全な実行方法） |
| `:title` | プレースホルダ。あとで値を渡す場所を指定 |
| `execute([...])` | 実際の値を渡してSQLを実行 |

📌 **演習問題**

- `DELETE FROM tasks WHERE id = 3;` をPHPで書いてみよう

---

## 9. サーバーとブラウザのやり取り

Webでは、**ブラウザ（クライアント）とサーバーが「リクエストとレスポンス」を通じて通信**

します。ユーザーがフォームに入力したデータも、こうした通信を通してPHPに渡されます。

### フォームと`GET`と`POST`の違い

### `GET`方式（URLにデータが表示される）

```html

<form method="get" action="submit.php">
  <input type="text" name="task">
  <input type="submit">
</form>
```

- データはURLに含まれて送信されます（例：`submit.php?task=買い物`）
- **検索やブックマーク可能な内容に向いている**
- データがURLに見えるので、**パスワードや個人情報の送信には不向き**

---

### `POST`方式（データは非表示で送信）

```html
<form method="post" action="submit.php">
  <input type="text" name="task">
  <input type="submit">
</form>
```

- デーはリクエストの本文（bodyに含まれて送られます
- URLには表示されません
- **ログイン・投稿・予約フォームなどに適している**

### PHP側での受け取り方の違い

```php

// GETで受け取る場合
$task = $_GET['task'] ?? '';

// POSTで受け取る場合
$task = $_POST['task'] ?? '';
```

💡 `$_REQUEST` を使うとどちらでも受け取れますが、**使い分けが曖昧になるため非推奨**です。

### ✅ 安全に表示するには

```php

echo htmlspecialchars($_REQUEST['task'], ENT_QUOTES, 'UTF-8');
```

- ユーザー入力をそのまま表示すると、**悪意あるスクリプト（XSS）を実行される可能性**があります。
- `htmlspecialchars()` を使って、HTMLの特殊文字（例： `<`, `>`, `"`）を無効化することが重要です。

📌 **演習問題**

- フォームから送られた値を`submit.php`で受け取り表示するコードを作成してみよう
- `task` という名前のフォームからPOSTで値を受け取り、`submit.php`でそのまま表示してみよう。
- `htmlspecialchars()` を使って表示内容を安全に保つようにしてみよう。

---

## 10. セキュリティーホールの理解

Webアプリでは、ユーザーの入力を信じすぎると大変危険です。

とくに注意すべき代表的な攻撃が **SQLインジェクション** と **XSS（クロスサイトスクリプティング）** です。

### SQLインジェクションとは？

SQLインジェクションとは、**入力フォームにSQLの命令を紛れ込ませて、意図しないデータベース操作をさせる攻撃**です。

### ❌ NG例（危険な書き方）

```php

$pdo->query("SELECT * FROM tasks WHERE id = $_GET[id]")
```

- ユーザーが `?id=1 OR 1=1` などと書くと、すべてのレコードが取得されてしまいます
- 最悪の場合、データベースの破壊や漏洩にもつながります

### ✅ OK例（安全な書き方：プリペアドステートメント）

```php

$stmt = $pdo->prepare("SELECT * FROM tasks WHERE id = :id");
$stmt->execute([':id' => $_GET['id']]);
```

- SQL文の構造と値を**分離**して処理するため、安全です
- 値が自動的にエスケープされ、不正な命令に変換されません

📌 **チェックリスト**

- `htmlspecialchars()` を使ってXSS対策
- プリペアドステートメントを使う

---

## 11. フォームのバリデーションチェック

バリデーション（validation）とは、**ユーザーの入力内容が正しいかどうかをチェックする処理**

です。これを行うことで、**不正なデータの保存や処理エラー、セキュリティリスクを防ぐ**ことができます。

### バリデーションの基本チェック項目

| チェック項目 | 目的 |
| --- | --- |
| 空欄チェック | 必須項目が入力されているか |
| 文字数制限 | 長すぎる入力を制限する |
| 形式チェック | メールアドレスや数値などのフォーマットを確認 |
| 値の範囲 | 数値などの上限・下限を設定する |
| 重複チェック | 同じタイトルなどが登録済みでないか確認（DB連携） |

### バリデーション例

```php
$title = trim($_POST['title'] ?? '');

// 空欄チェック
if (empty($title)) {
    echo 'タイトルは必須です';
}

// 文字数チェック
elseif (mb_strlen($title) > 50) {
    echo 'タイトルは50文字以内で';
}

// 成功時の処理（例）
else {
    echo '入力ありがとうございます：' . htmlspecialchars($title, ENT_QUOTES, 'UTF-8');
}

```

### ✅ 解説

| 処理 | 内容 |
| --- | --- |
| `$_POST['title'] ?? ''` | フォームから送られてきた `title` の値を取得。未定義の場合は空文字で初期化 |
| `trim()` | 入力文字列の前後にある空白を除去 |
| `empty()` | 空文字・NULL・0などの場合に true を返す（空欄チェックに使える） |
| `mb_strlen()` | マルチバイト文字（日本語など）の文字数を正確に数える |
| `htmlspecialchars()` | ユーザー入力を安全に表示する（XSS対策） |

📌 **演習問題**

- メールアドレスが正しい形式かチェックするコードを作ろう
- 年齢が0〜120の範囲内かどうかをチェックするコードを作ろう
- パスワードが8文字以上で英数字を含むかチェックするコードを作ろう

---

## 12. ToDoアプリ（削除・編集機能の追加）

### 概要

このToDoアプリは、以下のような機能を備えたシンプルで実用的なタスク管理アプリです。

PHPとMySQLで構築されており、ユーザーが日々のタスクを登録・完了・編集・削除できることを目的とします。

| 機能 | 説明 |
| --- | --- |
| ✅ タスク追加 | フォームから新しいタスクを登録できる |
| ✅ タスク表示 | 追加されたタスクを一覧で表示 |
| ✅ 完了状態切替 | チェックボックスで完了／未完了の状態を変更可能 |
| ✅ タスク編集 | タスク名を編集できるフォームを表示して内容を更新 |
| ✅ タスク削除 | タスクを削除するボタンでデータベースから削除 |

### 使用する技術

| 項目 | 使用技術・説明 |
| --- | --- |
| 言語 | PHP（バージョン7以上推奨） |
| データベース | MySQL（MAMPやXAMPPで動作） |
| HTML | フォームやリストのUI構築 |
| SQL | データ操作（SELECT, INSERT, UPDATE, DELETE） |
| バリデーション | PHP内でのサーバーサイドバリデーション実装 |

### ファイル構成（単一ファイル構成）

今回のアプリケーションは、以下のような最小構成で動作します：

```

Todo_app/
└── index.php  
```

> 今回は MVC構成は使用せず、学習目的でコードをすべて1つの index.php に記述します。
> 

## 現在の機能（初期実装）

| 機能 | 説明 |
| --- | --- |
| タスク追加 | フォームから新しいタスクを登録 |
| タスク表示 | DBに登録されたタスクを一覧表示 |
| 完了状態切替 | チェックボックスで完了／未完了を切り替え可能 |

## `tasks` テーブル構成（表形式）

| カラム名 | データ型 | 制約・説明 |
| --- | --- | --- |
| `id` | INT | 主キー（自動採番） |
| `title` | VARCHAR(255) | タスクの内容（最大255文字） |
| `is_done` | BOOLEAN | 完了状態（`0` = 未完了, `1` = 完了） |
| `created_at` | DATETIME | 作成日時（自動で現在時刻が入る） |
| `updated_at` | DATETIME | 最終更新日時（更新時に自動で更新される） |

### ✅ 各カラムの意味

- **`id`**：各タスクを一意に識別するための番号。自動で1, 2, 3...と増える
- **`title`**：ユーザーが入力したタスクの内容（例：「買い物に行く」など）
- **`is_done`**：タスクが完了しているかどうかを表す（チェックボックスで切替）
- **`created_at`**：タスクを追加した日時
- **`updated_at`**：タスクが編集または状態変更された日時

---

## 課題について

---

## Question1 タスクに削除機能を追加してみよう

問題：「Todo_app」フォルダ内と同じ階層に「assignment」フォルダを作り、その中に`index.php`ファイルを作成してください。

そのファイルに現在のTodoアプリの機能に対して「タスク削除機能」を追加してください。

※注意：「Todo_app」フォルダ内のindex.phpには書き込まないで下さい。

### 削除機能要件

| 機能 | 内容 |
| --- | --- |
| 削除ボタン | 各タスクの横に「削除」ボタンを表示 |
| 削除処理 | タスクIDを指定してDBから削除 |
| 条件 | `POST['type'] === 'delete'` を使って処理を分岐 |

## Question2 タスクを編集する機能を追加しよう

問題：Question１で作成した`assignment/index.php`ファイル(削除機能を追加したファイル)に、さらに「タスク編集機能」を追加してください。

### 【1】編集機能

| 機能 | 内容 |
| --- | --- |
| 編集ボタン | 各タスクの横に「編集」ボタンを表示 |
| 編集フォーム | タイトルを編集し `UPDATE` でDBを更新 |
| 条件 | `POST['type'] === 'update'` を使って処理を分岐 |

### 実装例

question1とquestion2に関して、以下のようになってればOK！

- 各タスクの右に、**タイトルを変更できるフォーム＋「update」「delete」ボタン**がある

![](https://storage.googleapis.com/zenn-user-upload/d96b136326e2-20250430.png)
---

- 更新フォームに編集したい内容を入力し、「update」ボタンを押すと、タスクのタイトルが変更される

![](https://storage.googleapis.com/zenn-user-upload/1f87cdc8f798-20250430.png)

---

- タスクリストの表示が更新されていて、phpMyAdmin の `tasks` テーブルでも**タイトルが更新されていること**を確認できる

![](https://storage.googleapis.com/zenn-user-upload/a1a5d3e8b30a-20250430.png)

---

- 「delete」ボタンを押すと、そのタスクが画面とデータベース両方から**正しく削除されること**が確認できる

![](https://storage.googleapis.com/zenn-user-upload/fdc0de889442-20250430.png)

## Question3 編集時にバリデーションを実装しよう

バリデーションとは、**ユーザー入力の正当性を確認する処理**です。編集・追加時には以下のようなチェックを行うことで、アプリの安定性と安全性を高めます。

### バリデーションの基本チェック項目

| チェック項目 | 目的 |
| --- | --- |
| 空欄チェック | 必須項目が入力されているか |
| 文字数制限 | 長すぎる入力を制限する |

### 実装例

以下のようになってればOK！

- 編集フォームが空のまま「update」ボタンを押したとき、編集対象のタスクの下に「タイトルは必須です」と表示される

![](https://storage.googleapis.com/zenn-user-upload/7d2ba88057c3-20250430.png)

- 入力が50文字を超えている場合に、「タイトルは50文字以内で入力してください」と表示される

![](https://storage.googleapis.com/zenn-user-upload/6f0130cadf6a-20250430.png)

---

## MySQLと接続するための準備と手順（MAMP使用）

ToDoアプリを動かすには、まず **PHPからMySQLに接続できる状態を作る必要があります。**

### ① MAMPを起動しよう

1. MAMPアプリケーションを起動
2. 「**Open WebStart Page**」をクリック
    
    → ブラウザが開き、MAMPのスタートページにアクセスされます
    

![](https://storage.googleapis.com/zenn-user-upload/8deca73f39de-20250430.png)
### ② MySQLの接続情報を確認しよう

WebStartPageに表示されている接続情報は以下の通りです：

| パラメータ | 値 |
| --- | --- |
| Host | `localhost` |
| Port | `8889` |
| User | `root` |
| Password | `root` |

PHPから接続する際は、**以下のコード**を使ってPDOで接続します。

```php
$pdo = new PDO('mysql:host=localhost;port=8889;dbname=mydb;charset=utf8', 'root', 'root');
```

## データベースとテーブルの作成（phpMyAdmin）

### ① phpMyAdminを開こう

WebStartPageのメニューにある「**phpMyAdmin**」をクリックして管理画面にアクセスします。

もしくは以下のURLを直接開いてもOKです：

```
http://localhost:8889/phpMyAdmin
```

### ② データベースを作成しよう

1. 左のナビゲーションで「**新規作成**」をクリック
2. データベース名に `mydb` と入力し、「作成」をクリック
    
    → これで `mydb` データベースが作成されます
    

### ③ `tasks` テーブルを作成しよう

`mydb` データベースを選択した状態で、**SQLタブ**をクリックし、以下のSQL文を貼り付けて「実行」してください：

```sql

CREATE TABLE tasks (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    is_done BOOLEAN DEFAULT FALSE,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

---

## GitHubでの提出手順（ToDoアプリの作成と提出）

ToDoアプリが完成したら、以下の手順で指定のGitHubリポジトリにアップロード（Push）してください。

### ① リポジトリをクローンしよう

以下のコマンドを使って、指定のリポジトリを自分のローカルにクローンします。

```bash
git clone https://github.com/EpshironPgSchl/epsilon_assignment2.git
```

### ② `assignment` フォルダを作成しよう

クローンしたフォルダに移動して、新しいフォルダ `assignment` を作成します。

```bash
cd epsilon_assignment2
mkdir assignment
cd assignment
```

この中に、今回作成した ToDo アプリの `index.php` を配置してください。

```
epsilon_assignment2/
└── assignment/
   └── index.php
```

### ③ 新しいブランチを作成しよう

作業用のブランチを作成して、そのブランチ上で開発を行います。

```bash
git checkout -b ブランチ名
```

### ④ ファイルを追加してコミットしよう

ToDo アプリが完成したら、ファイルをステージングしてコミットします。

```bash

git add .
git commit -m "ToDoアプリをassignmentフォルダに追加"
```

### ⑤ リモートに Push しよう

コミットした内容を GitHub 上の同じブランチにアップロードします。

```bash

git push origin ブランチ名
```

> origin はクローン元のGitHubリポジトリ、todo-app は作成したブランチ名です
> 

## 提出にあたっての注意

- 作業は必ず `assignment` フォルダ内で行ってください。
- ブランチ名は、だれが作ったかなど内容が分かる名前を使ってください。