Title: PAI Framework: Building a Personal AI Infrastructure on Claude Code
Date: 2026-04-16
Category: technology
Tags: AI, Claude Code, PAI, infrastructure, open-source
Slug: pai-framework
Summary: I'm open-sourcing the framework behind my Personal AI system — a skill-based, memory-persistent AI assistant built on Claude Code. Here's what it is, where it came from, and why I'm sharing it.

# PAI Framework: Building a Personal AI Infrastructure on Claude Code

I've been running a system I call PAI — Personal AI Infrastructure — on top of [Claude Code](https://claude.ai/claude-code) for the past few months. Today I'm open-sourcing the framework.

**Repository:** [github.com/davdunc/pai-framework](https://github.com/davdunc/pai-framework)

## What PAI Does

PAI turns Claude Code from a general-purpose assistant into a persistent, personalized AI system. It adds:

- **The Algorithm** — A structured 7-phase execution framework (Observe → Think → Plan → Build → Execute → Verify → Learn) that produces verifiable outcomes. Every task generates Ideal State Criteria and tracks progress against them.
- **Skills** — Modular capability packages. I use skills for trading analysis, multi-agent research, life goals tracking (TELOS), and analytical thinking (first principles, council debates, red teaming).
- **Hooks** — Lifecycle event handlers that fire on tool use, session start/end, and context compaction. They handle security validation, session learning, and system integrity automatically.
- **Memory** — A persistent file-based memory system. PAI remembers context across conversations — who I am, what I'm working on, what feedback I've given, and what it's learned from past sessions.

## Where It Came From

The architecture was originally designed by Daniel. I inherited the system and have been evolving it toward my own mission: systematic trading automation, Linux cloud infrastructure (Fedora Cloud SIG), and bridging the two through a platform called Falcon.

The framework is genuinely well-designed. The Algorithm alone — with its mandatory criteria decomposition, effort-level tiering, and built-in learning reflections — has changed how I approach complex work. I wanted to share it back, both as a thank-you to Daniel and because I think more people should be building personalized AI systems rather than using generic assistants.

## What I've Customized

My PAI instance is tuned for:

- **Trading** — Morning game plans, market data analysis, trade review, discipline workshop entries
- **Infrastructure** — Podman containers, bootable container images, gateway stacks
- **Learning** — Math concepts for quantitative trading, market microstructure, systematic approaches

The public repository is sanitized — no personal data, no credentials, no account numbers. It's a clean framework you can fork and make your own.

## How to Use It

1. Install [Claude Code](https://claude.ai/claude-code)
2. Clone the repo into `~/.claude/`
3. Create your own `PAI/USER/` directory with your goals and projects
4. Start a conversation — PAI's mode system (Minimal, Native, Algorithm) kicks in automatically

The most powerful feature is the TELOS system — a life operating system where you define your goals, projects, and challenges. PAI uses this context to personalize every interaction. When I ask for a morning trading game plan, it knows my risk tolerance, my playbook setups, and which behavioral patterns I'm working to fix.

## Why Open Source This

I'm an open-source person. I work on Fedora Cloud images. I believe tools should be shared, forked, and improved collectively.

More practically: if you're using Claude Code and you're not building persistent context around it, you're leaving most of the value on the table. PAI is one way to capture that value. There are certainly others, and I'd love to see what people build.

---

*David Duncan is a momentum trader, Fedora Cloud SIG contributor, and builder of AI-assisted infrastructure at [davidduncan.org](https://www.davidduncan.org).*
