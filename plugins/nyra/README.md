# Nyra for Claude

Connect Claude to your live books. Nyra is the bookkeeping platform from
[Otterz](https://otterz.co): AI agents do the bookkeeping, humans supervise.

This plugin points Claude at Nyra's hosted MCP server. There is nothing to install
locally and no API key to paste — you sign in with your Otterz account through OAuth
on first use.

## Install

```
/plugin marketplace add OtterzInc/nyra-claude-plugin
/plugin install nyra@otterz
```

The first time Claude uses a Nyra tool it opens your browser to authorize the
connection. Access is scoped to the businesses your Otterz account can already see.

## What Claude can do

**Read your books**
`list_businesses` · `get_financial_summary` · `get_cash_position` ·
`get_profit_and_loss` · `get_balance_sheet` · `list_transactions` ·
`list_open_approvals` · `list_open_tasks`

**Send work in**
`create_upload_link` · `upload_document` · `start_document_upload` ·
`submit_uploaded_document` · `document_status` · `document_findings` ·
`list_submitted_documents` · `upload_quota` · `list_questions_for_me` ·
`answer_question` · `flag_for_review`

## What it deliberately cannot do

- **No ledger writes.** Nothing Claude does posts a journal entry. Documents you send
  in land in the supervised approval queue, where a human approves them.
- **No downloads, no deletes.** There is no tool that returns a stored document or
  removes one.
- **Scoped access.** Every call is limited to the businesses your account can access.
- **Rate limited.** 30 documents per user per rolling 24 hours.

## Privacy and terms

- [Privacy policy](https://otterz.co/privacy-policy/)
- [Terms](https://otterz.co/terms-conditions/)
- Support: support@otterz.co

## Using it without the plugin

The same server works as a custom connector in Claude Desktop and the web app, and in
any other MCP client. Add `https://mcp.otterz.co/mcp` as a custom connector.

## License

Apache-2.0. See [LICENSE](LICENSE). The Nyra service itself is proprietary; this
repository contains only the Claude plugin manifest and documentation.
