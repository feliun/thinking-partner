---
type: reference
status: active
tags: [context, skill, thinking-partner, config, manifest]
---
# Skill: Manifest Resolver

Purpose:
Resolve config file paths for the thinking-partner plugin before command execution by reading the manifest.yaml registry.

When to use:
- Before any `thinking-partner:*` command that needs config files
- Standalone for debugging config resolution (`Invoke manifest-resolver for domain: thinking-partner`)

---

## Context

The thinking-partner plugin reads a central manifest (`commands/manifest.yaml`) to resolve config paths. This means config files can live anywhere — the user's Obsidian vault, the plugin's bundled samples, `~/.claude/thinking-partner/`, or any future location — without modifying plugin code.

## Algorithm

1. **Read** `commands/manifest.yaml`
2. **Select the domain** from the calling command's namespace (e.g., `thinking-partner:challenge` → domain `thinking-partner`)
3. **For each config key** in that domain:
   a. Iterate through the `paths` array in order
   b. **Expand path tokens:**
      - `$WORKSPACE` → the user's primary working directory (where Claude Code is running, shown in the environment context as "Primary working directory")
      - `~` → the user's home directory
      - Bare relative paths → resolve against the plugin's own root directory
   c. **Check existence:**
      - For `format: directory` → check the directory exists AND contains at least one file matching the expected pattern (e.g., `.md` for note directories)
      - For `format: yaml` or `format: markdown` → check the file exists and is readable
   d. **Return the first match** as the resolved path
   e. If no path matches and `required: true` → flag as ❌ with fix instructions
   f. If no path matches and `required: false` → flag as ⚠️ optional, skip

## Output

After resolution, emit a compact status block that the calling command can reference:

```
Config resolution (thinking-partner):
  ✅ vault             → /Users/name/my-vault
  ✅ thinking-style    → references/thinking-style.md
  ✅ values            → references/values.md
  ⚠️ weekly-reviews   → not found (optional, skipping)
```

If ALL configs resolve successfully, collapse to a single line:
```
Config: all resolved (N/N keys)
```

## Error Handling

- If `manifest.yaml` itself is missing → report error and abort the calling command
- If a required config is missing from all paths → report ❌ with fix instructions
- Never hard-fail the entire command over a missing optional config
- Always continue to the calling command with whatever was resolved

## Standalone Usage

To debug config resolution without running a full command:

```
Invoke manifest-resolver for domain: thinking-partner
```

This prints the full resolution table without delegating to any command.

---

## Anti-patterns

- Do NOT hard-fail the entire command over a missing optional config — continue with whatever was resolved
- Do NOT bypass the manifest by hardcoding config paths — always resolve through manifest.yaml
- Do NOT skip checking directory contents for `format: directory` configs — an empty directory is different from a missing one
