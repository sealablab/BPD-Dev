---
created: <% tp.date.now("YYYY-MM-DD") %>
type: handoff
---

# Handoff: <% tp.file.cursor(1) %>

**Date:** <% tp.date.now("YYYY-MM-DD HH:mm") %>
**Session:** <% tp.file.cursor(2) %>

---

## Context: What I Just Did

<% tp.file.cursor(3) %>

---

## Next Steps

@claude please continue by:
1. <% tp.file.cursor(4) %>

---

## Blockers

@human <% tp.file.cursor(5) %>

---

## Files Modified

- [[<% tp.file.cursor(6) %>]]

---

## Resources

**Documentation:**
- [[<% tp.file.cursor(7) %>]]

**Commands:**
```bash
<% tp.file.cursor(8) %>
```

---

## Success Criteria

- [ ] <% tp.file.cursor(9) %>

---

**Created:** <% tp.date.now("YYYY-MM-DD HH:mm") %>
**Status:** Active
