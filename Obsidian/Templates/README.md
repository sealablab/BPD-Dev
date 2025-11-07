# Templates

**Purpose:** Templater templates for creating consistent Obsidian notes

---

## Available Templates

### 1. `handoff.md`
**Purpose:** Session handoff notes for multi-session work

**Use when:**
- Session ends mid-task
- Need to preserve complex context
- Blocked on decision/input

**Creates:**
- Context section (what was done)
- Next steps with `@claude` routing
- Blockers with `@human` routing
- Files/resources/success criteria

**Output location:** `Obsidian/Project/Handoffs/`

---

### 2. `prompt.md`
**Purpose:** Reusable prompt library entries

**Use when:**
- Found useful analysis pattern
- Want to standardize workflow
- Creating repeatable operation

**Creates:**
- Purpose statement
- Prompt text (copy/paste ready)
- Usage notes and examples
- Related files

**Output location:** `Obsidian/Project/Prompts/`

---

### 3. `task.md`
**Purpose:** Task tracking with agent/human delegation

**Use when:**
- Planning multi-step work
- Coordinating agent and human actions
- Tracking discrete tasks

**Creates:**
- Task description
- Action items (`@claude` and `@human`)
- Context and success criteria
- Related files

**Output location:** Anywhere in `Obsidian/Project/`

---

## Using Templates

### In Obsidian (Recommended)

1. **Create new note** in appropriate directory
   - Handoffs: `Obsidian/Project/Handoffs/2025-11-06-1500-topic.md`
   - Prompts: `Obsidian/Project/Prompts/analyze-topic.md`
   - Tasks: `Obsidian/Project/task-topic.md`

2. **Insert template**
   - Command Palette: `Cmd/Ctrl+P`
   - Type: `Templater: Insert Template`
   - Choose template

3. **Fill placeholders**
   - Press `Tab` to jump between cursor positions
   - Fill in each `<% tp.file.cursor(N) %>` placeholder

4. **Save** - Template variables will populate

---

## Template Syntax

These templates use **Templater plugin** syntax:

### Date/Time
- `<% tp.date.now("YYYY-MM-DD") %>` - Current date (ISO 8601)
- `<% tp.date.now("YYYY-MM-DD HH:mm") %>` - Date and time

### Cursors
- `<% tp.file.cursor(1) %>` - Jump to position 1
- Press `Tab` to move to next cursor position

### Frontmatter
```yaml
---
created: <% tp.date.now("YYYY-MM-DD") %>
type: handoff
---
```

**Note:** No JavaScript used - simple Templater syntax only

---

## Configuring Templater

**Check plugin settings:**
1. Settings → Templater
2. Template folder location: `Obsidian/Templates`
3. Trigger Templater on new file creation: Enabled (optional)
4. Enable folder templates: Enabled (optional)

**Folder templates (optional):**
- Set `Obsidian/Project/Handoffs/` → `handoff.md`
- Set `Obsidian/Project/Prompts/` → `prompt.md`

---

## Frontmatter Fields

All templates use consistent frontmatter:

### Common Fields
- `created` - Creation date (YYYY-MM-DD)
- `type` - Note type (handoff/prompt/task)

### Type-Specific
- **Handoff:** `status` (active/complete)
- **Task:** `status` (open/in-progress/complete), `priority` (high/medium/low)

**Used for:**
- Dataview queries (if plugin installed)
- Filtering/searching
- Metadata tracking

---

## Customization

### Adding New Templates
1. Create `.md` file in `Obsidian/Templates/`
2. Use Templater syntax: `<% tp.date.now() %>`, `<% tp.file.cursor(N) %>`
3. Add frontmatter with `created` and `type`
4. Document in this README

### Modifying Templates
1. Edit template file directly
2. Changes apply to new notes only (existing notes unchanged)
3. Update this README if structure changes

---

## Related Documentation

- [Templater Plugin Docs](https://silentvoid13.github.io/Templater/)
- [[Obsidian/Project/README]] - Project workspace overview
- [[Obsidian/Project/Handoffs/README]] - Handoff conventions
- [[Obsidian/Project/Prompts/README]] - Prompt library guide

---

**Created:** 2025-11-06
**Last Updated:** 2025-11-06