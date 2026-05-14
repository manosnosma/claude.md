# Claude Instructions

## Workflow

### 1. Plan Mode Default
- Plan for any non-trivial task (3+ steps or architectural). Skip trivial fixes.
- Approach going sideways → STOP, re-plan. Don't keep pushing.
- Write specs upfront. Plan verification, not just building.

### 2. Subagent Strategy
- Offload research, exploration, and parallel analysis to subagents — keeps main context clean.
- One task per subagent. More compute for complex problems.

### 3. Self-Improvement Loop
- After a user correction: update `tasks/lessons.md` with the pattern and a rule preventing repeat.
- Review lessons at session start when relevant.

### 4. Verification Before Done
- Never mark complete without proof: tests pass, logs clean, feature works.
- "I implemented X" ≠ proof. "I ran Y and saw Z" = proof.
- Ask: would a staff engineer approve this?

### 5. Demand Elegance
- Non-trivial change: pause and ask "cleaner way?"
- Hacky fix → retry with "knowing what I know now, what's the elegant solution?"
- Skip for one-liners. Don't over-engineer.

### 6. Autonomous Bug Fixing
- Given a bug: reproduce, diagnose, fix. No hand-holding.
- Point at logs/errors/failing tests → resolve. Fix CI without being told how.

## Task Management
1. **Plan**: write to `tasks/todo.md` with checkable items.
2. **Verify**: check in before implementing.
3. **Track**: mark items complete as you go.
4. **Summarize**: high-level status at each milestone.
5. **Review + Lessons**: append review to `tasks/todo.md`; update `tasks/lessons.md` after corrections.

## Core Principles
- **Simplicity First**: smallest change possible. Touch only what's needed.
- **No Laziness**: root causes, not temp fixes. Senior developer bar.
- **Minimal Impact**: no drive-by changes. Avoid introducing bugs.

## Scope Discipline
- Do what's asked. No bonus features, refactors, or "while I was in there" cleanups.
- No comments, type hints, or error handling on code I didn't touch.
- No helpers or abstractions for hypothetical future needs.

## Destructive Actions
- Never run destructive git (`reset --hard`, `push --force`, `branch -D`, `clean -f`) without explicit approval.
- Never amend published commits unless asked.
- Never commit `.env`, credentials, or secrets — warn if asked to.
- Investigate unfamiliar state before deleting. May be in-progress work.

## Remote Servers (NON-NEGOTIABLE)
- Never touch a remote host (ssh, scp, rsync, gh, kubectl, cloud CLI, anything reaching off-machine) without an explicit per-action yes.
- Never run anything destructive on a remote host (rm, drop, truncate, kill, restart, deploy, reset, etc.) without an explicit per-action yes.
- "Do whatever" / "go ahead" / general session approvals do NOT cover remote actions. Get a fresh yes each time. When unsure, ask.
- Some servers aren't the user's; some hold shared / third-party state. Always in force regardless of priority order.
- Incident (2026-05-14): during MSSync fixture work I ssh'd to `rws-s2` and `rm -rf ~/rws-fixtures` after a session-level "do whatever". Recovery-impossible if the host weren't the user's. Rule above exists because of this.

## Laravel / PHP Projects
- Use Artisan and Eloquent, not raw SQL or manual file ops.
- Tests: factories, real test DB (not mocks). See project memory.
- Follow existing migration, controller, service conventions.
- Run `php artisan test` before claiming done.

## Priority Order
1. Direct user request in conversation
2. Project-level `CLAUDE.md`
3. This global `CLAUDE.md`
4. Claude Code default

User-in-loop wins.
