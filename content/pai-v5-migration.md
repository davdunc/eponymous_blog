Title: From PAI v4 to v5: What Changed and What I Kept
Date: 2026-05-02
Category: technology
Tags: PAI, Claude Code, Fedora, day trading, AI, infrastructure
Slug: pai-v5-migration
Summary: I upgraded my Personal AI Infrastructure from v4.0.3 to v5.0.0 — 42 new skills, a structural shift from Packs to first-class Skills, and a customization pattern that survives upstream syncs. Here's the migration log.

# From PAI v4 to v5: What Changed and What I Kept

I tried to run `/sec-updates` and got "unknown command." That's how I found out my [PAI](https://github.com/davdunc/pai-framework) install was a major version behind upstream — and how a missing security command turned into a full v4.0.3 → v5.0.0 migration. Here's what changed, what I kept, and what I added to support the two halves of my work: Fedora Cloud SIG and day trading.

## The architectural change

The biggest difference between v4 and v5 isn't a feature — it's structural.

In v4, PAI organized capabilities into **Packs** (umbrella containers like `Security` or `Investigation`) that bundled multiple sub-skills. In v5, those Packs got promoted to **first-class Skills**. What used to be `Packs/Security/src/SECUpdates/` is now reachable directly through the Security skill, alongside 45 other skills that ship in the release bundle.

Practically: v4 shipped 11 skills in `.claude/skills/`. v5 ships 46. Things that lived as sub-components — Aphorisms, ApertureOscillation, ArXiv, BrightData, Council, Fabric, FirstPrinciples, ISA, Knowledge, PAIUpgrade, Prompting, RedTeam, Remotion, RootCauseAnalysis, Webdesign, WorldThreatModel, WriteStory — are now top-level skills you can invoke directly.

## What I kept from v4

Three skills stayed exactly as they were:

- **Trading** — my intraday workflow: morning game plans, trade ingestion, daily reviews, ticker research
- **market-data** — historical OHLCV downloads for backtesting
- **trader-tools** — ATR-based stops, position sizing, Camarilla pivots

These are mine. They depend on credentials, accounts, and patterns specific to my setup. The v5 upgrade had no business touching them, and the install script left them untouched. The check was simple: confirm the file `mtime` on `Trading/SKILL.md` was unchanged after the upgrade. It was.

I also kept my customized `Agents`, `Research`, `Telos`, `Thinking`, `USMetrics`, and `Utilities` mega-skills rather than swapping them for v5's split versions. v5's smaller, more granular skills are arguably better-maintained, but my mega-skills already wrap the same functionality with the keywords I'm used to typing. In the future, I can split them if the cost shows up.

## What I added: 42 new skills, in five bundles

I categorized the v5 additions into five mission-aligned bundles and installed them as a unit rather than skill-by-skill:

1. **Security & Threat Intel** — `Security` (which holds SECUpdates, AnnualReports, Recon, WebAssessment, PromptInjection), `WorldThreatModel`, `RedTeam`. Direct fit for the Fedora Cloud SIG work — I need rapid awareness of CVEs that touch the images and containers I help ship.
2. **PAI Self-Maintenance** — `PAIUpgrade`, `CreateSkill`, `CreateCLI`, `BitterPillEngineering`, `Knowledge`, `Delegation`, `Evals`, `Prompting`. The meta layer that keeps the install current and lets me build new skills without reinventing scaffolding.
3. **Thinking & Reasoning Splits** — `Council`, `FirstPrinciples`, `IterativeDepth`, `RootCauseAnalysis`, `SystemsThinking`, `Science`, `BeCreative`, `Ideate`. These were buried inside my v4 Thinking mega-skill; v5 makes them invocable as commands.
4. **Content & Blogging** — `WriteStory`, `ExtractWisdom`, `Fabric` (240+ patterns), `Art`, `ArXiv`, `Aphorisms`. I publish here regularly; this is the production layer.
5. **Intel & Research** — `Browser`, `Investigation`, `PrivateInvestigator`, `Migrate`, `ContextSearch`, `ContentAnalysis`. Useful for community work and for moving data out of rented platforms.

## The customization pattern that survives upgrades

The most useful thing I learned during the migration is the `SKILLCUSTOMIZATIONS` pattern. Each upstream skill checks `~/.claude/PAI/USER/SKILLCUSTOMIZATIONS/<SkillName>/` for a `PREFERENCES.md` and any override files. If the directory exists, the skill loads them and adjusts behavior; if not, defaults apply.

For the Security skill, I wrote a `PREFERENCES.md` and a `sources.json` overlay that adds Fedora Package Announce, Red Hat Security Advisories, CISA KEV, NVD recent CVEs, AWS Security Bulletins, Fedora Magazine, the Linux kernel CVE tracker, and Podman security advisories on top of the upstream defaults (tldrsec, Krebs, Schneier). It also defines a four-tier ranking — CRITICAL through LOW — based on whether items touch the cloud Linux stack I work on.

The benefit: future upstream syncs don't blow away my preferences, because my preferences live outside the upstream tree.

## Sunday morning automation

Last step: I scheduled a remote Claude Code agent to run the customized Security skill every Sunday at 6 AM Central, with the report delivered as an email. The week starts with a tagged inventory of what I need to patch, what I need to watch, and what I can skim. No more clicking through ten browser tabs to compose the same picture by hand.

## The takeaway

Upgrading from v4 to v5 took about an hour and added 42 skills, 5 new agent personas (bringing the total to 19), and a tar backup of the previous install. The work was mostly in the categorization — figuring out what aligned with my missions versus what would just sit installed and unused. The architectural shift from Packs to Skills is genuinely well-thought-through, and the customization pattern means I can stay current with upstream without losing my Fedora and trading-focused tuning.

If you're running a v4 PAI fork and haven't upgraded yet, the [v5.0.0 release](https://github.com/danielmiessler/Personal_AI_Infrastructure/releases/tag/v5.0.0) is worth the migration. My fork — with custom skills excluded for privacy — is at [github.com/davdunc/pai-framework](https://github.com/davdunc/pai-framework).

---

*David Duncan is a momentum trader, Fedora Cloud SIG contributor, and builder of AI-assisted infrastructure at [davidduncan.org](https://www.davidduncan.org).*
