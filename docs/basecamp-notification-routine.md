# Basecamp notification clean-up routine

Set up 2026-11-19. Claude marks routine Basecamp notifications as read so the
Hey! menu only shows what needs attention. It never posts, edits, deletes or
unsubscribes; it only reads notifications and marks some of them read.

Names of people and clients are left out of this copy on purpose, because this
repository is public. The live rules, with the real names, are stored in the
scheduled tasks themselves.

## Schedule (Singapore time)

| Run | Time | Notes |
|---|---|---|
| Evening | 8:15 PM daily | Holds the rules |
| Late evening | 10:00 PM daily (runs at 9:57) | Reads the rules from the evening task |
| Midnight | 12:00 AM daily (runs about 12:03) | Reads the rules from the evening task |

All three tasks run inside one Claude Code conversation. If that conversation is
archived, they all stop.

## What gets cleared (marked as read)

A. **Due date changes** – title starts with `Due date changed:`.

B. **Completions** – title starts with `Completed:`.

C. **The QC teammate's comments** – title starts with `Re:`, written by the
   teammate who QCs work. The account owner does QC daily, so these are not
   needed.

D. **The manager's automation agents, four named clients** – anything they
   create about those four clients. Every type counts: added cards,
   assignments, comments, mentions. For each client the newest one is left
   unread so it is visible that something was posted.

E. **The QC teammate's @mentions that are QC reports** – cleared when the
   comment reports that work was QC'd / checked / approved and asks nothing.
   Kept unread when there is a question or a decision for the account owner.
   If unsure, kept.

## What is never cleared

- `Assigned you:` from anyone other than the manager's agents, or from them
  about any other client.
- Comments and @mentions from anyone else.
- Anything not listed in A to E.

## Settings this depends on

- Basecamp connector connected at claude.ai → Customize → Connectors.
- Connector tool permissions: **Mark As Read** set to "Always allow".
- Session mode: Auto.

## Known limits

- The connector only sees the 100 newest unread notifications. Older ones are
  reached only as newer ones get read; each run repeats up to 4 passes.
- Notifications cannot be marked unread again through the connector.
- Phone pop-ups and Basecamp's own notification settings cannot be changed by
  Claude; those are set in the Basecamp app or the phone's settings.

## Changing it

Tell Claude in that conversation, for example "also clear X", "stop clearing
Y" or "change the time to Z". Rule changes are made to the evening task and
the later runs pick them up automatically.
