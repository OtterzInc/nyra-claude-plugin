---
description: Review a business's books through Nyra — pull the P&L, balance sheet, and cash position, reconcile them against transactions, and surface what needs attention before close. Use when the user asks about their financials, month-end close, cash runway, open approvals, or "how is the business doing".
---

# Reviewing books with Nyra

Nyra reads a live general ledger. Numbers you get back are the client's real books — never
estimate, extrapolate, or fill a gap with a plausible figure. If a tool returns nothing, say so.

## Start by establishing scope

Always call `list_businesses` first. A user may have access to several businesses, and every
other tool is scoped to a business. Never assume which one they mean when there is more than one.

## Pulling the picture

- `get_financial_summary` — the fastest single call for "how are we doing".
- `get_profit_and_loss` / `get_balance_sheet` — statements for a period or as-of date.
- `get_cash_position` — cash on hand across accounts.
- `list_transactions` — the underlying detail. Reach for this when a statement line looks
  surprising; explain a variance from actual transactions rather than from intuition.

Report periods explicitly. "Revenue was $X" is ambiguous; "Revenue was $X for Jan–Jun 2026" is not.

## What needs a human

- `list_open_approvals` — postings waiting on a supervisor. These are *not* yet in the books;
  say so when they would change a number you just reported.
- `list_open_tasks` — bookkeeping work outstanding.
- `list_questions_for_me` — the bookkeeper is blocked on the client. Surface these proactively
  during any review; answer with `answer_question` only using what the user actually told you.
- `flag_for_review` — when you find something genuinely wrong, escalate rather than speculating
  in prose.

## Sending documents in

`create_upload_link` is the path that works for real documents: it returns a link the *user*
opens in their own browser. Prefer it. `upload_document` takes inline base64 but is capped at
64KB, so it suits only a small receipt. Track what you sent with `document_status`,
`document_findings`, and `list_submitted_documents`; `upload_quota` shows the remaining daily
allowance.

Uploads land in the processing pipeline and end in the approval queue — they do not post to the
ledger. Tell the user that, so nobody expects an immediate change in their statements.

## Boundaries

Nyra cannot post journal entries, download stored documents, or delete anything. Those are
deliberate. If a user asks you to change the books, explain that postings go through the
approval queue in the Otterz portal, and offer `flag_for_review` instead.

Do not give tax advice or an audit opinion. Report what the books say and what looks
inconsistent; leave the judgment to their accountant.
