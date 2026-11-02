# Guide 01: Getting Started

This guide walks you through bootstrapping a new application from this boilerplate repository.

---

## 1. Prerequisites Check

Before starting, confirm your development environment has the necessary tooling:

```bash
# Verify Git
git --version

# Verify GitHub CLI
gh --version
gh auth status
```

* If `gh` is not installed:
  * **Windows**: `winget install GitHub.cli`
  * **macOS**: `brew install gh`
  * **Linux**: `sudo apt install gh`
* If `gh` is not logged in, run:
  ```bash
  gh auth login
  ```

---

## 2. Creating a New Project From This Template

### Step A: Clone the Repository
Clone this repository to your target project folder:

```bash
git clone https://github.com/TheGreatL/Turbo-Monorepo.git my-new-project
cd my-new-project
```

### Step B: Point to Your New Remote Repository
Detach from the boilerplate remote and point to your newly created GitHub repository:

```bash
# Remove or rename boilerplate origin
git remote set-url origin https://github.com/<your-username>/<your-new-repo>.git

# Verify remote
git remote -v
```

---

## 3. Initializing Agent Skills & Issue Tracker

Inside your AI agent environment (Antigravity, Claude Code, Cursor, etc.), run:

```text
/setup-matt-pocock-skills
```

This interactive setup will:
1. Detect your new repository URL.
2. Create the 5 canonical triage labels (`needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`) directly on your new GitHub Issues board.
3. Update `docs/agents/issue-tracker.md`, `AGENTS.md`, and `CLAUDE.md` to point to your new project board.

---

## 4. Next Step

Now that your project is initialized, proceed to:
* **[Guide 02: Monorepo Structure](./02-monorepo-structure.md)** to plan your packages and applications.
* Or type `/ask-matt` in chat to begin designing your architecture!
