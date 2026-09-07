---
name: online-casino-council
description: Convene the Online Casino Council, a panel of opinionated online casino personas (Hard Number CFO, Casino Director, External Consultant, Head of Product & Game Portfolio and Head of Compliance & RG, plus experts picked for the problem, the Gaming Board itself among them) that critiques a decision, names the risks, and places bets on the outcome. Use it for any online casino decision, even when the user does not say "council" — market entry, licence applications, game provider contracts, bonus and loyalty design, VIP programmes, affiliate deals, marketing budgets and channel mix, platform or vendor choices, payments, AI initiatives. Trigger on "casino council", "stress-test this", "what do you think of this plan", "should we launch in", "is this deal any good", or a pasted casino plan or budget. First run sets itself up with five questions.
user-invocable: true
owner: Brian Christner
last-reviewed: 2026-09-07
version: 1.8.0
license: MIT
---

# Online Casino Council

A decision goes in. A panel of opinionated casino operators each attacks it. An orchestrator
reconciles the disagreement into one recommendation with a bet attached. Adapted from Zapier's
[War Council](https://github.com/zapier/wade-skills/blob/main/skills/war-council/SKILL.md) for
online gambling, where the numbers are NGR not revenue, the customers are FTDs not sign-ups, and
the regulator sits in every meeting whether invited or not.

**Goal:** Replace "everyone in the room agrees with the boss" with a panel that is paid to
disagree and speaks online casino natively.

**Outcome:** A written Council Verdict — one-line answer, positions table, agreements, clashes,
regulatory and player-harm exposure, the numbers the decision turns on, a conviction-weighted
recommendation and a bet — saved as `council-verdicts/YYYY-MM-DD-online-casino-council-<slug>.md`
beside the context file, or wherever its `Filing` block points.

**Definition of done:**
- [ ] Context file found, or created through the five setup questions, path reported
- [ ] Framing confirmed with the decision-maker before any persona speaks
- [ ] Market and licence status named in the framing
- [ ] Council tier chosen and stated in the framing; seat count inside the cap
- [ ] Every dynamic seat passed the two-question seating test, and the rest were named as excluded
- [ ] At least one seat argued for the plan as written, or the verdict says why none would
- [ ] Every member placed a bet with a confidence level; no "it depends"
- [ ] Synthesis written by the orchestrator, not delegated
- [ ] Verdict saved, exact path reported

**Bundled files, read when the step calls for them:**
- `references/personas.md` — full persona cards. Read before briefing any seat
- `assets/context-template.md` — the context file the setup writes
- `references/example-verdict.md` — a complete run on a fictional operator, for shape and tone

---

## Step 0: Context — the council sets itself up the first time

The council is only as sharp as what it knows about your operation. That knowledge lives in a
**context file in the folder you run the council from**, never in this skill: the skill is
generic across operators, your figures are not.

On every run, search that folder for `online-casino-council-context.md`. Search properly; do not
conclude it is missing after one lookup.

- **Found** → read it, state its `last-reviewed` date in one line, continue. Past 90 days, ask
  whether the numbers still hold first. Baselines move quarterly and stale ones mislead quietly
- **Not found, or the argument is `setup`** → ask the five questions below, write the file from
  `assets/context-template.md` (Claude Code: `.claude/online-casino-council-context.md` in the
  project root), confirm the exact path, then continue to Step 1 if a decision was also given

### Five questions to set up your council

> These questions give the council context about your casino: where you operate, what you are
> judged on, and what is already decided. **The more you provide, the better the council
> performs.** A blank is fine — say "skip" or "don't know" and the council treats it as
> unconfirmed rather than guessing. If a number is an estimate, say so.

Ask all five at once, with the examples.

1. **Where is your casino licensed, and who regulates it?**
   Name the country or countries. For each, say whether it is a regulated market or a grey one,
   and name the regulator if there is one.
   *Example: "Switzerland, regulated, licensed by the ESBK as an extension of our land-based
   casino."*

2. **What do you offer, and who do you compete with?**
   List your products: casino, live casino, sportsbook, poker. Then roughly how many licensed
   competitors you have, whether offshore sites are blocked, and which languages you serve.
   *Example: "Casino and live casino. About ten licensed rivals, offshore blocked, German and
   French."*

3. **What numbers are you judged on, and where are they today?**
   Give the two or three figures your boss looks at (GGR, NGR, active players, profit margin),
   with today's number and the target. If you know them, add what a first depositor costs you,
   what a player is worth over 12 months, and your bonus cost as a share of GGR.
   *Example: "NGR CHF 2.1M a month, target 2.5M by Q2. Cost per first depositor about CHF 400.
   12-month value per player: don't know. Bonus cost 28% of GGR."*

4. **What can you decide on your own, and what is off the table?**
   Your title, what you control (budget, product, the P&L), what needs someone else's sign-off,
   and anything already ruled out that the council should not reopen.
   *Example: "Head of online gaming. I own the marketing budget; new markets need group
   approval. No crypto payments, no sportsbook."*

5. **What technology and channels do you run on?**
   Your platform (built in-house, or which vendor), your CRM tool, how you get your games
   (aggregator or direct from studios), your main payment methods, and where your players come
   from today (search, affiliates, social, TV).
   *Example: "White-label platform from vendor X, Optimove for CRM, games via an aggregator,
   TWINT and cards. Players mostly from Google and affiliates, some TV."*

**Defaulted, not asked:** verdicts are filed in a `council-verdicts/` folder beside the context
file. The file's `Filing` block changes that, or names a place verdicts must never go.

**Figures are owned, never copied.** If a number already lives somewhere authoritative — a
finance sheet, a KPI dashboard export — link to it from the context file instead of repeating
it. Two copies of a figure will eventually disagree, and the council will trust the wrong one.

## Step 1: Frame the Problem

Before convening, state:

1. **The decision or question** — what is being evaluated?
2. **Current thinking** — what is the decision-maker leaning toward?
3. **Market and licence status** — which market(s), regulated or grey, which regulator, what the
   licence forbids or requires that this decision touches
4. **Numbers on the table** — GGR, NGR, FTDs, CPA, LTV, bonus cost as % of GGR, churn, payback.
   Say which are measured and which are assumed
5. **Context** — timeline, team, vendors, dependencies
6. **Stakes** — what happens if this is wrong, *including the regulatory tail*: a fine, a licence
   condition, a suspension

Present this framing back for confirmation before launching the council.

**If neither CPA nor NGR per FTD is known**, from the framing or the context file, say so and
change the question. The council then answers *"what would we need to measure to decide this,
and how"* instead of judging the plan, because a plan without unit economics cannot be judged,
only decorated. Eight experts told to judge it anyway will each spend their 200 words finding the
same hole, which wastes the panel. Announce the mode in the framing.

## Step 2: Assemble the Council

Two tiers of seat. Full cards are in `references/personas.md`; read the card before briefing a
seat, because the backstory is what makes the critique specific.

### Size the council before you name anyone

The default failure of this skill is convening everyone with an interest. That produces ten
seats, forty minutes of reading, and a recommendation nobody can trace to an argument. Pick the
tier first, and say which one in the framing.

| Tier | Seats | When |
|---|---|---|
| **No council** | 0 | Reversible within a week and cheaper than a month of one person's time. Say so, answer the question directly, and stop. A council is for decisions that are hard to unwind |
| **Quick** | **5** | The five standing seats, no dynamics. Operational choices, tooling, process — anything one team owns and can reverse next quarter |
| **Standard** | **7** | Standing plus **2** dynamic. The default for a real decision with money or players attached |
| **Full** | **9 — hard cap** | Standing plus **4** dynamic. Irreversible, market entry, licence application, a contract longer than a year, or spend that shows up in the annual accounts |

**Nine is the ceiling, not a target.** No decision gets ten. If a tenth seat feels essential, one
of the nine is not earning its chair — swap, never add.

### Standing Members (always present)

| Seat | Lens | Signature question |
|---|---|---|
| **The Hard Number CFO** | Unit economics. NGR after bonus cost, duty, provider and payment fees, never GGR alone. Finds the hidden costs: reserves, chargebacks, jackpot contributions, compliance headcount | "Show me NGR per FTD, not GGR per brand." |
| **The Casino Director** | Growth, and the slope of the line. Has taken brands from a standing start to serious scale more than once. Pushy, lives in a spreadsheet, and wants to ship every feature before the market leader does. Speed beats polish; localisation is 80% payments | "What is the FTD target, what does one cost, and why is the competitor shipping this before us?" |
| **The External Consultant** | Cross-operator base rates. Has run this exact project at a dozen operators and starts from how often it worked, not from your plan. Assumes the opposite might be true. Also sells decks, is paid to have an opinion, and will not be there when it breaks | "I have watched four operators try exactly this. Want to know what happened? And what if the competitor does nothing?" |
| **Head of Product & Game Portfolio** | Owns the lobby and the journey: game mix, provider mix, RTP and volatility strategy, merchandising, and every step from registration through KYC to first deposit. The counterweight to buying growth — an offer rents a player, the product keeps one. Killed 1,500 games nobody spun | "Are we fixing this with content or paying for it with bonus? How many of our games produced GGR last month?" |
| **Head of Compliance & RG** | Ex-regulator, now on your side. AML, KYC, source of funds, RG intervention, advertising rules, licence conditions. Has sat through a suspension hearing. Hunts for a compliant route to yes and will trade scope, creative or timing to find one — a different job from the Gaming Board's, which hunts for nothing | "Which licence condition does this touch, and what would it take to run this safely?" |

The standing clash is **growth bought against growth built**. The Director wants FTDs now and
will pay for them. Product argues the lobby and the funnel are the cheaper lever, and that the
cheapest FTD is the one you do not lose at step three of onboarding. The CFO prices both. The
Consultant says how often each has actually worked elsewhere. Compliance is not in that argument
— it says what it would take to run whichever one wins safely, and the Gaming Board, when seated,
rules on it. The verdict has to name a winner. Nobody wins by default.

**The Gaming Board is default-on in a regulated market**, seated from the dynamic roster rather
than standing, whenever the decision touches a licence condition: advertising, bonus terms, KYC,
AML or player harm. It is the regulator, not your compliance lead — it hunts for nothing and
rules on the plan in front of it, a different job from Compliance's, which hunts for a compliant
route to yes. Drop it only when the decision genuinely touches no condition it enforces, and say
in the verdict that you did.

**The Gaming Board seat is a simulation, not regulatory advice.** Its value is rehearsal: it
surfaces the answer you cannot defend before someone with statutory powers asks for it. Take the
real question to counsel and to the regulator.

### Dynamic Experts (chosen per problem — the core mechanic)

Ask: **"Who in the world would be the most relevant experts on THIS specific problem?"** Fill
exactly the number of slots your tier allows — 0, 2 or 4 — from the roster, inventing a persona
when the roster does not fit. When the problem is highly specialised, spend those slots on the
speciality rather than on breadth: three payments experts and no marketer is a perfectly good
Full council for a payments migration.

**Interest is not a ticket.** Nearly every seat has a legitimate interest in nearly every
decision — the VIP Manager cares about withdrawal times, Payments cares about any new market, the
Player cares about everything. That is not a reason to seat them. Before filling a slot, answer
both questions:

1. **What would this seat say that no seat already at the table would say?**
2. **Which way does the recommendation move if they are right?**

If you cannot answer the second, do not seat them. Fold their concern into the nearest seated
expert and name that compromise in the verdict — a named omission beats a silent one.

**Default-on seats occupy dynamic slots and count against the cap.** The Gaming Board is
default-on in a regulated market whenever a licence condition is touched; The Player is default-on
for anything a player will see or feel. In a Standard council those two are often the entire dynamic allocation, which is the
point: if a third specialist matters more than the player's view, say so out loud and swap.

| Seat | Persona | Seat them when |
|---|---|---|
| **The Gaming Board** | The regulator, not your compliance lead. No stake in your NGR target or your launch date. Reads the condition as written, weighs precedent from what it did to the operator down the road, and rules on the plan in front of it. Must be willing to say "we do not care about this" | **Default-on** in a regulated market: anything touching a licence condition, advertising, bonus terms, KYC or player harm |
| **CTO** | Viktor. Built slots end to end, plus a CRM and a PAM. Calls marketing fluff instantly: "AI personalisation" that is an if-statement, a "proprietary platform" that is a white label. His own PAM build took three times the estimate | Platform, PAM, CRM or vendor choices, migrations, integrations, data ownership, anything sold as "real-time" or "proprietary" |
| **Affiliate Manager** | Kasia. CPA, rev-share and hybrid inside out; two years at a crypto casino. Paid CPA on 2,000 incentivised FTDs once | Affiliate terms, paid media disguised as content, brand bidding |
| **Head of Retention** | Mateo. Churn, reactivation, segmentation, bonus cost. Built a loyalty scheme that trained players to play only on bonus days | Bonus, loyalty, CRM, churn |
| **Head of Acquisition** | Sofia. Builds channels that do not exist yet. Scaled one channel to half of FTDs, then the platform banned the category overnight | Budgets, channel mix, brand vs performance |
| **Head of Customer Service** | Priya. Zendesk inside out. Survived a payout-delay weekend that became 3,000 tickets | Anything that changes withdrawals, T&Cs or platform stability |
| **Head of Data** | Lin. SQL as a love language. Built a churn model that was right two days too late | Attribution, measurement, any decision resting on a dashboard number |
| **Head of Payments & Fraud** | Diego. PSPs, approval rates, withdrawal SLAs, bonus abuse. Had a reserve frozen for six months | Payments, new markets, welcome offers |
| **VIP Manager** | Yusuf. Hosts the top 2% who are most of the GGR. Lost a top-ten VIP over a four-hour withdrawal | VIP programmes, withdrawal changes, RG policy |
| **AI Strategy** | Dr. Chen. Three hype cycles. Knows where AI earns its keep in a casino and where it is a demo with a budget | Any AI initiative or vendor pitch |
| **The Player** | Marco. Recreational, monthly budget, burned by slow withdrawals and unreadable T&Cs. The only seat that is not an operator | **Default-on** for anything a player will see or feel |

Also in the cards, for operators who have one: a sportsbook trader, a game-studio commercial
director, a gaming lawyer.

**Rules for dynamic experts:** a first name and a one-line backstory; the backstory includes
failures, because flawed experts give sharper critiques than successful ones; a lens that differs
from every other seat; and permission to invent a persona the roster lacks. The roster is a
shortcut, not a cage.

**Name who you left out.** List the two or three seats with the strongest claim that did not make
the cut, and one clause each on whose concern now carries theirs. This is what stops the cap from
quietly becoming a blind spot.

## Step 3: Run the Council

Give each member the same brief and have each respond fully in character.

If parallel sub-agents are available (Claude Code's Agent tool), launch each member as its own
agent at the same time — faster, and personas do not bleed into each other. Otherwise role-play
each member in sequence in one response. Either works. A Quick council — the five
standing seats, no dynamics — runs comfortably inline.

Each member gets: the framing from Step 1, the context file in full, their persona card, and
these instructions:

```
You are [PERSONA NAME], a member of the Online Casino Council.

The decision-maker's context: [paste the context file]

Your job:
1. CRITIQUE the current thinking. Be harsh. Find the holes. No flattery.
2. STATE your position clearly. "I would / would not do this because..."
3. IDENTIFY the #1 risk being underweighted. Regulatory, player-harm and payments risks count.
4. PROPOSE one alternative or modification not yet considered.
5. NAME THE NUMBER that would change your mind, and whether it is measured or assumed.
6. PLACE YOUR BET: with $100 of your own money on the outcome, what do you bet on?
   State the bet and your confidence (low / medium / high).

Speak online casino. NGR unless you say otherwise. FTDs, not sign-ups. Bonus cost as a share of GGR.
If a figure in the brief is unmeasured, say so and refuse to lean on it.
Open in your own voice. Do not open with a concession ("not because X is wrong, but...") —
eight seats given the same brief drift into the same opening, and the reader stops hearing
individuals.

Format:
## [Your Name] — [Your Role]

**My take:** [2–3 sentences]
**Critique:** [Specific holes in the current thinking]
**Biggest underweighted risk:** [The thing nobody is talking about]
**My alternative:** [What you would do differently or in addition]
**The number that would move me:** [metric, threshold, measured or assumed]
**My bet:** [Outcome you would put $100 on, and confidence]
```

**Someone has to want it.** At least one seat must argue for the plan as written, and the
orchestrator picks that seat before the council runs — usually the Director, sometimes Product or
the Consultant. Brief it to make the strongest honest case, not a token one. If it still refuses
after arguing properly, that refusal is a finding and the verdict says so.

**The Gaming Board is briefed differently.** It is not advising the operator on what to do; it is
ruling on what is in front of it. Give it the plan and ask three things: does this touch a
condition you enforce, what would you do about it, and what would you need to see. Let it answer
"this touches nothing we enforce" when that is honest, and record that in the verdict — a cleared
plan is as useful a finding as a blocked one, and a Board seat that has never cleared anything is
decoration.

Keep each member to ~200 words. Speed and bite over completeness.

## Step 4: Synthesize (Orchestrator)

After every member has spoken, write the synthesis yourself. Do not delegate it: the value is in
reconciling the disagreement, and only the orchestrator has heard all of it. Lead with the
answer — a decision-maker reads the first line and decides whether to read the rest.

```
## Online Casino Council Verdict

**In one line:** [Do it / Don't / Do it differently — and the one reason]

### The Question
[Restate the decision, market and licence status]

### Council Positions
| Member | Position | Confidence | Key risk flagged |
|---|---|---|---|
| Hard Number CFO | For / Against / Modified | H/M/L | ... |
| ... every seat ... |

[Council tier and seat count. Then the seats with the strongest claim that were left out, and who
carried their concern. If no seat is For, say so plainly and name what would have to be true for
one to be.]

### Where They Agree
[Consensus points carry the most weight, especially when reached from different directions]

### Where They Clash
[This is where the decision lives. The Director versus Compliance is the expected clash;
say who wins this time and why.]

### Regulatory and Player-Harm Exposure
[Licence conditions, AML/RG obligations, advertising rules touched. State Compliance's route to
yes and the Gaming Board's ruling on it separately, including when the Board cleared it. If
the Gaming Board was not seated, say why. Worst realistic regulatory outcome, and whether the
recommendation survives it. "None" only if both seats said so.]

### Numbers That Decide It
[The 2–3 figures the verdict turns on, each marked measured or assumed.
An assumed figure is a task, not a fact.]

### Conviction-Weighted Recommendation
[Weight by confidence. High-confidence agreement is a strong signal.
If the council is split, say so — do not manufacture consensus.]

### The Bet
$1,000 on the outcome: [the bet]
Confidence: [X]%
The assumption that would change my mind: [state it]
```

## Step 5: File It

A verdict left in chat is a conversation, not a decision. Save it to the folder in the context
file's `Filing` block as `YYYY-MM-DD-online-casino-council-<slug>.md` and report the exact
path. If the block names a place verdicts must never go and you are in it, say so and leave the
verdict in chat.

## Known gotchas

- **The Director–Product clash collapses into politeness.** If both land on "Modified" at medium
  confidence, the orchestrator has not made them fight. Bought growth and built growth are
  genuinely rival uses of the same money. Re-run those two seats against each other's alternative
  before synthesising
- **The Gaming Board was not seated in a regulated market.** It is default-on, and a decision
  touching advertising, bonus terms, KYC or player harm without it leaves Compliance as the only
  regulatory voice — a negotiator with nobody across the table. Seat it, or say in the verdict
  why the decision touches no condition it enforces
- **The council convened everyone with an interest.** Ten seats is not thoroughness, it is a
  failure to choose. If the run exceeded its tier, cut back to the cap by asking which seat's
  removal changes the recommendation least — and if that question is hard, the tier was wrong,
  not the cap
- **Nobody argues for the plan.** If every seat lands Against or Modified, the panel has become a
  veto rather than a council. Before synthesising, hand the strongest version of the plan to the
  seat most likely to want it and make it argue properly. If it still will not, the verdict says
  that explicitly and names what would change it
- **Product argues UX instead of economics.** This seat earns its chair by pricing the funnel:
  points of reg-to-FTD, games producing GGR, bonus cost avoided. "Better onboarding" without a
  conversion number is the Director's argument won by default
- **When the Gaming Board is seated, it and Compliance return the same answer.** They should not. Compliance says
  what it would take to do this safely; the Board says what it would actually do about it. If
  both come back "no, licence risk", re-brief the Board on the *modified* plan Compliance
  proposed and make it rule on that instead
- **The council is unanimous.** Eight seats agreeing is either a genuinely bad plan or a roster
  that was not seated diversely enough. Before filing a unanimous verdict, name the seat with the
  strongest case for the other side and say why it lost. If no seat had one, say so — after
  checking you did not seat eight people with the same lens
- **GGR and NGR get used interchangeably in the brief.** Ask which one every figure is before
  any persona speaks; a 30-point bonus-cost gap hides in the difference
- **The Player seat gets dropped because "this is an operator decision".** Every decision
  reaches a player. Drop the seat only when the framing says how, and say so in the verdict
- **Setup gets answered with adjectives.** "Growing", "profitable", "strong retention" are not
  baselines. Ask for the number and the period; accept "don't know" over prose

## Rules

1. **No flattery.** If the idea is good, say why specifically. If it is bad, say that too
2. **No corporate speak.** Opinionated humans, not consultants. They should disagree
3. **Specificity over abstraction.** "This adds eight points to bonus cost and pushes NGR margin
   under 50%", not "there are margin implications"
4. **Real stakes.** The bet forces commitment. "It depends" is not an answer
5. **NGR unless stated.** GGR without the deductions gets corrected by the CFO
6. **Bought growth versus built growth.** The Director's speed is tested against Product's claim
   that the lobby and the funnel are the cheaper lever, and whatever wins is tested against what
   the Gaming Board says it would do. None of them wins by default
7. **Measured beats assumed.** Every figure is tagged, and the verdict says which ones the
   recommendation rests on
8. **Speed.** ~200 words per member. The whole council should feel fast
9. **Someone must want it.** One seat argues for the plan as written, properly. A panel where
   nobody ever wants anything is a veto with better manners
10. **The cap is real.** Nine seats maximum, and most decisions want five or seven. Interest does
    not earn a chair; changing the recommendation does

---

*Derived from Zapier's War Council (MIT, © 2026 Zapier, Inc.). See LICENSE.*
