# Context Manager Commands

## Export Session Context

**Command:** `contextManager.export`

**Description:** Save current session summary to context repository

**Usage:**
```
Command Palette → "Context Manager: Export Session Context"
```

**Prompts:**
- Session summary (required)

**Output:**
- Creates `session-YYYYMMDD-HHMMSS.md` in `.context/` folder
- Commits and pushes to remote repository

**Example:**
```
Summary: "Implemented JWT authentication with refresh tokens"
→ Creates: .context/session-20241114-143022.md
```

---

## Retrieve Past Context

**Command:** `contextManager.retrieve`

**Description:** Load previous session summaries

**Usage:**
```
Command Palette → "Context Manager: Retrieve Past Context"
```

**Options:**
- Recent (last 3 sessions)
- Search by keyword
- Search by date (YYYYMMDD)

**Output:**
- Displays matching sessions in output panel

**Examples:**
```
Recent → Shows last 3 sessions
Keyword: "auth" → Shows sessions mentioning authentication
Date: 20241114 → Shows sessions from Nov 14, 2024
```

---

## Setup Project

**Command:** `contextManager.setup`

**Description:** Link current project to context repository

**Usage:**
```
Command Palette → "Context Manager: Setup Project"
```

**Prompts:**
- Project name (defaults to current folder name)

**Actions:**
1. Creates directories in context repo
2. Creates `.context` symlink
3. Creates `.secrets` symlink
4. Updates `.gitignore`

**Output:**
```
✓ Project directories created
✓ Symlinks created
✓ .gitignore updated
```

---

## Unlock Repository

**Command:** `contextManager.unlock`

**Description:** Decrypt secrets using 1Password key

**Usage:**
```
Command Palette → "Context Manager: Unlock Repository"
```

**Requirements:**
- 1Password CLI signed in
- Key stored as "ai-agents-context-key" in 1Password

**Output:**
```
✓ Repository unlocked
```

**Note:** Run this once per machine or when repo is locked

---

## Sync Context

**Command:** `contextManager.sync`

**Description:** Push/pull context changes

**Usage:**
```
Command Palette → "Context Manager: Sync Context"
```

**Actions:**
1. Commits local changes
2. Pulls from remote
3. Pushes to remote

**Output:**
```
✓ Context synced
```

---

## Configuration

### contextManager.repositoryPath
- **Type:** string
- **Default:** `~/ai-agents-context`
- **Description:** Path to central context repository

### contextManager.autoRetrieve
- **Type:** boolean
- **Default:** `true`
- **Description:** Automatically load context when starting session

### contextManager.autoExport
- **Type:** boolean
- **Default:** `false`
- **Description:** Automatically save context after session

---

## Keyboard Shortcuts

Add to `keybindings.json`:

```json
[
  {
    "key": "cmd+shift+e",
    "command": "contextManager.export"
  },
  {
    "key": "cmd+shift+r",
    "command": "contextManager.retrieve"
  }
]
```

---

## Workflow

### Daily Usage

1. **Start session:**
   - Open project in Claude Code
   - Auto-retrieves context (if enabled)
   - Or run: `Context Manager: Retrieve Past Context`

2. **Work with Claude:**
   - Claude has context from past sessions
   - Ask questions referencing previous work

3. **End session:**
   - Run: `Context Manager: Export Session Context`
   - Enter summary of accomplishments

### First-Time Setup

1. **Setup project:**
   ```
   Context Manager: Setup Project
   ```

2. **Unlock repository:**
   ```
   Context Manager: Unlock Repository
   ```

3. **Start working:**
   Context is now available for this project

---

## Troubleshooting

### Command not found
- Verify plugin installed correctly
- Restart Claude Code

### Repository locked
- Run: `Context Manager: Unlock Repository`
- Check 1Password CLI: `op whoami`

### Scripts fail
- Verify repo exists: `~/ai-agents-context`
- Check scripts executable: `chmod +x ~/ai-agents-context/scripts/*.sh`

### Sync conflicts
- Pull changes first
- Resolve conflicts manually
- Then run sync again
