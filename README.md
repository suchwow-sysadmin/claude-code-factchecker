# 🐾 Claude Code Factchecker

> Plug in a live MCP server like [Hyperbrowser] (https://www.hyperbrowser.ai/)
> for nuanced, context-sensitive, AI-powered fact-checking that doesn’t just
> check a link—**it browses, crawls, clicks, and understands.**

> **Skip to [Easy Mode](#easy-mode-no-mcp-server) below if you're not familiar
> with MCP! (Manual review of Claude-provided URLs strongly advised.)**

> This is not an app. It is a folder of instructions Claude reads. Read more
> here on Claude [_skills_](https://claude.com/blog/skills).

---

## 🚀 For Technical Users & Early Adopters (MCP Server Required)

- **Magic Mode:** Claude + MCP = automated, multi-step, contextual
  fact-checking.
- Requires:
  - MCP server (tested with Hyperbrowser via Docker Desktop)
  - Strong opinions regarding terminal applications
- Features:

  - Follows links, clicks through, verifies in real-time.
  - Context-aware suggestions (not just “true/false”).
  - Modular—bring your own agentic browsing stack.

- [**Set up and run Magic Mode**](#magic-mode-mcp-setup)

---

## 📝 For Journalists, Writers, and General Valuers of Facts Wishing to Avoid MCP Servers

**Jump to:**
[👉 Easy Mode Instructions (for Non-Technical Users)](#easy-mode-no-mcp-server)

---

# [Easy Mode (No MCP Server)](#easy-mode-no-mcp-server)

- No MCP, no automation.
- Just Claude + your terminal.
- Still lets you check sources, catch errors, and get context—but you’ll need to
  review URLs manually.

**Claude Code can directly assist you with installing, connecting, and
understanding MCP servers. Just ask!**

---

## Demo Files

- [bad_Ai_essay.md](./Bad_Ai_Essay.md)

## What You Need (Check These First)

- Anthropic Claude subscription ($20/month) - [Sign up](https://claude.ai/)
- A terminal (typing window). These steps use the free Warp Terminal
  ([download](https://www.warp.dev/)).
- This fact-checker folder, unzipped, on your Desktop
- Your draft file to check (put it in the same folder)

---

## Step 1: Get the Folder

1. On this GitHub page, click the green **Code** button.
2. Click **Download ZIP**.
3. Open your Downloads folder. Double-click the ZIP to unzip it.
4. Drag `fact-checker-skill-test-main` onto your **Desktop**.

Did it work? You should see the folder on your Desktop with files like
`README.md` and `.claude`.

### Step 2: Open Warp

- Mac: Press `Cmd + Space`, type `Warp`, press Enter.
- Windows: Open the Start menu, type `Warp`, click it.

Did it work? Warp shows a dark window with a blinking cursor.

### Step 3: Point Warp at the Folder

1. In Warp, type `cd ` (type `cd` then a space).
2. Drag the `fact-checker-skill-test-main` folder from your Desktop into Warp.
3. Press Enter.

Did it work? The line before the cursor should end with the folder name. No
error message means success.

### Step 4: Install Claude Code (first time only)

1. Type `claude` and press Enter.
2. If Claude Code is not installed, follow the on-screen steps at
   [claude.ai/code](https://claude.ai/code). If Warp offers to install Node.js
   for you, say yes.
3. If asked to reopen the terminal after install, close Warp, reopen Warp, and
   repeat Step 3 (`cd` into the folder).

Did it work? Typing `claude` now shows a Claude greeting. If you see errors,
visit [claude.ai/code](https://claude.ai/code) and follow the prompts again.

### Step 5: Initialize the Fact-Checker (first time only)

1. With Claude running (you see its greeting), type:

```
/init
```

2. Press Enter.

Did it work? Claude says it scanned the folder and found the fact-checker skill.
You only do `/init` once per folder.

### Step 6: Test Fact-Checking

1. In Claude, say: `Please fact-check bad_AI_essay.md`
2. Claude will read the file and give you a report - with citations!

Did it work? You see a report with ✅ ⚠️ ❌ next to sources and claims.

_Note: Some markdown viewers do not render the report links correctly. Use
Warp's built-in Markdown viewer for best results._

## What It Checks

- ✅ Do your cited sources exist?
- ✅ Do sources say what you claim?
- ✅ Are there factual errors?
- ✅ Are quotes accurate?
- ✅ Are any sources questionable?

---

## Commands You Will Use

| Command/Action                 | What it does                                       |
| ------------------------------ | -------------------------------------------------- |
| `claude`                       | Starts Claude Code in the terminal                 |
| `/init`                        | Scans the folder so Claude learns the fact-checker |
| "Please fact-check [filename]" | Runs the fact-checker on your file                 |
| `/memory`                      | Shows what Claude remembers                        |
| `/help`                        | Shows all commands                                 |
| `/exit` or `Ctrl + C`          | Stops Claude Code                                  |

---

# Demo Session

You: Please fact-check bad_AI_essay.md

Claude: I'll fact-check your draft now.

[Claude reads your file, checks sources, and generates a report]

📋 FACT-CHECK REPORT ━━━━━━━━━━━━━━━━━━━━ ✅ Citation 1: Verified - URL
accessible, quote accurate ⚠️ Citation 2: Warning - Publication date unclear ❌
Citation 3: Error - URL returns 404 (page not found) ...

Video:

---

## Magic Mode MCP Setup

If you want Claude to open web links for you, add an MCP server like
**HyperBrowser**. Setup details are in `CLAUDE.md` under "MCP Server
Configuration."

- With HyperBrowser: Claude can open URLs, read pages, and verify quotes.
- Without it: Claude provides links to check yourself.
- Standards for how these citations are chosen are detailed in @CLAUDE.md Fact
  Checking Workflow>Source Classification.

---

# Disclaimers

- Provided "AS IS" without warranty. This tool helps but does not replace your
  own verification.
- You are responsible for all claims before publication.
- ⚠️ The repo creator flags U.S. federal government data published after January
  2025 as unreliable, due to mass layoffs of federal employees and other
  unprecedented interference. Data before January 2025 is considered usable with
  standard checks.

---

## License

MIT License - Free to use, modify, and share.

**Version**: 1.0 | **Updated**: November 2025 | README audited by Ultra-Doc
https://github.com/justfinethanku/ultra-doc

Need help? Open an issue on GitHub. Pull requests and contributions are welcome.
