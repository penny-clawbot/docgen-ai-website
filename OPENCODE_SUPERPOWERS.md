# OpenCode Superpowers Installation Guide

## Overview

**Superpowers** is a collection of AI-powered development skills and workflows for [OpenCode.ai](https://opencode.ai). It provides structured methodologies for brainstorming, debugging, code review, TDD, and more.

## Installation

### Quick Install (macOS/Linux)

```bash
# Clone repository
if [ -d ~/.config/opencode/superpowers ]; then
  cd ~/.config/opencode/superpowers && git pull
else
  git clone https://github.com/obra/superpowers.git ~/.config/opencode/superpowers
fi

# Create directories
mkdir -p ~/.config/opencode/plugins ~/.config/opencode/skills

# Create symlinks
ln -s ~/.config/opencode/superpowers/.opencode/plugins/superpowers.js ~/.config/opencode/plugins/superpowers.js
ln -s ~/.config/opencode/superpowers/skills ~/.config/opencode/skills/superpowers

# Restart OpenCode
```

### Quick Install (Windows - PowerShell)

```powershell
# Clone repository
git clone https://github.com/obra/superpowers.git "$env:USERPROFILE\.config\opencode\superpowers"

# Create directories
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.config\opencode\plugins"
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.config\opencode\skills"

# Create plugin symlink (requires Developer Mode or Admin)
New-Item -ItemType SymbolicLink -Path "$env:USERPROFILE\.config\opencode\plugins\superpowers.js" -Target "$env:USERPROFILE\.config\opencode\superpowers\.opencode\plugins\superpowers.js"

# Create skills junction (works without special privileges)
New-Item -ItemType Junction -Path "$env:USERPROFILE\.config\opencode\skills\superpowers" -Target "$env:USERPROFILE\.config\opencode\superpowers\skills"

# Restart OpenCode
```

## Verification

### Check Installation (macOS/Linux)

```bash
ls -l ~/.config/opencode/plugins/superpowers.js
ls -l ~/.config/opencode/skills/superpowers
```

Both should show symlinks pointing to superpowers directory.

### Check Installation (Windows - PowerShell)

```powershell
Get-ChildItem "$env:USERPROFILE\.config\opencode\plugins" | Where-Object { $_.LinkType }
Get-ChildItem "$env:USERPROFILE\.config\opencode\skills" | Where-Object { $_.LinkType }
```

Look for `<SYMLINK>` or `<JUNCTION>` in output.

### Check Plugin Loading

```bash
# View OpenCode logs for superpowers
opencode run --print-logs "test" 2>&1 | grep -i superpowers
```

Should see plugin loading message.

## Available Skills

### Using Superpowers (Bootstrap)
- **Path:** `using-superpowers`
- **Purpose:** Establishes skill usage workflow
- **Auto-loads:** Injected into every conversation
- **When to use:** Always loaded automatically

### Process Skills

1. **Brainstorming**
   - When to use: Starting any new feature or complex task
   - Purpose: Systematic exploration of options
   - Output: Structured brainstorming with categories

2. **Systematic Debugging**
   - When to use: Any bug or unexpected behavior
   - Purpose: Methodical debugging workflow
   - Output: Debugging strategy and execution

3. **Test-Driven Development**
   - When to use: Writing tests-first code
   - Purpose: TDD methodology
   - Output: Test planning and implementation

4. **Dispatching Parallel Agents**
   - When to use: Multiple independent tasks
   - Purpose: Parallel execution via subagents
   - Output: Coordinated multi-agent workflow

### Implementation Skills

5. **Subagent-Driven Development**
   - When to use: Building features with specialized agents
   - Purpose: Structured agent delegation
   - Output: Agent coordination and integration

6. **Writing Plans**
   - When to use: Documenting development approach
   - Purpose: Clear implementation roadmap
   - Output: Structured development plan

7. **Executing Plans**
   - When to use: Following a written plan
   - Purpose: Plan execution and tracking
   - Output: Progress tracking and completion

8. **Using Git Worktrees**
   - When to use: Working on multiple branches simultaneously
   - Purpose: Efficient parallel development
   - Output: Worktree setup and management

### Review Skills

9. **Requesting Code Review**
   - When to use: Need peer feedback on code
   - Purpose: Get external review
   - Output: Code review request

10. **Receiving Code Review**
    - When to use: Reviewing someone else's code
    - Purpose: Provide structured feedback
    - Output: Review findings and suggestions

11. **Verification Before Completion**
    - When to use: Finishing a development branch
    - Purpose: Ensure quality before merge
    - Output: Checklist and validation

12. **Finishing a Development Branch**
    - When to use: Ready to merge feature branch
    - Purpose: Clean branch completion
    - Output: Merge preparation and cleanup

### Other Skills

13. **Writing Skills**
    - When to use: Creating custom skills
    - Purpose: Skill authoring guidelines
    - Output: Skill structure and best practices

## Usage

### List All Skills

```bash
opencode run "use skill tool to list all skills"
```

### Load a Specific Skill

```bash
opencode run "use skill tool to load superpowers/brainstorming"
```

### Available Skill Names

- `superpowers/using-superpowers` - Bootstrap (auto-loaded)
- `superpowers/brainstorming` - Brainstorming workflow
- `superpowers/systematic-debugging` - Debugging methodology
- `superpowers/test-driven-development` - TDD workflow
- `superpowers/dispatching-parallel-agents` - Parallel agents
- `superpowers/subagent-driven-development` - Agent development
- `superpowers/writing-plans` - Plan writing
- `superpowers/executing-plans` - Plan execution
- `superpowers/using-git-worktrees` - Git worktrees
- `superpowers/requesting-code-review` - Request review
- `superpowers/receiving-code-review` - Give review
- `superpowers/verification-before-completion` - Pre-merge checklist
- `superpowers/finishing-a-development-branch` - Branch completion
- `superpowers/writing-skills` - Create skills

## Skill Priority Order

When multiple skills could apply, use this order:

1. **Process skills first** (brainstorming, debugging, TDD)
   - These determine HOW to approach the task
   - Must be invoked before implementation

2. **Implementation skills second** (agent development, writing plans)
   - These guide execution based on process output
   - Build on process skill results

**Example:**
- "Build a new feature" → Use `brainstorming` first, then `subagent-driven-development`
- "Fix this bug" → Use `systematic-debugging`
- "Write tests" → Use `test-driven-development`

## Skill Categories

### Rigid Skills (Follow Exactly)
- `test-driven-development`
- `systematic-debugging`

These skills have strict workflows. Follow them exactly without deviation.

### Flexible Skills (Adapt to Context)
- `brainstorming`
- `subagent-driven-development`
- `writing-plans`

These skills provide frameworks that adapt to your specific situation.

## The "Red Flags" of Skill Evasion

Avoid these thoughts - they mean you're rationalizing not using a skill:

| Thought | Reality |
|---------|---------|
| "This is just a simple question" | Questions are tasks. Check for skills. |
| "I need more context first" | Skill check comes BEFORE gathering. |
| "Let me explore the codebase first" | Skills tell you HOW to explore. Check first. |
| "I can check git/files quickly" | Files lack conversation context. Check for skills. |
| "This doesn't need a formal skill" | If a skill exists, use it. |
| "I remember this skill" | Skills evolve. Read current version. |

## Troubleshooting

### Plugin Not Loading

1. Check plugin exists:
   ```bash
   ls ~/.config/opencode/superpowers/.opencode/plugins/superpowers.js
   ```

2. Check symlink:
   ```bash
   ls -l ~/.config/opencode/plugins/
   ```

3. Check OpenCode logs:
   ```bash
   opencode run --print-logs "test" 2>&1 | grep -i plugin
   ```

### Skills Not Found

1. Verify skills symlink:
   ```bash
   ls -l ~/.config/opencode/skills/superpowers
   ```
   Should point to `superpowers/skills/`

2. List available skills:
   ```bash
   opencode run "use skill tool to list all skills"
   ```

3. Check skill structure:
   ```bash
   ls ~/.config/opencode/superpowers/skills/
   ```
   Each skill needs a `SKILL.md` file with valid YAML frontmatter.

### Windows: Symlink Privileges Error

**Error:** "You do not have sufficient privilege"

**Solution 1:** Enable Developer Mode
- Windows 10: Settings → Update & Security → For developers
- Windows 11: Settings → System → For developers

**Solution 2:** Run as Administrator
- Right-click PowerShell → "Run as Administrator"

**Solution 3:** Use Junctions
```powershell
# Use junctions instead of symlinks (doesn't require privileges)
New-Item -ItemType Junction -Path "target" -Target "source"
```

### Git Bash Symlinks Not Working

**Problem:** Git Bash's `ln` command copies files instead of creating symlinks.

**Solution:** Use `cmd //c mklink`:
```bash
cmd //c "mklink \"path\" \"target\""
```

### Bootstrap Not Appearing

1. Verify using-superpowers skill exists:
   ```bash
   ls ~/.config/opencode/superpowers/skills/using-superpowers/SKILL.md
   ```

2. Check OpenCode version supports hooks:
   ```bash
   opencode --version
   ```

3. Restart OpenCode after plugin changes:
   - Full quit and restart required

## Updating

```bash
cd ~/.config/opencode/superpowers
git pull
```

Restart OpenCode to load updates.

## Uninstallation

```bash
# Remove symlinks
rm ~/.config/opencode/plugins/superpowers.js
rm ~/.config/opencode/skills/superpowers

# Remove repository (optional)
rm -rf ~/.config/opencode/superpowers

# Restart OpenCode
```

## Support

- **Issues:** https://github.com/obra/superpowers/issues
- **Documentation:** https://github.com/obra/superpowers
- **OpenCode Docs:** https://opencode.ai/docs/

## Advanced: Creating Custom Skills

### Personal Skills

```bash
mkdir -p ~/.config/opencode/skills/my-skill
```

Create `~/.config/opencode/skills/my-skill/SKILL.md`:
```markdown
---
name: my-skill
description: Use when [condition] - [what it does]
---

# My Skill

[Your skill content here]
```

### Project Skills

```bash
# In your OpenCode project
mkdir -p .opencode/skills/my-project-skill
```

Create `.opencode/skills/my-project-skill/SKILL.md`:
```markdown
---
name: my-project-skill
description: Use when [condition] - [what it does]
---

# My Project Skill

[Your skill content here]
```

### Skill Locations (Priority Order)

1. **Project skills** (`.opencode/skills/`) - Highest priority
2. **Personal skills** (`~/.config/opencode/skills/`)
3. **Superpowers skills** (`~/.config/opencode/skills/superpowers/`)

---

**Last Updated:** February 23, 2026
**Version:** 1.0.0
**Status:** Installed and tested on macOS
