---
name: attachments
description: Read what an email attachment says - PDF including scanned pages, Word, Excel, PowerPoint - as text, from any connected Outlook, Hotmail, Microsoft 365, Gmail, Yahoo, AOL, iCloud, Fastmail or other IMAP mailbox. Use when asked what a file someone sent says, to pull a figure or a date out of one, or to compare attachments.
---

# Read attachments as text

1. Find the message: across every mailbox with `messages_list_all_mailboxes`, or one mailbox with `messages_list` in its own query language - Outlook reads hasAttachments:true, Gmail has:attachment and filename:pdf. A search answers only its first results: before saying the message is not there, search alone each mailbox the answer names under `more`, and page on with the token `messages_list` answers.
2. Read it with `messages_get`, or the whole conversation with `threads_get`. Each message names its attachments with their ids and sizes.
3. Read the file with `messages_attachments_get`. It answers what the file says, as plain text. A long document comes in parts: where the answer names a continuation, ask again with it before answering anything that depends on the whole document.
4. Fetch the original whenever the words read back make no sense - a scan read sideways comes back as noise - or the person wants the file itself. Every answer names a link to it, served whole for 15 minutes after it is given to a plain GET carrying no credential: from a terminal, `curl --fail-with-body -o <a new path of your own> "<link>"` fetches it to open with your own tools, and elsewhere ask again with as original. To carry a file into a draft, name it by its mailbox, message id and attachment id rather than copying its bytes - that works from any connected mailbox into a draft in the same mailbox or any other.

Quote figures, dates and names exactly as the text has them, and say which file each came from. Where the answer says no words could be read - a file locked by a password, one with no words, one that took longer to read than a call may run - say so, and that the original can still be had. Never guess at what a file says.

Examples:

- "What total does the invoice Dana sent to my Outlook come to?"
- "Read the PDF attached to the latest email from the letting agent in Hotmail and list its dates."
- "Compare the two spreadsheets attached to the budget thread in Gmail."
