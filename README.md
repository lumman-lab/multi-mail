# Multi Mail

Gmail, Outlook, Hotmail, iCloud and Fastmail mailboxes - several at once, one search across all.

A Claude Code plugin made by Lumman. It connects Claude Code to the Multi Mail connector and adds four skills for working across your mailboxes.

## Install

```
/plugin marketplace add lumman-lab/multi-mail
/plugin install multi-mail@multi-mail
```

You need a Lumman account with your mailboxes connected at https://lumman.co/mcp, where each mailbox's permissions are set. The first time a skill reaches the connector, Claude Code asks you to sign in; if it does not, run `/mcp` and choose the multi-mail server.

## Skills

- `/multi-mail:triage` - what is waiting across every mailbox: what needs a reply, what needs a decision, what can wait. Changes nothing.
- `/multi-mail:attachments` - what a PDF (scanned pages included), Word, Excel or PowerPoint attachment says, read as text.
- `/multi-mail:drafting` - a new message, reply or forward written as a draft and shown to you, then sent only after you say yes to that draft.
- `/multi-mail:labels` - duplicate labels (Outlook categories), and in Gmail unused ones, found and a merge proposed, with nothing changed until you agree.

Claude also picks a skill by itself when a request matches it.

## Examples

- "What in my Outlook and Gmail still needs a reply?"
- "What total does the invoice Dana sent to my Hotmail come to?"
- "Reply to Sam in Outlook that Friday works, and show me before it goes."

## Where your mail goes

Every call the plugin makes goes to one address: https://lumman.co/mcp/mail. Signing in runs through the authorisation server that address names. What the connector passes on, and to whom, is in the privacy policy: https://lumman.co/privacy.

The drafting skill asks Claude to show a draft and wait for your yes. What the connector itself enforces is each mailbox's permission to send, set at https://lumman.co/mcp: with sending off, nothing is sent, whatever a client asks.

## Limits

- Gmail mailboxes are in Google's preview, which admits a fixed number of accounts; once its places are spent, no new Gmail mailbox can be connected.
- Discarding a draft, and reading or setting a signature, work in Gmail mailboxes only.
- Microsoft lets an Outlook category take a new colour, never a new name.
- iCloud and Fastmail mailboxes connect with an app password and take every tool except filters, the vacation responder, send-as and discarding a draft. Their labels are their folders, as your own mail app shows them, and the labels skill leaves them alone.
- Mail whose words screen as a prompt attack is refused rather than passed on, and a call whose screening cannot finish is closed.

## Evals

`claude plugin eval .` runs four cases, one per skill, against invented Hotmail and Gmail mailboxes answered from fixed mock files under `evals/`.

To see what the skills add, every case ran in two setups with the connector's tools in place: once with the plugin as shipped, once with its `skills/` folder removed (`claude plugin eval <copy> --ablation none`). Run on 6 October 2026 with Claude Code 2.1.285, model claude-sonnet-5-5 and judge claude-haiku-4-5, three runs per case each way:

- triage - lists the two threads waiting for a reply and nothing else: 3 of 3 with the skills, 1 of 3 without; without them the invoice was twice listed as needing a reply.
- attachments - gives the total and due date read off the invoice PDF: 3 of 3 with and without. The skill adds nothing measurable here.
- drafting - saves the reply as a draft, shows it and asks before sending: 3 of 3 with, 0 of 3 without; without the skills Claude sent the reply at once in every run.
- labels - proposes the merge and asks before changing anything: 3 of 3 with, 0 of 3 without; without them Claude re-labelled messages before asking in every run.

Overall score 1.00 with the skills and 0.625 without. Three runs per case is a small sample, and the mocks answer the same whatever Claude changes.

## Support

[in@lumman.co](mailto:in@lumman.co)

## Licence

MIT
