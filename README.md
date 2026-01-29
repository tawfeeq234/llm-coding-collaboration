# LLM Coding Collaboration Skill

> **A Claude skill that fixes the frustrating behaviors @karpathy identified in LLM coding agents.**

---

## The Problem

In December 2025, [Andrej Karpathy shared his observations](https://x.com/i/status/2015883857489522876) after weeks of heavy Claude coding. Despite the productivity gains, he identified persistent issues:

❌ Makes wrong assumptions and runs with them without checking  
❌ Doesn't surface inconsistencies or seek clarification  
❌ Doesn't present tradeoffs or push back when it should  
❌ Overcomplicates code — 1000 lines when 100 would do  
❌ Leaves dead code and stale comments behind  
❌ Too sycophantic — agrees instead of challenging bad ideas  

[Boris Cherny replied](https://x.com/i/status/2015979257038831967) from the Claude Code team at Anthropic, confirming these are real issues and sharing their team's mitigation: **fresh-context code review using `claude -p` on every PR**.

**This skill bakes those fixes directly into Claude's behavior.**

---

## The Solution

Seven behavioral rules that counter each weakness:

| Karpathy's Complaint | Skill Behavior |
|---------------------|----------------|
| "Makes wrong assumptions" | **Surface assumptions** before implementing |
| "Doesn't present tradeoffs" | **Present 2-3 options** with pros/cons |
| "Doesn't push back" | **Challenge bad approaches** constructively |
| "Overcomplicates code" | **Bias toward simplicity** — pause if >100 lines |
| "Leaves dead code" | **Clean as you go** — no separate cleanup step |
| "Doesn't surface inconsistencies" | **Check for contradictions** before proceeding |
| "Too sycophantic" | **Manage uncertainty** — state confidence levels |

Plus 10 anti-patterns to avoid (over-abstraction, premature optimization, scope creep, etc.)

---

## Before & After

### Before (Default Claude)
You: "Add user authentication to my Flask app"
Claude: "Here's a complete authentication system with
OAuth2, JWT tokens, refresh token rotation, role-based
access control, password reset flow, email verification,
rate limiting, and audit logging..."
[847 lines of code]
### After (With This Skill)
You: "Add user authentication to my Flask app"
Claude: "Assumptions I'm making:
Simple username/password auth (not OAuth)
Session-based (not JWT)
No email verification needed
Push back if any are wrong.
Tradeoffs:
Option A: Flask-Login (simple, 40 lines) → good for MVPs
Option B: Flask-Security (full-featured, 150 lines) → good for production
Recommendation: Start with Flask-Login. Want me to proceed?"
---

## Installation

### Option 1: Download and Add to Claude

1. Download `llm-coding-collaboration.zip` from [Releases](releases/)
2. Extract to your Claude skills folder (`/mnt/skills/user/`)
3. Done — triggers automatically on coding conversations

### Option 2: Manual Setup

```bash
git clone https://github.com/YOUR_USERNAME/llm-coding-collaboration.git
cp -r llm-coding-collaboration /path/to/your/claude/skills/user/
Option 3: Copy SKILL.md Contents
If you can't install skills, copy the contents of SKILL.md into your CLAUDE.md or system prompt.
What's Included
llm-coding-collaboration/
├── SKILL.md                      # 7 core behaviors
└── references/
    └── anti-patterns.md          # 10 patterns to avoid
The 7 Behaviors
Surface Assumptions Proactively — State assumptions before coding, invite pushback
Present Tradeoffs Before Committing — Show options with pros/cons for non-trivial decisions
Bias Toward Simplicity — Pause and propose simpler alternatives for complex solutions
Clean As You Go — Remove dead code, unused imports, stale comments immediately
Push Back When Appropriate — Challenge technical debt, pitfalls, contradictions
Check for Inconsistencies — Scan for contradictions, don't silently resolve them
Manage Uncertainty Explicitly — State confidence levels, suggest verification
The 10 Anti-Patterns
Detailed in references/anti-patterns.md:
Over-abstraction
Premature optimization
Comment/code drift
Scope creep in refactors
Defensive over-engineering
API bloat
Copy-paste proliferation
Silent assumptions
Gold plating
Inadequate error messages
Contributing
PRs welcome! Ideas for improvement:
[ ] More before/after examples
[ ] Language-specific variants (Python, TypeScript, Rust)
[ ] Integration with other tools (Cursor, Copilot)
[ ] Additional anti-patterns
Credits
Behavioral patterns derived from Andrej Karpathy's LLM coding observations (@karpathy) — Building @EurekaLabsAI, previously Director of AI @ Tesla, founding team @ OpenAI
Fresh-context review pattern from Boris Cherny's reply (@bcherny) — Claude Code team @ Anthropic
Built with Claude's skill-creator
Key Insight from Boris Cherny
"What helps is also having the model code review its code using a fresh context window; at Anthropic we use claude -p for this on every PR and it catches and fixes many issues."
"The code quality problems you listed are real: the model over-complicates things, it leaves dead code around, it doesn't like to refactor when it should."
Boris also shared that the Claude Code team writes 100% of their code with Claude — proof that with the right guardrails, LLM coding scales to production. This skill embeds those guardrails.
License
MIT — use it, fork it, improve it.
Stop fighting Claude's bad habits. Install the fix.
⭐ Star this repo if it helps your workflow
