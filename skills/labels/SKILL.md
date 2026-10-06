---
name: labels
description: Tidy the labels of a connected Outlook, Hotmail, Microsoft 365 or Gmail mailbox - in Outlook its categories - by finding duplicates and, in Gmail, labels nothing carries, proposing merges, renames and removals, and changing nothing until the person agrees. Use when asked to clean up, merge or prune labels or categories.
---

# Label hygiene

1. List the labels of each mailbox in question with `labels_list`. An Outlook mailbox's categories are its labels. Gmail's own system labels (INBOX, SENT, SPAM, TRASH and the like) are not the person's to tidy.
2. Find what to tidy:
   - duplicates and near-duplicates - one name in another case, spacing, spelling or plural ("Receipts", "Reciepts");
   - labels nothing carries - in Gmail, search for each label's threads with `messages_list` (label:name). An Outlook category cannot be searched for: its messages are found only by reading the categories on the messages a search answers, so never call an Outlook category unused on that evidence;
   - in Gmail, one subject split across two parents by "/" nesting.
3. Propose a plan, one line per change: the label kept, the labels merged into it, those renamed or removed, and how many threads each change moves - in Outlook, among the mail searched. Change nothing yet.
4. On the person's yes to the plan, do what it says and nothing more:
   - merge - on every thread carrying the old label, `threads_modify` adds the kept label and removes the old one; only then does `labels_delete` remove the old label. A Gmail search answers a page at a time, so search for the old label again until it answers nothing before deleting it. In Outlook the merge reaches only the threads found carrying it, so say that messages the searches did not reach keep the old name;
   - rename - `labels_update` with the new name, in Gmail. Microsoft lets an Outlook category take only a new colour, so an Outlook rename is a new category from `labels_create`, the threads moved onto it, then the old one deleted;
   - remove - `labels_delete`. No message is deleted: in Gmail the label comes off every message; an Outlook category leaves the list while the messages that carried it keep its name, so move them first.
5. Report what changed and anything that failed, label by label.

Never add or remove SPAM or TRASH here: that junks or bins mail.

Examples:

- "Tidy the categories in my Outlook."
- "My Hotmail has both Receipts and Reciepts - merge them."
- "Which of my Gmail labels have nothing in them?"
