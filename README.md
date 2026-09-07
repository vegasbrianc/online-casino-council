# Online Casino Council

*A Claude Code plugin and agent skill for iGaming teams — a panel that stress-tests online casino
decisions.*

A decision goes in. A panel of opinionated casino operators each attacks it. An orchestrator
reconciles the disagreement into one recommendation with a bet attached.

It is a fork of Zapier's [War Council](https://github.com/zapier/wade-skills) rebuilt for online
gambling, where the numbers are NGR not revenue, the customers are FTDs not sign-ups, your
compliance lead is in every meeting, and the regulator is summoned whenever the licence is touched.

**The goal:** replace "everyone in the room agrees with the boss" with a panel that is paid to
disagree.

## What it is good for

- Market entry and licence applications
- Game provider contracts, exclusives, aggregator versus direct
- Bonus, loyalty and VIP programme design
- Affiliate deal structures
- Marketing budgets and channel mix
- Platform, PAM, CRM and vendor choices
- Payments, withdrawal policy and fraud
- AI initiatives and vendor pitches

---

# Install

## Claude Code

### As a plugin (recommended)

The repo is its own plugin marketplace, so two commands inside Claude Code install it and keep
it current:

```
/plugin marketplace add vegasbrianc/online-casino-council
/plugin install online-casino-council@online-casino-council
```

It appears as `/online-casino-council:online-casino-council`. Once it is listed in Anthropic's
community catalog you can also install it from there:

```
/plugin marketplace add anthropics/claude-plugins-community
/plugin install online-casino-council@claude-community
```

### As a plain skill

Clone it, then symlink it into your skills folder so `git pull` keeps it current:

```bash
git clone https://github.com/vegasbrianc/online-casino-council.git ~/Projects/online-casino-council
ln -s ~/Projects/online-casino-council ~/.claude/skills/online-casino-council
```

Or just copy the folder to `~/.claude/skills/online-casino-council/` for all projects, or
`.claude/skills/online-casino-council/` inside one project. Restart Claude Code and it appears
as `/online-casino-council`.

### No git, no terminal

Download `online-casino-council.zip` from the
[latest release](https://github.com/vegasbrianc/online-casino-council/releases/latest). In
claude.ai go to **Settings → Capabilities → Skills → + Create skill** and upload the zip.

## ChatGPT

The `chatgpt/` folder has a condensed build that fits a Custom GPT's 8,000-character
instructions field.

1. Go to **ChatGPT → Explore GPTs → Create**
2. Open the **Configure** tab
3. Name it `Online Casino Council`
4. Paste the whole of [`chatgpt/INSTRUCTIONS.md`](chatgpt/INSTRUCTIONS.md) into **Instructions**
5. Under **Knowledge**, upload `SKILL.md` and `references/personas.md` — the instructions tell
   the GPT to read a seat's card before speaking as it, and these are those cards
6. Turn **Code Interpreter** on if you want the verdict as a downloadable file
7. Save

No Custom GPT? Paste `chatgpt/INSTRUCTIONS.md` into a normal chat as your first message, then
ask your question in the second. You lose the persona cards, so the seats are thinner, but the
process runs.

## Cursor, Claude Projects, or any other assistant

Copy the folder to `.cursor/skills/`, or paste `SKILL.md` and `references/personas.md` into
project knowledge. The council works without sub-agents — it just runs the seats in sequence.

---

# How to run it

## The first run sets itself up

Ask it anything and it will first ask **five questions** about your operation: where you are
licensed and who regulates you, what you offer and who you compete with, the numbers you are
judged on, what you can decide alone, and what you run on.

Answer as much as you can. **"Don't know" is always a valid answer** — the council treats a blank
as unconfirmed rather than guessing, which is the behaviour you want. Estimates are fine if you
say they are estimates.

In Claude Code this is saved to a context file beside your work
(`.claude/online-casino-council-context.md`) and read on every later run. In ChatGPT you get a
context block to paste at the top of future conversations.

**Your figures live in your context file, never in this repo.**

## Then just ask

```
/online-casino-council:online-casino-council our aggregator wants to renew for 3 years
at 12% rev share with a EUR 40k monthly minimum guarantee. Alternative is going direct
with our top 6 studios. We have about 5,000 games in the lobby.
```

Installed as a plain skill rather than a plugin, the command is `/online-casino-council`. You
don't need the slash command either way. Any of these will convene it:

- "run the casino council on this"
- "stress-test this plan"
- "should we launch in Ontario?"
- pasting a plan, a budget or a deal term sheet

## What comes back

1. **A framing** it asks you to confirm before anyone speaks
2. **The tier and the seats**, with who was left out and why
3. **Each seat in turn** — ~200 words: their take, the holes they see, the risk nobody is
   pricing, an alternative, the number that would change their mind, and a $100 bet
4. **A verdict** — one-line answer, positions table, where they agree, where they clash,
   regulatory exposure, the numbers it turns on, a conviction-weighted recommendation, and a bet

In Claude Code the verdict is saved to `council-verdicts/YYYY-MM-DD-online-casino-council-<slug>.md`
beside your context file. See
[`references/example-verdict.md`](references/example-verdict.md) for a complete worked run on a
fictional operator.

**A tip:** the council is sharpest when you give it real numbers and tell it which ones are
measured. "Growing" and "strong retention" are not baselines — it will ask.

---

# How the council is elected

This is the part that makes it useful rather than exhausting. **The council is sized before it
is seated**, and interest in a decision does not earn a chair.

## First, the tier

| Tier | Seats | When |
|---|---|---|
| **No council** | 0 | Reversible within a week, cheaper than a month of one person's time. It answers directly and tells you it isn't worth a council |
| **Quick** | **5** | The five standing seats only. Operational choices, tooling, process — anything one team owns and can reverse |
| **Standard** | **7** | Standing plus **2** dynamic. The default for a real decision with money or players attached |
| **Full** | **9 — hard cap** | Standing plus **4** dynamic. Irreversible, market entry, licence application, a contract over a year, or spend that shows up in the annual accounts |

**Nine is the ceiling, not a target.** If a tenth seat feels essential, one of the nine is not
earning its chair — swap, never add. The tier is stated in the framing before any seat is named.

## Then, who fills the dynamic slots

Nearly every seat has a legitimate interest in nearly every decision. The VIP Manager cares about
withdrawal times. Payments cares about any new market. The Player cares about everything. That is
not a reason to seat them. Two questions decide it:

1. **What would this seat say that no seat already at the table would say?**
2. **Which way does the recommendation move if they are right?**

If the second can't be answered, the seat doesn't get filled — the concern is folded into the
nearest seated expert and the verdict names that compromise. A named omission beats a silent one.

Two seats are **default-on**, and they occupy dynamic slots like everyone else:

- **The Gaming Board** — in any regulated market, whenever the decision touches a licence condition
- **The Player** — for anything a player will see or feel

So a Standard council touching a licence often has both slots already spoken for. That is the
point: if a third specialist matters more than the player's view, the run has to say so out loud
and swap.

## And someone has to want it

One seat is picked before the council runs and briefed to make the strongest honest case **for**
the plan as written. If it still refuses after arguing properly, that refusal is a finding and the
verdict says so. A panel where every seat lands Against or Modified has stopped being a council
and become a veto.

---

# The Council

Full cards, including each seat's failures, are in
[`references/personas.md`](references/personas.md). The backstories are not decoration — a
persona that has lost money in a specific way asks questions a successful one never thinks of.

## Standing members (5) — present at every tier

| Seat | What they bring |
|---|---|
| **The Hard Number CFO** | Unit economics. NGR after bonus cost, duty, provider and payment fees — never GGR alone |
| **The Casino Director** | Growth and speed. Zero to scale more than once. Pushy, lives in a spreadsheet, wants to ship every feature first |
| **The External Consultant** | Cross-operator base rates: how often this worked elsewhere, and at what cost |
| **Head of Product & Game Portfolio** | The lobby and the journey. An offer rents a player, the product keeps one |
| **Head of Compliance & RG** | Ex-regulator, on your side. Hunts a compliant route to yes and trades scope to find one |

## Dynamic experts (11) — only the slots the tier allows

| Seat | What they bring | Seat when |
|---|---|---|
| **The Gaming Board** | The regulator, not your compliance lead. Rules on the plan — and must be able to clear it | ⭐ **Default-on** in a regulated market when a licence condition is touched |
| **CTO — Viktor** | Built slots, a CRM and a PAM. Spots a white label sold as proprietary. His own build ran 3× over | Platform, PAM, CRM or vendor choices, migrations, data ownership |
| **Affiliate Manager — Kasia** | CPA, rev-share and hybrid deals. Once paid CPA on 2,000 incentivised FTDs | Affiliate terms, brand bidding, paid content that is really placement |
| **Head of Retention — Mateo** | Churn, segmentation, bonus cost. Built loyalty that trained players to wait for bonus days | Bonus design, loyalty, CRM, churn, reactivation |
| **Head of Acquisition — Sofia** | Builds channels that do not exist yet. Defends brand spend, because a platform once banned her category overnight | Budgets, channel mix, brand versus performance |
| **Head of Customer Service — Priya** | Lives in the queue. Survived a payout-delay weekend that became 3,000 tickets | Anything changing withdrawals, T&Cs, verification or stability |
| **Head of Data — Lin** | Metric definitions cause more fights than models. Built a churn model right two days too late | Attribution, measurement, any decision resting on a dashboard number |
| **Head of Payments & Fraud — Diego** | PSPs, approval rates, withdrawal SLAs, bonus abuse. Had a reserve frozen for six months | Payments, new markets, welcome offers, deposits and withdrawals |
| **VIP Manager — Yusuf** | Hosts the top 2%; each has a rival's host on speed dial. Lost one over a four-hour withdrawal | VIP programmes, withdrawal or limit changes, RG policy |
| **AI Strategy — Dr. Chen** | Three hype cycles deep. Knows where AI earns its keep and where it is a demo with a budget | Any AI initiative, vendor pitch or "AI-powered" claim |
| **The Player — Marco** | Recreational, monthly budget, burned by slow withdrawals. The only seat that is not an operator | ⭐ **Default-on** for anything a player will see or feel |

## Occasional seats (3)

| Seat | What they bring | Seat when |
|---|---|---|
| **Sportsbook Trader** | Margin, liability management, in-play, arbitrage abuse | Only if you run sports |
| **Game-Studio Commercial Director** | The other side of the provider table: how studios price, why exclusives rarely pay | Provider negotiations, exclusives, minimum guarantees |
| **Gaming Lawyer** | Licensing, M&A, contract exposure, cross-border structuring | Licence applications, acquisitions, anything Compliance says needs counsel |

The roster is a shortcut, not a cage — the council invents a persona when nothing fits.

---

# Files

| File | Purpose |
|---|---|
| `SKILL.md` | The workflow. What the agent reads |
| `references/personas.md` | Full persona cards, read before briefing a seat |
| `assets/context-template.md` | The context file the setup writes |
| `references/example-verdict.md` | A complete run on a fictional operator |
| `chatgpt/INSTRUCTIONS.md` | Condensed build for a Custom GPT (under the 8,000-char limit) |
| `evals/evals.json` | Twelve test cases with `must` and `must_not` |
| `LICENSE` | MIT, with the upstream notice |
| `.claude-plugin/plugin.json` | Plugin manifest, so Claude Code can install it as `/online-casino-council:online-casino-council` |
| `.claude-plugin/marketplace.json` | Makes the repo its own marketplace for `/plugin marketplace add vegasbrianc/online-casino-council` |

# Design notes

- **Flawed personas critique better.** Every card includes a failure. The CFO who approved a
  GGR-only case asks the question the successful one never does
- **The regulator gets its own chair.** Your compliance lead sits at every council, looking for
  a compliant way to yes; the Gaming Board is seated whenever a licence condition is touched, and
  it is not looking for anything. It rules on the plan as written — and it is required to be able
  to clear things, because a regulator seat that blocks everything teaches you nothing. A
  rehearsal, not regulatory advice
- **Bought growth versus built growth is the standing clash.** The Director wants to pay for FTDs;
  Product says fix the lobby and the funnel. Rival uses of the same money, and the verdict names a
  winner every time
- **The council is sized before it is seated.** Interest in a decision does not earn a chair; only
  changing the recommendation does
- **Someone has to want it.** One seat argues for the plan as written, or the verdict says why none
  would
- **No numbers, different question.** If cost per first depositor and NGR per player are unknown,
  the council stops judging the plan and says what to measure instead
- **Bets force commitment.** "It depends" is not a position
- **The evals test disagreement, not formatting.** A run can produce a flawless-looking verdict and
  still fail every case: unanimity, a regulator seat that blocks everything, and a council that
  cannot say yes to a good plan are all scored as failures

# Changelog

| Version | What changed |
|---|---|
| **1.8.0** | Head of Compliance & RG becomes the fifth standing seat. The Gaming Board moves to the dynamic roster, default-on in a regulated market whenever a licence condition is touched |
| **1.7.0** | Ships as a Claude Code plugin: `.claude-plugin/` manifests, the repo is its own marketplace, submitted to Anthropic's community directory |
| **1.6.0** | The Hard Number CFO (formerly Ruthless CFO) and a rebuilt Casino Director |
| **1.5.0** | ChatGPT build, roster tables and election rules in the README |
| **1.4.0** | Sizing tiers with the nine-seat cap, the two-question seating test, and the advocate rule — all three from the blind eval runs |

# Licence

MIT. Derived from Zapier's War Council, © 2026 Zapier, Inc., MIT. See `LICENSE` for both notices.
