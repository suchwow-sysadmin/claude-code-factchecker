---
name: fact-checker
description: Verify citations and factual claims in long-form content. Checks URLs for accessibility and accuracy, validates quotes, analyzes source credibility, and distinguishes facts from opinions. Use when fact-checking article drafts, validating citations, or reviewing claims before publication.
---

# Fact-Checker for Writers

A specialized fact-checking system for long-form content, investigative journalism, and analytical writing.

## When to Use This Skill

Invoke this skill when you need to:
- Verify citations in drafts (internal sources and external URLs)
- Validate factual claims and identify unsourced assertions
- Check if sources say what the author claims they say
- Distinguish between claims needing sources vs. critiques demonstrating dysfunction
- Generate comprehensive fact-check reports with actionable recommendations

## Instructions

When this skill is invoked, you must follow the comprehensive fact-checking system prompt located at:

`../../../fact_checker_system_prompt_1.1.xml`

Read this file and follow ALL instructions within it exactly.

**Current Version**: 1.1 (includes User Context Verification Protocol)

### Quick Reference

The system prompt defines:

1. **5-Step URL Verification Protocol**
   - Accessibility check (404, paywall, redirects)
   - Publication date verification
   - Retraction/correction check
   - Quote verification (verbatim vs paraphrased)
   - Context verification (supports claim vs misrepresented)

2. **Claim Type Taxonomy** (Type A/B/C/D)
   - **Type A: Factual Claim** - Needs verification or sourcing
   - **Type B: Critique/Example** - Demonstrates dysfunction (verify accuracy, not "find sources")
   - **Type C: Opinion/Interpretation** - Label clearly or add supporting sources
   - **Type D: Rhetorical/Voice** - No action needed

3. **Source Classification**
   - Acceptable: Government data, academic research, journalism, primary documents
   - NOT acceptable as factual sources: AI conversation threads (opinion/analysis only)
   - Warning: U.S. federal (.gov) sources published after January 2025 flagged as potentially unreliable

4. **Critical Nuance Principle**
   > "Factual errors may exist within valid arguments. Correct the error, preserve the valid critique."

## Output Format

Generate structured reports with:
- **Citation Verification** (internal and external sources)
- **Factual Claims Analysis** (by type: A/B/C/D)
- **Research Gaps Identified** (with priority: HIGH/MEDIUM/NO ACTION)
- **Summary** (✅ Verified / ⚠️ Needs Review / ❌ Problematic)
- **Recommendations** (actionable next steps)

Use clear status indicators:
- ✅ = Verified, no issues
- ⚠️ = Needs review or user attention
- ❌ = Problem found, requires action

## Legal Disclaimer

This fact-checking system is provided "AS IS" without warranty. It is designed to ASSIST with fact-checking and should not be relied upon as the sole method of verification. Users are responsible for independently verifying all claims before publication.

## Technical Note

This skill works best with web scraping tools (like HyperBrowser MCP) for automated URL verification. Without web scraping tools, URL verification will be manual or limited.
