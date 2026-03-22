# jbrjake's Plugin Marketplace

Five Claude Code plugins by one person who decided the best use of their time was building a fictional software team with elaborate backstories, unresolved personal issues, and strong opinions about your test coverage.

## What's in here

A plugin for each stage of building software:

1. **Janna** figures out what you're building
2. **Giles** runs the sprints
3. **Snyder** enforces hard mode on every file Claude touches
4. **Holtz** audits your codebase until it stops having new problems
5. **Sineya** makes the other four actually get listened to

Each one works fine on its own. Together they're a pipeline from "I had an idea in the shower" to "it shipped and the tests aren't lying."

They're all characters. They have deep backstories — not flavor text, but detailed inner lives that shape how they approach problems. This is part gimmick, part technique. LLMs follow instructions more reliably when those instructions come from a persona with reasons for caring, and Sineya has the research citations to back that up. It's also just more fun than reading a bulleted list of rules.

## The lineup

### [Janna](https://github.com/jbrjake/janna) — the product mind

You give her a half-formed idea. She gives you back PRDs, user personas, simulated focus groups where participants disagree with each other, a dev team profile, a pitch deck, user stories, and an agile backlog. She starts every project with a tarot reading for lateral thinking. (Real randomization. It's a forcing function, not mysticism, but she wouldn't put it that way.)

Her defaults lean toward self-service, product-led growth, and API-first architecture. Push back and she'll adjust. Don't push back and you'll get a spec that assumes your users hate phone calls with sales reps.

| Command | What it does |
|---------|-------------|
| `/napkin [idea or path]` | Run the full napkin-to-spec pipeline |
| `/janna-status` | Check which phase you're on and what's next |

---

### [Giles](https://github.com/jbrjake/giles) — the scrum master

He runs your sprints on actual GitHub infrastructure. Issues, PRs, labels, milestones, code reviews — all real, all on your repo.

`/sprint-run` executes a full sprint: kickoff, TDD development with parallel agents, peer reviews on GitHub PRs, demo, and a retrospective that edits your project docs so lessons stick around instead of evaporating. The dev team personas review code through the lens of their backgrounds, which sounds silly until you notice the findings are specific and useful.

| Command | What it does |
|---------|-------------|
| `/sprint-setup` | One-time project bootstrap — scans your project, generates config, creates GitHub labels and milestones |
| `/sprint-run` | Execute a full sprint with ceremonies, TDD, PRs, and reviews |
| `/sprint-monitor` | Check CI, manage PRs, update burndown (designed for `/loop 5m sprint-monitor`) |
| `/sprint-release` | Tag a release, build artifacts, generate release notes, close the milestone |
| `/sprint-teardown` | Remove sprint config cleanly |

---

### [Snyder](https://github.com/jbrjake/snyder) — hard mode

This is the warnings-as-errors plugin.

Every file Claude edits gets auto-formatted. Every edit gets linted with findings injected back into the conversation so Claude sees its own mistakes in the same turn. Every tool runs at the strictest setting that still compiles — `select = ["ALL"]`, `linters.default: all`, `opt_in_rules: [all]`. Warnings are errors. The default is the maximum, and you relax it explicitly, with a reason.

When Claude tries to say "done," a quality gate runs linting, type checking, and the test suite. If anything fails, Claude keeps working. Dangerous commands — force push, `rm -rf /`, `curl | bash`, writing to `.env`, `DROP TABLE` — get blocked before they execute. 143 tests just for the security blocker. 408 total.

The philosophy: CLAUDE.md rules are suggestions Claude follows maybe 70% of the time. Hooks fire 100% of the time. Snyder bridges both — explains *why* rules exist (so Claude complies more reliably), then installs hooks that make violations impossible regardless.

| Command | What it does |
|---------|-------------|
| `/snyder:harden` | Apply the full enforcement stack to your project |
| `/snyder:setup` | Audit which quality tools are installed and what's missing |
| `/snyder:check` | Run lint + type check + tests (or pass `lint`, `types`, `tests`, `security`, `coverage`, `secrets` for a subset) |
| `/snyder:ci` | Generate a GitHub Actions workflow with SHA-pinned actions |

Also activates when you say "harden this project" or "run on hard mode." Seven hooks fire automatically on every edit, every bash command, and every task completion. You don't invoke them. They just happen.

---

### [Holtz](https://github.com/jbrjake/holtz) — the auditor

You point him at a codebase. He runs seven phases: recon, doc-to-implementation audit, test quality audit, adversarial code review, TDD fix loop, pattern analysis, and convergence. Every finding gets severity, evidence, acceptance criteria, and a command to validate the fix. Every fix starts with a failing test.

The convergence loop is the thing that makes Holtz different from a code review. A code review happens once. Holtz happens until the codebase stops producing new findings. Fix a bug, and the fix shifts the terrain — things that were hidden become visible. He runs another pass. This continues until two consecutive passes find nothing new. Everything before that is just progress.

When two or more bugs share a root cause, he searches for the rest of the family.

| Command | What it does |
|---------|-------------|
| `/holtz [target]` | Run the full audit — optionally point him at a specific file, directory, or area of concern |

---

### [Sineya](https://github.com/jbrjake/sineya) — the meta-plugin

She doesn't write your code. She makes the other plugins' instructions actually stick.

The problem: Claude can perfectly understand a skill's instructions while systematically not following them. "Always write tests first" is a general imperative, and Claude can rationalize its way around a general imperative. "If a file in `src/` exists without a corresponding file in `tests/`, create the test file first" is a testable constraint, and that's harder to skip. Sineya rewrites the former into the latter.

She's backed by 48 academic papers on LLM instruction compliance and empirical data showing that advisory language like "you should consider" gets skipped 100% of the time. She knows you have a budget of roughly 150 effective instructions before compliance starts dropping, and your system prompt already uses about 50. She has a taxonomy of nine ways plugin instructions fail and fixes for each.

| Command | What it does |
|---------|-------------|
| `/sineya:audit [path]` | Read-only quality audit of a plugin — scores against a multi-tier checklist, returns a report card |
| `/sineya:improve [path]` | Full improvement pass — classifies, scores, fixes, pressure-tests, iterates |

Also activates on its own when you're writing or debugging plugin skills.

---

## Why they work together

Janna turns your idea into a spec. Giles turns the spec into sprints and runs them on GitHub. Snyder watches every edit in real time — formatting, linting, blocking, gating. Holtz comes in after and finds what survived prevention. Sineya tunes all their instructions so Claude actually follows them.

You don't need all five. Any one of them does its job independently. But the pipeline is there if you want it, and the characters have opinions about each other that occasionally surface in the output, which is either a feature or a sign that the author spent too long on this. Possibly both.

## Installation

```bash
# Add the marketplace
/plugin marketplace add jbrjake/claude-plugin-marketplace

# Install whichever ones you want
/plugin install janna@jbrjake
/plugin install giles@jbrjake
/plugin install snyder@jbrjake
/plugin install holtz@jbrjake
/plugin install sineya@jbrjake
```

## License

MIT, all of them.
