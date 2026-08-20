---
name: linear
description: Read this before any Linear write, and whenever work starts, stops, changes status, gets blocked, or switches to something else. Covers Cattlytx team IDs, the status model, assignee rules, how to write a context-switch state note, PR linking, labels, and the search-before-create rule. Use it for creating issues, updating status, commenting, closing, or folding a pile of new context (a call transcript, site-visit notes) into the board.
---

# Linear at Cattlytx

The reflex rules live in `CLAUDE.md` and are always loaded. This file is the mechanics.
Read it once per session before your first write.

## Why this exists

Someone new, or Jeff, should be able to open Linear and know what is being worked on,
by whom, in what state, and what is left, without asking anyone. Today that is
impossible: of 287 issues, one is In Progress, and 136 open issues have not been
touched in over a month. Two people hold the real state in their heads.

The test at the end of a working session: **if your human vanished right now, could
someone else pick up exactly where they left off from Linear alone?** If not, you are
not done.

## Auth

Your human mints a personal API key at <https://linear.app/settings/api> and sets it as
`LINEAR_API_KEY`. Never use anyone else's key. Never commit it.

Use either the **Linear MCP server** or the GraphQL API at
`https://api.linear.app/graphql` with header `Authorization: <key>` — no `Bearer`
prefix. Pick one and stay consistent within a session.

## Teams

| Team | ID | Use for |
|---|---|---|
| **CAT** (Cattlytx) | `812b0ff0-d872-41f5-ab38-060a21a6bea6` | All real work: features, bugs, infra, customer commitments |
| **PI** (Product Intel) | `75e2cede-e519-45fc-935b-40cb2e44ea05` | Owned by the Product Intel agent. **Do not create issues here.** |

## Status

`Backlog`, `Todo`, `In Progress`, `In Review`, `Done`, `Canceled`, `Duplicate`.

**In Progress means a human is actively on it today.** Not this sprint, today. That
single definition is what makes the board readable; if In Progress comes to mean
"started at some point," the board is worthless again.

`In Review` when a PR is open. `Done` when it merges. `Canceled` with a one-line reason
when abandoned. Nothing sits In Progress that nobody is touching.

**Assignee means who is actually doing the work** — not a queue, not a default. Do not
assign to Jeff unless Jeff is doing it. You will find older issues assigned to Jeff
with `owner:*` labels from a previous convention; leave them alone, do not copy it.

## The context-switch state note

This is the highest-value thing you write, because it is the context that currently
exists only inside someone's head. When your human moves off unfinished work, before
you touch the new thing, comment:

    **[Amanda's agent]**
    Paused here.

    - Works: pen list renders, filters apply, pagination correct
    - Half done: CSV export writes headers but not rows, ~60%
    - Broken/untested: nothing tested against Nodaway data
    - Code: branch amanda/pen-export, no PR yet, 3 uncommitted files
    - Next step: wire the row serializer, then test with a Nodaway tenant

Then set status honestly — back to `Todo`; if blocked, add the `blocked` label and
state the reason, unless they are returning to it within the day.

**Write it for a stranger, not for your human.** They already know. It is for whoever
picks this up in three weeks, quite possibly your human after they have forgotten.

## Volume: post constantly, keep each post small

The frequency is the point, not the length.

**Cheap and constant** — status changes, assignee changes, state notes, links. Never
skip one to avoid noise.

**Selective** — prose commentary. A comment should carry a fact: a cause with its
evidence, a decision and what was rejected, a blocker and what would clear it, a
discovery that changes the work. Not narration of effort. "Working on this" tells a
reader nothing; "auth works, token refresh untested, branch is amanda/token-refresh"
tells them everything.

When unsure whether something is worth writing, **write it**. Under-reporting is the
failure this system exists to fix. Over-reporting we can tune later.

## Things that are not code

A customer call, a decision made in Slack, a constraint someone mentioned in passing,
context from a site visit. If it changes what should be built or in what order, it goes
on the relevant ticket as a comment, or becomes a new ticket if none fits.

## Bulk updates are expected

When your human hands you a pile of new context — a visit transcript, a call recording,
a page of notes — do the full sweep without being asked: create what is missing, update
what changed, close what is done, comment the context onto the right issues. This is the
point of the system, not an overreach.

**What is not allowed is reorganizing on your own initiative.** Do not restructure,
relabel, or mass-close because the board looks untidy to you. Bulk work follows new
information, never tidiness.

## Link the ticket to the PR, always

Put the Linear identifier in the **branch name** (`cat-123-short-slug`) and in the **PR
title**. If the GitHub integration is connected this auto-links; do not rely on that
alone, also post the PR URL as a comment on the issue so the link exists either way.
Same in reverse: opening a PR for existing work means commenting the URL on the ticket.

## Search before creating

287 issues already exist with a long tail of near-duplicates. Search open issues by
keyword and read the top matches first. If something close exists, comment on it
instead. **Duplicates are worse than silence** — they split the record of one problem
across two places.

## Causes need evidence

If you state why something broke, cite it: a log line, a stack trace, a reproduction, a
commit. With no evidence, write the symptom and say "cause unknown" or "timing suggests
X, unconfirmed". A confident wrong cause is worse than none, because it stops other
people looking.

## Do not reopen without post-fix evidence

Before calling something a regression, **check the merge date of the fix that closed it
and confirm your occurrences are after that date.** The Product Intel agent spent two
days reopening already-fixed tickets by counting occurrences in a window that still
contained pre-fix events. Do not repeat that.

## Labels — use these, do not invent

| Group | Labels |
|---|---|
| Type | `Bug`, `Feature`, `Improvement`, `regression`, `observation` |
| Area | `backend`, `frontend`, `data` |
| Source | `agent-filed` (put this on everything you create), `human-filed`, `src:amanda` |
| State | `blocked`, `unverified`, `blocked:darr-input`, `darr-input-received` |
| Customer | `prospect:darr`, `prospect:bimeda`, `prospect:herddogg`, `prospect:midwest`, `prospect:vitafirm-alltech`, and the rest of the `prospect:*` set |
| Business | `type:revenue`, `type:product`, `type:expense-discipline`, `type:investment` |

## Do not

- Modify or close issues assigned to someone else. Comment instead.
- Create issues in the PI team.
- Delete anything.
- Invent labels.

## Expect it to be rough

The first couple of weeks will be noisy and you will get some of this wrong. Prefer
writing the update and being slightly wrong over skipping it, with one exception:
**never state a cause you cannot evidence.**
