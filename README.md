# Houlens plugins

Plugins that connect AI assistants to Houlens (法レンズ), a search service for Japanese case law and statutes run by Normantics Inc.

- `claude/houlens/`: the plugin for Claude. It contains the Houlens remote MCP server (`https://houlens.jp/api/mcp`) and a skill that teaches Claude how to use the Houlens tools
- `openai/houlens/`: the plugin package for ChatGPT and Codex. It points to the Houlens MCP endpoint for OpenAI clients (`https://houlens.jp/api/mcp/openai`)

このリポジトリには、AIのクライアントを法レンズへ接続するプラグインを置きます。`claude/houlens/` はClaude向け、`openai/houlens/` はChatGPTとCodex向けです。

Both plugins are released under the MIT License.
