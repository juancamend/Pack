# Pack the PRD Drafting CLI

I write a lot of PRDs. I built this to spend less time on structure and more time on thinking. It takes minimal input about a product problem and generates a complete PRD draft with goals, non-goals, open questions, and success metrics. The output is a starting point, not a finished document.

## Setup

```bash
# Clone the repo
git clone https://github.com/juancamend/Pack
cd prd-cli

# Install dependencies
pip install anthropic

# Set your API key
export ANTHROPIC_API_KEY="your-api-key"
```

## Usage

```bash
python prd.py
```

The tool will prompt you for:
- Product name
- Problem statement (1-2 sentences)
- Target user
- Key constraints (technical, time, scope)
- Primary success metric

It generates a markdown file in the `./output/` directory.

## Example Output

Here's a real PRD generated from these inputs:

- **Product name:** Competitor Change Monitor
- **Problem statement:** Product teams miss important competitor updates because manually checking pricing pages and changelogs is tedious and inconsistent.
- **Target user:** Product managers and competitive intelligence analysts at B2B SaaS companies
- **Key constraints:** Solo build, no real-time requirements, MVP scope only
- **Primary success metric:** Number of competitor changes detected per week that users act on

---

# PRD: Competitor Change Monitor
*Generated March 05, 2026 — review and edit before sharing*

## Problem
Product teams at B2B SaaS companies routinely miss competitor pricing changes, feature launches, and positioning shifts because no one has time to manually check dozens of websites on a regular cadence. This blind spot leads to reactive decision-making: teams learn about competitive moves from customers or sales calls rather than proactively. The result is slower response times and weaker competitive positioning.

## Target User
Product managers and competitive intelligence analysts at mid-market and enterprise B2B SaaS companies. These users are responsible for tracking 5-20 competitors and need to brief stakeholders on market movements. They care about accuracy, signal-to-noise ratio, and being able to quickly share findings with their team. They currently rely on manual checks, Google Alerts (which miss most page changes), or expensive enterprise tools that require procurement cycles.

## Goals
1. Detect pricing page changes across monitored competitors within 24 hours of the change occurring
2. Surface changelog and release note updates from competitor product blogs and docs
3. Reduce time spent on manual competitor monitoring by at least 50%
4. Achieve a 70%+ action rate on detected changes (users mark them as relevant or share them)
5. Support monitoring of at least 20 competitors per user in the MVP

## Non-Goals
- Real-time alerting (daily or twice-daily batches are sufficient for MVP)
- Sentiment analysis or interpretation of what changes mean strategically
- Monitoring social media, press releases, or news coverage
- Competitive battlecard generation or sales enablement content
- Multi-user collaboration or team workspaces

## Proposed Approach
The core product is a monitoring service that periodically screenshots and extracts text from user-specified competitor URLs (pricing pages, changelog pages, release notes). When meaningful differences are detected between snapshots, the user receives a summary of what changed.

Users configure monitoring by adding URLs and setting a check frequency. The system stores historical snapshots so users can see how a page evolved over time. The MVP focuses on visual diffs (screenshot comparison) and text diffs (content extraction), avoiding complex semantic analysis.

Delivery happens via email digest or a simple web dashboard. The emphasis is on low noise: only surface changes that are likely to matter, and make it easy for users to dismiss false positives so the system learns their preferences.

## Open Questions
1. What URL patterns reliably point to pricing and changelog pages across different SaaS products, or do users need to manually specify each URL?
2. How do we distinguish meaningful content changes from layout tweaks, A/B tests, or localization variations?
3. What's the right default check frequency? Daily might miss fast-moving competitors; hourly might create noise and cost issues.
4. Should the MVP include any historical archive, or just alert on new changes?
5. How do users want to consume this—email, Slack, dashboard, or all three?

## Success Metrics

**Primary metric:** Number of competitor changes detected per week that users act on (view details, share, or mark as important).

**Leading indicators:**
- Number of URLs actively monitored per user
- Check-in frequency (how often users open the digest or dashboard)
- Time from change detection to user viewing the change

**Lagging indicators:**
- User retention at 30 and 90 days
- Expansion from MVP users to paid plans
- Reduction in self-reported time spent on manual competitor monitoring

---

## Limitations

This tool generates a draft, not a finished PRD. After running it:

1. **Review every section.** The AI expands your inputs but doesn't know your business context.
2. **Rewrite the approach.** The tool stays deliberately vague here. You need to add specifics.
3. **Validate the non-goals.** Make sure they reflect real scope decisions, not just plausible guesses.
4. **Answer the open questions.** That's the actual work. The PRD is just the container.
5. **Delete anything that doesn't fit.** Less is more in a PRD.

This is not a replacement for thinking. It's a way to skip the blank page.
