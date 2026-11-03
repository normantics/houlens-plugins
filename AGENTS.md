# AGENTS.md

このリポジトリは、法レンズ (https://houlens.jp) のMCPサーバを、AnthropicとOpenAIのディレクトリへ出すためのプラグインを置く。法レンズの本体のコードは置かない。

## 置くもの

- `claude/houlens/`: Claude向けのプラグイン。MCPサーバの設定は `https://houlens.jp/api/mcp` の1つだけにする。
- `openai/houlens/`: ChatGPTとCodex向けのプラグイン。MCPサーバの設定は `https://houlens.jp/api/mcp/openai` の1つだけにする。
- `submission/`: 申請の画面に入れる文の下書き。リポジトリを公開にする前に消す。

## 守ること

1. 秘密 (APIキー、トークン、審査用の資格情報) をファイルにもコミットにも書かない。
2. スキルの文は、法レンズの本体のMCPサーバの instructions と、法レンズの接続の案内と食い違わないように書き、事実を足さない。instructions を変えたときは、同じ日にスキルも直す。
3. Claude向けのプラグインを変えたら、`claude plugin validate ./claude/houlens` を流して通してからコミットする。

## コミットとPRの書き方

コミットの件名には、何を変えたかを書く。本文には、何を変えたか、なぜ変えたか、何を確かめたかを書く。PRの説明文も同じ内容で書く。自動のコミットは除く。
