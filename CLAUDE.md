# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the **Fact-Checker Skill** for Claude Code - a specialized system for verifying citations and factual claims in long-form content, investigative journalism, and analytical writing. It is implemented as a Claude Code skill that automatically activates when users request fact-checking.

### Directory Structure

```
fact-checker-skill-test/
├── .claude/
│   └── skills/
│       └── fact-checker/
│           └── SKILL.md              # Skill metadata and activation trigger
├── fact_checker_system_prompt.xml   # Complete verification protocol (533 lines)
├── bad_AI_essay.md                   # Sample test content
├── README.md                         # User-facing documentation
└── CLAUDE.md                         # This file
```

## Architecture

### Core Components

1. **Skill Definition** (`.claude/skills/fact-checker/SKILL.md`)
   - Metadata and skill description
   - Activation trigger: When user requests fact-checking
   - Points to the comprehensive system prompt

2. **System Prompt** (`fact_checker_system_prompt.xml`)
   - Complete fact-checking protocol (533 lines)
   - Source classification rules
   - URL verification protocol (5-step process)
   - Claim type taxonomy (Type A/B/C/D)
   - Report generation templates

3. **Test Content** (`bad_AI_essay.md`)
   - Sample content for testing the fact-checker

### Fact-Checking Workflow

The system follows this verification pipeline:

1. **Source Classification**
   - Acceptable: Government data, academic research, journalism, primary documents
   - NOT acceptable as factual sources: AI conversation threads (opinion/analysis only)
   - Special handling: U.S. federal .gov sources published after January 2025 are flagged as potentially unreliable

2. **Verification Protocols**
   - Internal sources: File existence, claim validation, context verification
   - External sources: 5-step URL verification protocol (accessibility, publication date, retractions, quotes, context)

3. **Claim Type Taxonomy**
   - **Type A (Factual Claim)**: Needs verification or sourcing
   - **Type B (Critique/Example)**: Demonstrates dysfunction - verify accuracy, not "find sources"
   - **Type C (Opinion/Interpretation)**: Label clearly or add supporting sources
   - **Type D (Rhetorical/Voice)**: No action needed

4. **Report Generation**
   - Structured markdown format with status indicators (✅ ⚠️ ❌)
   - Citation verification section
   - Factual claims analysis by type
   - Research gaps with priority levels
   - Actionable recommendations

### Critical Design Principles

**Source Type Enforcement**: AI conversation threads can be used for voice training and perspective but NEVER as factual sources. This is rigorously enforced.

**Context-Aware Analysis**: The system distinguishes between factual claims needing sources and critiques demonstrating dysfunction. Example: "Government search returns outdated article" is a critique showing poor search functionality, not a claim needing a source.

**Error Nuance Principle**: "Factual errors may exist within valid arguments. Correct the error, preserve the valid critique." The system assesses whether underlying arguments remain valid despite factual errors.

**U.S. Federal Data Warning**: Any U.S. federal government data sources (.gov) published AFTER January 2025 are flagged with reliability warnings due to documented infrastructure disruption.

## Skill Activation

The fact-checker skill is automatically invoked when the user's request contains fact-checking intent. The skill system reads `.claude/skills/fact-checker/SKILL.md`, which points to `fact_checker_system_prompt.xml` for the complete protocol.

### Activation Triggers

User requests that activate the skill:
- "Please fact-check this draft"
- "Verify the citations in bad_AI_essay.md"
- "Check the sources for [content]"
- Any variation mentioning fact-checking, citation verification, or source validation

### Execution Flow

When activated, the skill:
1. Loads the complete verification protocol from `fact_checker_system_prompt.xml`
2. Applies the 5-step URL verification protocol for external sources
3. Classifies claims by type (A/B/C/D taxonomy)
4. Generates a structured fact-check report with status indicators (✅ ⚠️ ❌)

### Testing the Skill

Use `bad_AI_essay.md` as test content:
```bash
# In Claude Code terminal:
claude

# Then in the Claude Code session:
User: "Please fact-check bad_AI_essay.md"
```

## Web Scraping Requirements

External URL verification requires web scraping capabilities. The system will use available tools automatically.

### Recommended Tools

- **HyperBrowser MCP**: `@hyperbrowserai/mcp` (recommended)
- **Any MCP-compatible web scraping tool**: WebFetch, browser automation tools
- **Without tools**: URL verification will be manual/limited

### 5-Step URL Verification Protocol

For each external URL cited in content:

1. **Accessibility Check**: Verify URL resolves (not 404, check for paywalls/redirects)
2. **Publication Date**: Extract actual date from byline, compare to draft claims
3. **Retraction/Correction Scan**: Search for corrections or retractions
4. **Quote Verification**: Confirm quotes appear verbatim (not just paraphrased)
5. **Context Verification**: Validate source supports claim (not misrepresented)

### MCP Server Configuration

If using HyperBrowser, configure in Claude Code settings:
```json
{
  "mcpServers": {
    "hyperbrowser": {
      "command": "npx",
      "args": ["-y", "@hyperbrowserai/mcp"]
    }
  }
}
```

## Development Constraints

When working with or modifying this fact-checker system:

### DO NOT
- Modify the core verification protocol without understanding the full claim taxonomy (A/B/C/D)
- Accept AI conversation threads as factual sources (opinion/analysis only)
- Flag critiques demonstrating dysfunction as "missing sources" (verify accuracy instead)
- Remove valid critiques due to minor factual errors (correct error, preserve critique)
- Skip claim type classification before flagging research gaps

### DO
- Use web scraping tools for all external URL verification
- Classify every claim by type (A/B/C/D) before analysis
- Provide clear status indicators (✅ ⚠️ ❌) in all reports
- Include legal disclaimers in generated reports
- Flag U.S. federal .gov sources published after January 2025 as potentially unreliable
- Assess whether underlying arguments remain valid despite factual errors

## Report Output Structure

Generated fact-check reports follow this structure:

```markdown
# Fact-Check Report: [Draft Title]
**Date**: YYYY-MM-DD
**Status**: ✅ VERIFIED / ⚠️ NEEDS REVIEW / ❌ PROBLEMATIC

## Citation Verification

### Internal Sources
[File existence, claim validation, context verification]

### External Sources (Web Verification)
- **URL**: [full URL]
- **Accessibility**: ✅ / ❌ / ⚠️
- **Publication Date**: Actual vs. Claimed
- **⚠️ U.S. Federal Post-Jan 2025**: YES/NO
- **Quotes Verified**: ✅ VERBATIM / ⚠️ PARAPHRASED / ❌ NOT FOUND
- **Context**: ✅ SUPPORTS / ⚠️ PARTIAL / ❌ MISREPRESENTED

## Factual Claims Analysis
- **Type A**: Factual claims needing sources
- **Type B**: Critiques demonstrating dysfunction (verify accuracy)
- **Type C**: Opinions/interpretations (label or support)
- **Type D**: Rhetorical/voice elements (no action)

## Research Gaps
- **HIGH**: Missing sources for factual claims
- **MEDIUM**: Optional supporting sources
- **NO ACTION**: Critiques (verify accuracy instead)

## Recommendations
[Actionable next steps for editorial review]
```

## Legal Context

This system includes legal disclaimers in multiple locations:

- **Provided "AS IS"** without warranty
- Designed to **ASSIST**, not replace independent verification
- Users responsible for verifying all claims before publication
- No liability for errors, omissions, or consequences

Disclaimers appear in:
- `fact_checker_system_prompt.xml` (top-level XML comment)
- `README.md` (Legal Notice section)
- `.claude/skills/fact-checker/SKILL.md` (Legal Disclaimer section)
- Generated fact-check reports (header and footer)
