---
title: "Claude MCPのざっと概要"
emoji: "🆕"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["claude","claudemcp","tech","newfeature"]
published: false
---
は〜いこんにちは⤵︎
またまたB4の猪田です。

今日は、最近Claudeを開発したAnthropic社が作った「**Model Context Protocol(MCP)**」について超絶ざっと概要だけ紹介したいと思います。
僕自身弱々情報学生ですが、自分でも理解できるくらい咀嚼して書いたので概要を軽く理解したい方は是非読んでってください。

## 私たちの研究室(NISLab)

https://nisk.doshisha.ac.jp/

## アドベントカレンダー 8日目~

https://nislab-advent-calendar-2024-12.vercel.app/

---

## MCP(Model Context Protocol)とは？

一言で言うと、
**「githubやGoogle Drive等の外部のツールやデータをclaudeやChatGPTで簡単に操作したりデータやり取りしたりする仕組みのこと」** です。

これまで、複雑なプログラムを用意しなければアクセスできなかった外部ツールやデータソースに、チャットだけでアクセス・操作が可能になります。

このプロトコルは、Claudeを開発しているAnthropic社が主導となり、GoogleやGitHubといった主要な企業を巻き込んで作ったルールで、これにより、外部ツールとのスムーズなデータのやり取りが可能となったオープンプロトコルです。

---

## MCPのアーキテクチャ

以下が公式ドキュメントより引用したMCPの基本アーキテクチャです。
![](https://storage.googleapis.com/zenn-user-upload/e4646a5ad035-20241207.png)

MCPは以下の3つの要素で構成されています：

1. **MCP Host**
   - リソース(データ)にアクセスするためのインターフェース。例として、Claudeや統合開発環境 (IDEs) が挙げられます。

2. **MCP Server**
   - リソースごとに構築され、特定のデータや機能をMCPホストに提供します。
   - 例：天気情報にアクセスするためのMCPサーバを構築すれば、チャットを通じて天気情報が取得可能になります。

3. **(Local or Remote) Resource**
   - データや情報の集合体で、MCPサーバがアクセスする対象。例えばGoogle DriveやBraveブラウザ。

:::message
つまり、任意の外部ツールへの**MCPサーバを構築**さえすれば、Claude等でチャットで操作、アクセスし放題になります。
:::

---

## MCPサーバについて

すでに、用意されたMCPサーバもいくつかあります。

![](https://storage.googleapis.com/zenn-user-upload/517c2434fed8-20241207.png)

それぞれのサーバの機能や簡単なセットアップ方法なども紹介されているので、興味ある方は見てみてください。
https://github.com/modelcontextprotocol/servers



また、すでに準備されたMCPサーバを活用するだけでなく、**独自のサーバを構築**することも可能です!!
実際に強強エンジニアの方がnotionにアクセスするサーバを自作されていたので自分でサーバを構築してみたい方はよければ参考にしてみてください！
https://qiita.com/suekou/items/44c864583f5e3e6325d9

## MCPを試してみる

ここまで読んで、MCP実際に触ってみたいという方は、ぜひラボのメンバーが実践記事を書いているのでそれを見ながら実際に触ってみてください！
https://zenn.dev/nislab/articles/2024-11-30-claude-mcp

一応公式ドキュメントも貼っておきます。

https://modelcontextprotocol.io/quickstart

---

## 感想

MCPの登場によって、これまで既に強力だったLLMアプリケーションがより強力なツールになると感じました。
今後、さまざまなサーバが構築されたり、MCPを用いたサービスによってこのプロトコルがどのように進化し、日常業務や技術分野にどのような影響を与えるのか、個人的にめちゃくちゃ楽しみです！！

## 参考文献
https://modelcontextprotocol.io/introduction

https://www.anthropic.com/news/model-context-protocol

https://github.com/modelcontextprotocol/servers
