# Handoffs

**Purpose:** Session continuation notes for work that spans multiple Claude sessions

---

## What Are Handoffs?

Handoff notes capture context when:
- Session ends mid-task (work incomplete)
- Complex work requires multiple sessions
- Need to preserve decision context
- Blocked on human input or external dependency

**Key principle:** Handoffs are **ephemeral** - delete after work is committed to git. Git history is the permanent record.

---

## Naming Convention

**Format:** `YYYY-MM-DD-HHMM-<brief-description>.md`

**Examples:**
- `2025-11-06-1430-voltage-type-refactor.md`
- `2025-11-06-1745-fsm-observer-debug.md`
- `2025-11-07-0900-register-mapping-design.md`

**Why this format:**
- `YYYY-MM-DD-HHMM` - Sorts chronologically, unique identifier
- `<brief-description>` - Quick topic identification
- `.md` - Markdown format

---

## When to Create

**DO create handoff when:**
- ✅ Session ending with incomplete work
- ✅ Multi-step task needing continuation
- ✅ Complex context that's hard to recreate
- ✅ Blocked on decision/input

**DON'T create handoff when:**
- ❌ Work completed and committed
- ❌ Simple task (can restart from scratch easily)
- ❌ Already documented in git commit message

---

## Template Usage

**Using Templater in Obsidian:**
1. Create new file: `2025-11-06-1500-topic.md`
2. Command palette: "Templater: Insert Template"
3. Choose: `handoff.md`
4. Fill in placeholders
5. Use `@claude` to indicate continuation needed

**See:** [[Obsidian/Templates/README|Templates README]]

---

## Lifecycle

```
1. Create handoff
   ↓
2. Commit to git (if mid-work)
   ↓
3. Next session reads handoff
   ↓
4. Work continues
   ↓
5. Work completed & committed to git
   ↓
6. Delete handoff (history now in git)
```

---

## What to Include

**Essential sections:**
- **What was done** - Completed work this session
- **What's next** - Specific next steps with `@claude`
- **Blockers** - Issues/decisions with `@human` if needed
- **Files modified** - Wikilinks to relevant files
- **Context** - Resources, commands, external references

**See template for full structure:** [[Obsidian/Templates/handoff.md]]

---

## Finding Handoffs

```bash
# List all handoffs (newest first)
ls -lt Obsidian/Project/Handoffs/

# Find handoffs needing Claude action
grep -l "@claude" Obsidian/Project/Handoffs/*.md

# Find handoffs needing human input
grep -l "@human" Obsidian/Project/Handoffs/*.md

# Search by topic
grep -l "voltage" Obsidian/Project/Handoffs/*.md
```

---

## Cleanup Strategy

**When to delete:**
- Work committed to git (history preserved)
- Context no longer relevant
- Replaced by new handoff

**Command:**
```bash
# After committing work
rm Obsidian/Project/Handoffs/2025-11-06-1500-completed-task.md
git add -u
git commit -m "docs: Clean up completed handoff"
```

**Keep if:**
- Work still in progress
- Reference for similar future work
- Contains important decision context

---

## Related Documentation

- [[Obsidian/Project/README]] - Full system overview
- [[Obsidian/Templates/handoff.md]] - Handoff template
- [[.claude/handoffs/README.md]] - Historical examples (different system)

---

**Created:** 2025-11-06
**Last Updated:** 2025-11-06