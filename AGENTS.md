## Linear

Linear is the true record of all work at Cattlytx. Keeping it true is your job, not
your human's. Their workflow does not change; yours does.

- **Anything that happens goes to Linear the same session.** Work started, work
  stopped, status changed, something learned, something broken, something fixed.
- **Never ask permission to write to Linear.** Not "should I make a ticket?", not
  "want me to close this?". Do it, then say so in one line at the end of your reply.
- **Work with no ticket: create it when work STARTS**, not when it finishes. Set it
  In Progress, assign your human, comment one line on what prompted it.
- **Something merely mentioned as needing doing is a Backlog ticket now.** Linear
  should hold everything we could be working on, not only what is in flight.
- **Switching tasks: write the state of the old thing before you touch the new one.**
  What works, what is half built, what is broken, the branch, and what the next step
  was going to be. Then set its status honestly and move the new thing to In Progress.
- **Before your human starts something, check whether someone else is already on it.**
  If Linear says so, tell them before they begin.
- **Every comment opens with `**[<your human>'s agent]**`** on its own line. Replace
  `<your human>` with the name of the person whose personal API key is active (for
  example, `**[Garrett's agent]**` or `**[Amanda's agent]**`). Without the tag there
  is no way to distinguish the agent's writing from the human's.
- **Never state a cause you cannot evidence.** Cite the log line, trace, or commit, or
  write "cause unknown".

**Before your first Linear write in a session, read `.claude/skills/linear/SKILL.md`**
for team IDs, the status model, labels, PR linking, the context-switch state note format
and the rest of the mechanics. Claude Code loads it automatically as a skill. Codex should
open it with a file read. Either way, read it before you write, not after.
