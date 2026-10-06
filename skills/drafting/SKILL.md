---
name: drafting
description: Write, reply to or forward an email from a connected Outlook, Hotmail, Microsoft 365 or Gmail mailbox as a draft, show it, and send it only after the person says yes to that draft. Use for any request to write, answer or forward mail.
---

# Draft, confirm, then send

Nothing is sent until the person has seen the draft and said yes to it.

1. Write a draft, never a direct send:
   - a new message - `drafts_create`;
   - a reply, kept in its thread and quoting the message below - `drafts_reply`, with replyAll to answer everyone on it;
   - a forward with the files it carries - `drafts_forward`.

   Write from the mailbox the conversation is in. For a new message, ask which mailbox when more than one could send it.
2. Show the draft: the mailbox it is in, who it goes to, who is copied and blind-copied, the subject, the text and every file it carries. Ask whether to send it.
3. For changes, edit the same draft with `drafts_update` - a field left out stays as it was - and show it again.
4. Only on an explicit yes to the draft as last shown, send it with `drafts_send`, under a request id of your own that is new for this message. A yes to an earlier version is not a yes to this one.
5. If the answer says the provider is holding back its sending, send again later under the same request id. If it says the message may have gone, send nothing more under that id: look in that mailbox's sent mail first.

This skill never uses `messages_send`, `messages_reply` or `messages_forward`: each sends in one call, with no draft to show.

A draft that is not wanted: `drafts_delete` discards it in a Gmail mailbox. An Outlook draft keeps its id once sent, so the connector never discards one - ask the person to delete it in Outlook.

Examples:

- "Reply to Sam in my Outlook that Friday works for signing the lease."
- "Forward the boarding pass in Hotmail to alex@example.com."
- "Draft a note from Gmail asking the landlord when the boiler will be fixed."
