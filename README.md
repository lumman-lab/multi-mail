# Multi Mail

Gmail, Outlook, Hotmail, Microsoft 365, iCloud, Fastmail, other IMAP mailboxes: search, read, send.

Multi Mail is a remote MCP server run by Lumman Ltd. It puts every mailbox you connect - Gmail, Outlook.com, Hotmail, Microsoft 365, iCloud, Fastmail and other IMAP mailboxes - behind one connector, so an AI client can search all of them in one call and read, draft, send and organise mail in each. This repository holds what clients install: the manifests for Claude Code, Cursor, Gemini CLI, Antigravity and Kiro, four skills and their evals. The server itself is not in it.

## Before you start

You need a Lumman account with at least one mailbox connected at https://lumman.co/mcp/account/multi-mail. Sign in there with Google, Microsoft, a passkey or an emailed code. Outlook, Hotmail and Microsoft 365 mailboxes connect with Microsoft sign-in, iCloud and Fastmail with an app password, other IMAP mailboxes with their address and a password, and Gmail with Google sign-in while Google's preview has room; once it is full, a Gmail or Google Workspace mailbox connects with an app password. Each mailbox's permissions - reading, drafts, sending, organising and settings - are set on the same page.

## Add it to your client

### Claude

Open Multi Mail in Claude's connectors directory, https://claude.ai/directory/connectors/multi-mail, and press Connect. The listing connects at https://lumman.co/mcp/mail.

### Claude Code

```
/plugin marketplace add lumman-lab/multi-mail
/plugin install multi-mail@multi-mail
```

The plugin adds the connector at https://lumman.co/mcp/mail and the four skills below. The first time a skill reaches the connector, Claude Code asks you to sign in; if it does not, run `/mcp` and choose the multi-mail server.

### Cursor

Add the connector to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "multi-mail": { "url": "https://mail.lumman.co/mcp" }
  }
}
```

### VS Code

Run `MCP: Add Server`, choose `HTTP`, paste `https://mail.lumman.co/mcp` and name it `multi-mail`. Or add it to your user `mcp.json`:

```json
{
  "servers": {
    "multi-mail": { "type": "http", "url": "https://mail.lumman.co/mcp" }
  }
}
```

### Gemini CLI

```
gemini extensions install https://github.com/lumman-lab/multi-mail
```

The extension adds the connector at https://mail.lumman.co/mcp and the four skills below. Its first call opens Lumman's sign-in in your browser; `/mcp auth multi-mail` opens it again.

### Antigravity

```
agy plugin install https://github.com/lumman-lab/multi-mail
```

The plugin adds the connector at https://mail.lumman.co/mcp and the four skills below, for the Antigravity CLI, app and IDE alike. To sign in, run `/mcp` in the CLI, open `multi-mail_multi-mail` and choose Authenticate, or in the app or IDE press Authenticate next to it under Agent settings, Customizations; approve on the Lumman page that opens, then paste the code Antigravity's page shows back into Antigravity.

### Kiro

In the Powers panel press Add Custom Power, choose Import power from GitHub, paste `https://github.com/lumman-lab/multi-mail/tree/main/kiro` and press Install. The power adds the connector at https://mail.lumman.co/mcp.

### ChatGPT

Works fully on ChatGPT Business, Enterprise and Edu.

1. For a mailbox you connect with a password, add it first in your account, under Add a mailbox.
2. Open chatgpt.com/plugins, press +, then Add custom MCP server.
3. Name it Multi Mail, paste `https://mail.lumman.co/mcp`, choose OAuth, tick the box and press Create as a plugin.
4. Install it. On the Lumman page, sign in, add a mailbox if none is connected, and approve.
5. In a chat, type @ and choose Multi Mail.

### Any other client

Add a remote MCP server at `https://mail.lumman.co/mcp`: Streamable HTTP, OAuth 2.1 with dynamic client registration. No key or client id is needed.

## Signing in

The connector answers a client's first call with where to sign in. The client registers itself with Lumman's authorisation server and opens a Lumman page that names it: sign in, add a mailbox if none is connected, and approve. Every client you approve is listed under AI apps at https://lumman.co/mcp/account/multi-mail, where it can be removed.

## Skills

Claude Code, Cursor, Gemini CLI and Antigravity load four skills with the connector, and pick one by themselves when a request matches it. In Claude Code each is also a command, such as `/multi-mail:triage`.

- `triage` - what is waiting across every mailbox: what needs a reply, what needs a decision, what can wait. Changes nothing.
- `attachments` - what a PDF (scanned pages included), Word, Excel or PowerPoint attachment says, read as text.
- `drafting` - a new message, reply or forward written as a draft and shown to you, then sent only after you say yes to that draft.
- `labels` - duplicate labels (Outlook categories), and in Gmail unused ones, found and a merge proposed, with nothing changed until you agree.

Examples:

- "What in my Outlook and Gmail still needs a reply?"
- "What total does the invoice Dana sent to my Hotmail come to?"
- "Reply to Sam in Outlook that Friday works, and show me before it goes."

## Ready requests

The connector offers these requests ready-made; a client shows them as prompts or commands.

- `needs_reply` - What needs a reply. Messages across all your mailboxes still waiting for your answer.
- `waiting_on` - Who is waiting on whom. Who waits on your reply, and whose reply you wait on, across all your mailboxes.
- `tidy_newsletters` - Tidy newsletters. Find newsletters and promotions across all your mailboxes and archive them.
- `morning_brief` - Morning brief. A short summary of every inbox, made to run as a Claude scheduled task.
- `clean_up_inbox` - Clean up my inbox. See who fills an inbox, then clear only the groups you choose.
- `keep_tidy` - Keep my inbox tidy. Keep the newest few from the senders you choose and archive the rest, set up as a scheduled task.
- `manage_rules` - Manage my rules. See the rules that file your incoming mail, and add, change or remove only the ones you choose.

## Tools

| Tool | Name | What it does |
|---|---|---|
| `mailboxes_list` | List mailboxes | The mailboxes this account holds, by name |
| `messages_list` | Search a mailbox | One mailbox, in its provider's search terms |
| `messages_list_all_mailboxes` | Search every mailbox | Every mailbox at once, newest first |
| `threads_get` | Read a thread | Every message in one thread |
| `messages_get` | Read a message | One message, with its headers and body |
| `messages_attachments_get` | Read an attachment | What one attachment holds |
| `sweeps_preview` | Preview a clear-out | Who fills a folder, by sender |
| `drafts_create` | Draft a message | Composes a message kept as a draft |
| `drafts_update` | Edit a draft | Replaces what a draft says |
| `drafts_reply` | Draft a reply | A reply, drafted inside its thread |
| `drafts_forward` | Draft a forward | A forward with its files, as a draft |
| `drafts_delete` | Discard a draft | Throws a draft away, nothing sent is touched |
| `messages_send` | Send a message | Composes a new message and sends it |
| `drafts_send` | Send a draft | Sends a draft out of the mailbox |
| `messages_reply` | Reply to a message | Sends a reply inside the message's thread |
| `messages_forward` | Forward a message | Sends a message on, with its files |
| `labels_list` | List labels | The labels the mailbox holds, with their ids |
| `labels_create` | Create a label | Creates a label and returns its id |
| `labels_update` | Edit a label | Renames or recolours a label |
| `labels_delete` | Delete a label | Deletes a label, every message stays |
| `threads_modify` | Label a thread | Adds or removes the labels a thread holds |
| `threads_archive` | Archive a thread | Out of the inbox, still in search |
| `threads_trash` | Move a thread to the trash | Into the trash, where the provider keeps it |
| `threads_untrash` | Restore a thread from the trash | Back out of the trash |
| `sweeps_apply` | Clear out a preview | Bins, archives, files or marks read its groups |
| `sweeps_put_back` | Put a clear-out back | Returns what a clear-out moved, for 7 days |
| `settings_filters_list` | List filters | The rules incoming mail is filed by |
| `settings_filters_create` | Create a filter | Files incoming mail - no forward, bin or junk |
| `settings_filters_update` | Change a filter | Changes, pauses or resumes a rule |
| `settings_filters_delete` | Delete a filter | Deletes a rule, filed mail stays put |
| `settings_send_as_patch` | Edit the signature | Replaces the signature its mail goes out with |
| `settings_send_as_get` | Read the signature | The signature its mail goes out with |
| `settings_send_as_find` | Find the signature | The signature its sent mail carries, as a draft |
| `settings_get_vacation` | Read the vacation responder | Whether it replies, and what it says |
| `settings_update_vacation` | Set the vacation responder | Turns it on or off, and what it says |

## Where your mail goes

Claude and Claude Code send every call to https://lumman.co/mcp/mail, every other client to https://mail.lumman.co/mcp - two addresses of one server, run by Lumman. Signing in runs through the authorisation server those addresses name. Lumman keeps no copy of your mail: each message and attachment is fetched from its provider when a client asks, its words are screened for prompt attacks by Google Cloud's Model Armor - an attachment asked for as the original file is not - as are the words of every draft and send before they reach the provider, and the mail is passed on only to the client you approved - an attachment's original also to whoever holds the 15-minute link that client is given. What the connector passes on, and to whom, is in the privacy policy: https://lumman.co/privacy.

The drafting skill asks the client to show a draft and wait for your yes. What the connector itself enforces is each mailbox's permission to send, set at https://lumman.co/mcp/account/multi-mail: with sending off, nothing is sent, whatever a client asks.

## Limits

- Gmail sign-in is in Google's preview, which admits a fixed number of accounts; once its places are spent, a Gmail or Google Workspace mailbox connects with an app password.
- A clear-out, and any change to a draft, in a mailbox connected with a password needs a mail server that names where it moves each message, as iCloud, Fastmail and Gmail do, and clears a Gmail connected that way out of its inbox alone.
- Microsoft lets an Outlook category take a new colour, never a new name.
- Mailboxes connected with a password - iCloud, Fastmail, Gmail and other IMAP mailboxes - take every tool except filters and the vacation responder. iCloud and Fastmail labels are their folders, as your own mail app shows them, and the labels skill leaves them alone.
- Yahoo, AOL, Yandex and Mail.ru mailboxes are not connected.
- Each account has a daily allowance of tool calls; past it, a call is refused with the time the next one is available.
- A message whose words screen as a prompt attack is withheld from the answer that would carry it, and the rest is still given; anything else that screens so is refused, and a call whose screening cannot finish is closed.

## Evals

`claude plugin eval .` runs four cases, one per skill, and thirteen `choose-*` cases, against invented Hotmail, Gmail, iCloud and IMAP mailboxes answered from fixed mock files under `evals/`. Each `choose-*` case is a request in a person's own words - a mailbox by its provider, every account at once, sending, filing, a rule, an auto-reply, clearing out an inbox - that the connector's tools should take, and three are requests no mail tool should take. They read the tools' own descriptions, saved in `evals/mocks/multi-mail/_tools.json`; the mocks carry no server instructions. Run on 2 November 2026 with Claude Code 2.1.308 and model claude-sonnet-5-5, three runs per case: all thirteen passed 3 of 3.

To see what the skills add, each of the four skill cases ran in two setups with the connector's tools in place: once with the plugin as shipped, once with its `skills/` folder removed (`claude plugin eval <copy> --ablation none`). Run on 18 October 2026 with Claude Code 2.1.292, model claude-sonnet-5-5 and the CLI's default Haiku judge, three runs per case each way:

- triage - lists the two threads waiting for a reply and nothing else: 3 of 3 with the skills and 3 of 3 without. The skill adds nothing measurable here.
- attachments - gives the total and due date read off the invoice PDF: 3 of 3 with and without. The skill adds nothing measurable here.
- drafting - saves the reply as a draft, shows it and asks before sending: 3 of 3 with, 0 of 3 without; without the skills Claude sent the reply at once in every run.
- labels - proposes the merge and asks before changing anything: 3 of 3 with, 0 of 3 without; without them Claude re-labelled messages before asking in every run.

Overall score 1.00 with the skills and 0.74 without. Three runs per case is a small sample, and the mocks answer the same whatever Claude changes.

## Security

Report a vulnerability privately through GitHub, as [SECURITY.md](SECURITY.md) describes.

## Support

Write to the address under Contact Us in Lumman's privacy policy: https://lumman.co/privacy.

## Licence

The files in this repository are under the MIT licence in [LICENSE](LICENSE). The Multi Mail service they connect to is provided under Lumman's terms: https://lumman.co/terms.
