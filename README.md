# Online Casino Council

*An agent skill for iGaming teams — a panel that stress-tests online casino decisions.*

An agent skill that convenes a panel of opinionated online casino personas to stress-test an
operator decision. Five standing members — a Ruthless CFO, a Casino Director from the grey market,
an External Consultant who has run this project at a dozen operators, a Head of Product & Game
Portfolio who thinks the lobby is a cheaper lever than the bonus, and the Gaming Board itself —
plus two to four experts picked for the specific problem. Each critiques the
plan, names the risk nobody is pricing, and bets on the outcome. An orchestrator reconciles the
disagreement into one recommendation.

It is a fork of Zapier's [War Council](https://github.com/zapier/wade-skills) rebuilt for online
gambling, where the numbers are NGR not revenue, the customers are FTDs not sign-ups, and the
regulator is in every meeting.

## What it is good for

- Market entry and licence applications
- Game provider contracts, exclusives, aggregator versus direct
- Bonus, loyalty and VIP programme design
- Affiliate deal structures
- Marketing budgets and channel mix
- Platform, PAM, CRM and vendor choices
- AI initiatives and vendor pitches

## Install

**Claude Code:** copy this folder to `~/.claude/skills/online-casino-council/` (global) or
`.claude/skills/online-casino-council/` inside a project. Invoke with `/online-casino-council`
or by saying "run the casino council".

**Cursor:** copy the folder to `.cursor/skills/`.

**Claude Projects, a custom GPT, any chatbot:** paste `SKILL.md` and `references/personas.md`
into the system prompt or project knowledge. The skill works without sub-agents; it just runs the
personas in sequence.

## First run

The council asks five questions about your operation — jurisdiction and regulator, products and
competitors, the numbers you are judged on, what you can decide, and your stack — and writes
them to a context file beside your work. Every later run reads that file. The more you give it,
the sharper the council gets; "don't know" is always an acceptable answer.

Your figures stay in your context file, never in the skill.

## Files

| File | Purpose |
|---|---|
| `SKILL.md` | The workflow. What the agent reads |
| `references/personas.md` | Full persona cards, read before briefing a seat |
| `assets/context-template.md` | The context file the setup writes |
| `references/example-verdict.md` | A complete run on a fictional operator |
| `evals/evals.json` | Nine test cases for checking changes. Each has `must` and `must_not` |

## Design notes

- **Flawed personas critique better.** Every card includes a failure. The CFO who approved a
  GGR-only case asks the question the successful one never does
- **Bought growth versus built growth is the standing clash.** The Director wants to pay for
  FTDs; Product says fix the lobby and the funnel. They are rival uses of the same money, and the
  verdict has to name a winner every time
- **Compliance is default-on, not standing.** In a regulated market every decision is a licence
  decision, so the seat is filled from the dynamic roster automatically — and the verdict has to
  say so when it is left empty
- **The regulator gets its own chair.** Your compliance lead is looking for a compliant way to
  yes; the Gaming Board is not looking for anything. It rules on the plan as written — and it is
  required to be able to say "we do not care about this", because a regulator seat that blocks
  everything teaches you nothing. A rehearsal, not regulatory advice
- **No numbers, different question.** If cost per first depositor and NGR per player are unknown,
  the council stops judging the plan and says what to measure instead. Judging an unpriced plan
  produces eight people finding the same hole
- **Bets force commitment.** "It depends" is not a position
- **The council is sized before it is seated.** Five, seven or nine seats — nine is a hard cap,
  and some questions get told they do not need a council at all. Interest in a decision does not
  earn a chair; only changing the recommendation does
- **Someone has to want it.** One seat argues for the plan as written. A panel where every seat
  is Against or Modified has stopped being a council and become a veto
- **The evals test disagreement, not formatting.** A run can produce a flawless-looking verdict and
  still fail every case: unanimity, a regulator seat that blocks everything, and a council that
  cannot say yes to a good plan are all scored as failures

## Licence

MIT. Derived from Zapier's War Council, © 2026 Zapier, Inc., MIT. See `LICENSE` for both notices.
