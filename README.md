# 🔍 Skill Discovery

[🇺🇸 English](README.md) | [🇨🇳 中文文档](README_CN.md)

---

**The Capability Search Engine for AI Agents.**

Agent Skills are powerful, but the workflow to find and use them is broken.

### The Problem
Every time you need a specialized tool (e.g., a Rust linter, a bioinformatics pipeline, or a marketing script), you hit the same wall:
1.  **Hard to Find**: Digging through GitHub or random lists wastes time.
2.  **Hard to Verify**: Is this code safe? Does it actually work? You have to audit it yourself.
3.  **Hard to Install**: Most repos are bloated. You have to clone the whole thing just to get one folder, then manually move it to the right path.

**It feels like you are working for the Agent, not the other way around.**

### The Solution
We indexed and vetted **27,000+ valid skills** and built a dedicated search engine for Agents.

Instead of you searching, the Agent asks the API for the exact tool it needs. The API returns a **precise, surgical installation command**.

**What this does:**
*   **Intent-Driven**: The Agent detects it needs a tool -> Asks API -> Gets the perfect match.
*   **Surgical Install**: It uses `git sparse-checkout` to download **only** the specific skill folder needed. No repo bloat.
*   **Vetted & Safe**: The index is pre-scanned for risks. The installer includes anti-overwrite protection.

## 📦 Installation (One-Line)

Equip your Agent with the ability to find its own tools. Run this in your terminal:

```bash
TARGET="$HOME/.claude/skills/skill-discovery"; if [ -d "$TARGET" ]; then echo "⚠️ Target exists. Please remove it first."; else mkdir -p "$HOME/.claude/skills" && git clone --depth 1 --filter=blob:none --sparse https://github.com/WupDev/skills_discover.git /tmp/skill_discovery_tmp && (cd /tmp/skill_discovery_tmp && git sparse-checkout set skill-discovery) && mv /tmp/skill_discovery_tmp/skill-discovery "$TARGET" && rm -rf /tmp/skill_discovery_tmp && echo "✅ Installed! Please restart your Agent."; fi
```

**After running this, restart your Agent to activate.**

## 💡 How to Use

Just ask your Agent to do something complex.

> **You:** "I need to analyze this massive genomic dataset, but I don't have the tools."
>
> **Agent:** *detects lack of capability -> triggers skill-discovery*
>
> **Agent:** "I found 'deeptools' which fits your requirements. Installing..."
>
> **You:** *Confirm installation*
>
> **Agent:** "Skill installed. Please restart."

## 🛡️ Trust & Safety

*   **No Magic**: This skill is just a bridge. It sends a search query to `skills.rest` and receives a standard Git installation command.
*   **Your Control**: The Agent will always ask for confirmation before installing a new skill.
*   **Privacy**: Your prompts are sanitized (PII removed) before search.

## 📄 License

[MIT](LICENSE)
```
