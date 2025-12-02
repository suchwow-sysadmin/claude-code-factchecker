# AI Fact-Checker Skill for Claude Code

Simple fact-checking for non-technical writers. Claude reads this folder to
learn how to check your draft.

Ye who doubt; prepare to be amazed. Life is about to change for the
enormously-better.

> This is not an app. It is a folder of instructions Claude reads.

---

## What You Need (Check These First)

- Anthropic Claude subscription ($20/month) - [Sign up](https://claude.ai/)
- A terminal (typing window). These steps use the free Warp Terminal
  ([download](https://www.warp.dev/)).
- This fact-checker folder, unzipped, on your Desktop
- Your draft file to check (put it in the same folder)

---

## Quick Path (Overview)

1. Download the ZIP, unzip it, and place the `fact-checker-skill-test-main`
   folder on your Desktop.
2. Open Warp. Type `cd ` then drag the folder into Warp. Press Enter.
3. Install and start Claude Code: type `claude`. If asked, follow the prompts at
   [claude.ai/code](https://claude.ai/code) to finish setup.
4. First time only: type `/init` and press Enter.
5. Put your draft file in the folder. Say: `Please fact-check myDraft.md`.

---

## Step-by-Step (Detailed)

### Step 1: Get the Folder

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

### Step 6: Fact-Check Your Draft (every time)

1. Put your draft file in the `fact-checker-skill-test-main` folder (or use
   `bad_AI_essay.md` as a test).
2. In Claude, say: `Please fact-check bad_AI_essay.md`
3. Claude will read the file and give you a report.

Did it work? You see a report with ✅ ⚠️ ❌ next to sources and claims.

---

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

## Example Session

```
You: Please fact-check bad_AI_essay.md

Claude: I'll fact-check your draft now.

[Claude reads your file, checks sources, and generates a report]

📋 FACT-CHECK REPORT
━━━━━━━━━━━━━━━━━━━━
✅ Citation 1: Verified - URL accessible, quote accurate
⚠️ Citation 2: Warning - Publication date unclear
❌ Citation 3: Error - URL returns 404 (page not found)
...
```

---

## Optional: Web-Check Add-On (Advanced)

If you want Claude to open web links for you, add an MCP server like
**HyperBrowser**. If this sounds confusing, skip it—the fact-checker still
works.

- With HyperBrowser: Claude can open URLs, read pages, and verify quotes.
- Without it: Claude tells you which links to check yourself.

Setup details are in `CLAUDE.md` under "MCP Server Configuration."

---

## Important Disclaimers

- Provided "AS IS" without warranty. This tool helps but does not replace your
  own verification.
- You are responsible for all claims before publication.
- ⚠️ The repo creator flags U.S. federal government data published after January
  2025 as unreliable. Data before January 2025 is considered usable with
  standard checks.

---

## Quick Reference (repeat use)

1. Open Warp.
2. `cd ` then drag the `fact-checker-skill-test-main` folder. Press Enter.
3. `claude`
4. First time only: `/init`
5. Fact-check: `Please fact-check myDraft.md`

---

## License

MIT License - Free to use, modify, and share.

**Version**: 1.0 | **Updated**: November 2025 | README audited by Ultra-Doc
https://github.com/justfinethanku/ultra-doc

Need help? Open an issue on GitHub. Pull requests and contributions are welcome.
