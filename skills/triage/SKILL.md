---
name: triage
description: Sort what is waiting across every connected mailbox - Outlook, Hotmail, Microsoft 365 and Gmail together - into what needs a reply, what needs a decision and what can wait. Use when asked what needs attention, what is still waiting for an answer, or for a summary of the inboxes.
---

# Triage across mailboxes

This skill reads and changes nothing: no drafts, labels, archiving or sending.

1. Call `mailboxes_list`. It names every connected mailbox by the name the other tools take. Say which mailbox could not be read.
2. Search every mailbox at once with `messages_list_all_mailboxes`, by thread. Across providers only from:, to:, subject:, plain words and quoted phrases read alike, so keep the shared query to those. The answer names the mailbox of each result and any mailbox it could not search. It takes only a few results from each mailbox and names under `more` every mailbox holding others: search each of those alone as in step 3.
3. For a time window or anything only one provider reads (Outlook's received:, Gmail's newer_than:), search that mailbox alone with `messages_list` in its own query language, paging with the token it answers.
4. Open a thread with `threads_get` only where its snippet cannot tell whether it waits on the person.

A thread waits on the person when its newest message came from a person rather than a list or an automated sender, is addressed to them, and asks something or expects an answer they have not sent. A message that wants an act rather than an answer - a bill to pay, a form to sign - is a decision, not a reply.

Answer grouped by mailbox, the longest waiting first:

- Needs a reply - who wrote, the subject, what they need in one line, how long it has waited.
- Needs a decision or has a deadline - one line each.
- The rest - a count of newsletters, promotions and notifications, not a list.

Examples:

- "What in my Outlook and Gmail still needs a reply?"
- "Anything in Hotmail from this week I have not answered?"
- "Give me a morning summary of all my inboxes."
