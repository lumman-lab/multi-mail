---
name: attachments
description: Read what an email attachment says - PDF including scanned pages, Word, Excel, PowerPoint - as text, from any connected Outlook, Hotmail, Microsoft 365, Gmail, iCloud or Fastmail mailbox. Use when asked what a file someone sent says, to pull a figure or a date out of one, or to compare attachments.
---

# Read attachments as text

1. Find the message: across every mailbox with `messages_list_all_mailboxes`, or one mailbox with `messages_list` in its own query language - Outlook reads hasAttachments:true, Gmail has:attachment and filename:pdf. A search answers only its first results: before saying the message is not there, search alone each mailbox the answer names under `more`, and page on with the token `messages_list` answers.
2. Read it with `messages_get`, or the whole conversation with `threads_get`. Each message names its attachments with their ids and sizes.
3. Read the file with `messages_attachments_get`. It answers what the file says, as plain text. A long document comes in parts: where the answer names a continuation, ask again with it before answering anything that depends on the whole document.
4. Ask for the original only when the person wants the file itself. To carry a file into a draft, name it by its mailbox, message id and attachment id rather than copying its bytes - that works Gmail to Gmail, Outlook to Outlook, and between any iCloud and Fastmail mailboxes.

Quote figures, dates and names exactly as the text has them, and say which file each came from. Where the answer says no words could be read - a file locked by a password, one with no words, one that took longer to read than a call may run - say so, and that the original can still be had. Never guess at what a file says.

Examples:

- "What total does the invoice Dana sent to my Outlook come to?"
- "Read the PDF attached to the latest email from the letting agent in Hotmail and list its dates."
- "Compare the two spreadsheets attached to the budget thread in Gmail."
