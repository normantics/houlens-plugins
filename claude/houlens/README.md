# 法レンズのClaude向けプラグイン

## 日本語

このプラグインは、Claudeを法レンズにつなぎます。法レンズは、株式会社Normanticsが運営する、AIエージェントの検索と読解に最適化した日本の判例と条文の検索サービスです。

法レンズは、資料と一緒に、次に何を調べるとよいかの手掛かりも返します。そのためClaudeは、届いた資料を読みながら、次の検索や読む箇所を自分で選び、調査を組み立てていけます。あなたは、回答の根拠を原文で確かめられます。

プラグインは、法レンズのMCPサーバ `https://houlens.jp/api/mcp` と、そのツールの使い方をClaudeに教えるスキルを追加します。スキルを入れると、Claudeは判例を特定してから言及し、裁判所・言渡日・事件番号と法レンズの判例IDを添え、判決文の実文を引用します。検索が0件のときも、判例が存在しないとは断定しません。

### houlens.jp へ送る情報

- Claudeがあなたの問いから組み立てるツールの引数。検索の文、判例ID、事件番号、裁判所名、日付、法令名、条番号です。検索の文には、会話の中の語が入ることがあります
- あなたが法レンズにログインして接続を承認したときに発行される、OAuthのアクセストークン

このプラグインは、あなたのパソコンでプログラムを動かさず、データを `houlens.jp` だけへ送ります。法レンズが受け取った情報の扱いと、意味検索に使う外部のサービスは、[プライバシーポリシー](https://houlens.jp/privacy)に書いてあります。

### 利用の条件

利用には、法レンズのアカウントとご契約が必要です。Claudeが最初にツールを使うときに、法レンズへのログインを求めます。接続の案内は https://houlens.jp/connect に、利用規約は https://houlens.jp/terms にあります。

法レンズは、調べるための資料を届けるサービスで、法律相談や個別の判断はしません。最終的な法的判断については、専門家にご相談ください。

## English

This plugin connects Claude to Houlens (法レンズ), a search service for Japanese case law and statutes run by Normantics Inc. Houlens is built for the search and reading done by AI agents. Along with each result, it returns cues for what to look at next, so Claude can choose its next search or the next part of a decision to read and build the research step by step. You can check the grounds of each answer in the source text.

The plugin adds the Houlens remote MCP server at `https://houlens.jp/api/mcp` and a skill that teaches Claude how to use its tools. With the skill, Claude identifies each decision before citing it, adds the court, date of decision, case number, and Houlens case ID, quotes the actual text of the decision, and does not claim that a decision does not exist when a search returns no results.

### What the plugin sends to houlens.jp

- The tool arguments that Claude builds from your questions: search text, which can include words from your conversation, case IDs, case numbers, court names, dates, law names, and article numbers
- The OAuth access token issued when you sign in to Houlens and approve the connection

The plugin runs no local code and sends data only to `houlens.jp`. How Houlens handles the data it receives, including the external services it uses for semantic search, is described in the [privacy policy](https://houlens.jp/privacy).

### Requirements

You need a Houlens account with an active Houlens contract. Claude asks you to sign in to Houlens the first time it uses a tool. The setup guide is at https://houlens.jp/connect, and the terms of service are at https://houlens.jp/terms.

Houlens provides research material and does not give legal advice. For a final legal judgment, consult a professional.
