# Case 005 — Trajectory Lock: Three Weeks Chasing a "Rate Limit" That Turned Out to Be a Twenty-Line Timeout Bug

**Status:** Accepted
**Evidence level:** E0 — Self-Reported
**Date:** ~2026-05
**Domain:** Software engineering — browser automation against a
third-party integration, small-business production system
**AI system involved:** A coding agent driving both the debugging
process and the automation being debugged
**Maps to:** candidate Pattern **Trajectory Lock** — not yet in
`../../patterns/` (this is its primary anchor; see
`PLAIN_LANGUAGE_GUIDE.md` Entry 12 for a second, smaller, independent
same-week incident of the same shape, described inline in this case)

### Plain-Language Version (人话版)

*Added by maintainer, per protocol §9 (Accepted cases should carry
one).*

A login automation kept failing, and each time an AI coding agent
proposed a fix, confirmed it worked, then watched it fail again —
until it settled on "the vendor is rate-limiting us" and spent three
weeks building progressively more elaborate workarounds (paid proxies,
a dedicated home-network device) that were never actually needed. It
broke only when a human asked the most basic possible question — would
a paying customer really get rate-limited that hard? — and the real
cause turned out to be a twenty-line timeout bug: the automation wasn't
waiting for the login code the way a human naturally would.

> De-identified per `../../protocol/open-praop-v0.1-final.md` §7 — the
> operator's name is removed throughout (→ "the operator"); the
> third-party rate-lookup platform is described only by function, never
> named; no customer or personal data is involved in this incident.

---

### A. Basic Information

**Case title:** Three Weeks Chasing a "Rate Limit" That Turned Out to
Be a Twenty-Line Timeout Bug
**Date:** ~2026-05
**Domain:** Browser automation integrating with a third-party
rate-lookup platform, small-business production system
**AI system involved:** A coding agent, both writing the automation
and diagnosing its own failures

### B. What Were You Trying to Do?

A small-business system automated a login-and-lookup flow against a
third-party platform that required paid-account access: log in,
navigate the site, and pull pricing data — a process a person would
otherwise do by hand. The login flow included an SMS-based two-factor
step. The goal was simply to keep this automated login reliable.

### C. What Actually Happened?

The login automation worked one day and failed the next, repeatedly,
over an extended period. Each time it failed, the coding agent
proposed a fix, applied it, confirmed it worked — and then it failed
again shortly after. At one point the agent concluded the third-party
platform was rate-limiting the account due to how it was being
accessed, and proposed progressively more elaborate workarounds:
routing traffic through paid proxy services, then through a home
internet connection (observed to have fewer restrictions), and
eventually setting up a dedicated small home computer as a permanent
proxy — which itself then needed its network configuration fixed
before it would work at all. Each fix moved further from the original
problem: what started as "why does login fail intermittently" became
"how do we get a home-network proxy device working." Over roughly
three weeks, most of the effort went into this proxy chain, and at no
point did anyone stop to ask whether the original "rate limit"
explanation was actually correct.

The explanation finally broke when the operator asked a basic
question: the account was a paying customer of the platform — why
would it be aggressively rate-limited at all? That question alone was
enough to make the "rate limit" theory feel implausible. Instead of
pursuing another workaround, the operator asked the agent to replicate
exactly what a human does when logging in manually through a browser:
receive the SMS code, then simply wait for it, typing it in whenever it
arrived. It turned out the automated version was not doing this — it
was measuring a fixed wait window and, if the code hadn't been
processed within that window, treating the attempt as failed and
backing off, which produced exactly the retry/lockout pattern that had
been misread as external rate-limiting. The actual fix — stop
enforcing an artificial timeout and just wait for the code the way a
human does — took a few dozen lines of code. It has run without a
recurrence since.

**A second, smaller, independent incident, same week:** while fixing an
unrelated search bug, the same coding agent again confidently attributed
the problem to an external vendor's site having changed, made three
separate edits chasing that theory, before the operator found the
actual cause was an internal code branch that had simply never been
tested.

### D. Why Did It Matter?

Roughly three weeks of engineering effort went into infrastructure
(proxy services, a dedicated home-network device, remote configuration)
that turned out to be entirely unnecessary — none of it was used in the
eventual fix. The underlying automation reliability problem remained
unresolved that entire time, and every day it stayed broken carried
real risk to a production business process.

### E. What Was Surprising?

At every step, the agent's proposed explanation was plausible, its
patches were competently executed, and progress felt like it was being
made — a proxy was found that seemed to help, for instance. Nothing
about the process looked like flailing; it looked like methodical
debugging. What made it hard to catch was exactly that competence: a
weaker, more obviously wrong series of patches would have prompted
reconsideration much sooner. The eventual fix required abandoning the
entire accumulated theory and going back to the most basic possible
question — not a more sophisticated diagnosis, a more naive one.

### F. What Did You Try?

In order: a series of code-level "fixes" that each briefly appeared to
work; a hypothesis that the account was being rate-limited due to
originating IP reputation; routing through paid proxy services; routing
through a home internet connection; provisioning a dedicated small
computer as a permanent home-network proxy; troubleshooting that
device's own network connectivity. None of these addressed the actual
cause. What worked: discarding the rate-limit theory entirely and
replicating the exact manual login timing a human uses.

### G. What Happened Afterward?

The fix has run without recurrence for over a month at the time of
writing (both the SMS-based path and a secondary notification path).
None of the proxy or dedicated-device infrastructure built during the
three-week period was used in the final solution.

### H. Evidence

Evidence retained only as the operator's own contemporaneous account
of the three-week period and the eventual fix. No externally
retrievable log or transcript is attached to this submission.

### I. Interpretation

This resembles a "locked inference trajectory" failure shape: once a
plausible-sounding explanation is adopted, an AI-driven debugging
process tends to absorb each new piece of contradicting evidence as a
reason to elaborate the existing theory further, rather than as a
prompt to re-examine whether the theory itself still holds. The lock
did not break from inside the process — every step of increasingly
elaborate patching felt locally reasonable — it required an external
interruption asking the most basic possible question. This is
interpretation, not confirmed general theory from one case; the second,
independent same-week incident above (same mechanism, much smaller
scale) is offered as a second data point, not proof.

### J. Anti-Mapping Question

Could this simply be "a hard bug that took a while to find," rather
than evidence of a distinct pattern? The specific, narrower claim being
made: it is not the difficulty of the underlying bug that's notable —
the actual fix was a few dozen lines and took minutes once correctly
diagnosed — it's that three weeks of increasingly elaborate, competently-
executed effort were spent *moving away* from the actual problem,
without anyone stopping to ask whether the founding assumption still
held. If the same three weeks had instead been spent on a series of
directly relevant, if unsuccessful, diagnostic attempts, that would
point to "hard bug," not "locked trajectory."

### K. What Would You Do Differently Next Time?

When a fix "works" and then fails again shortly after, treat that
specifically as a signal to question the original diagnosis — not as a
cue to patch further within the same theory. Before investing in
progressively more elaborate infrastructure to work around a suspected
external constraint, verify the constraint actually exists (in this
case: a single question — "would a paying customer really be
rate-limited this aggressively?" — would have raised doubt immediately).
When debugging automation meant to replicate a manual process, check
whether the automation actually replicates the manual process's timing
and behavior before assuming an external cause.

---

### Maintainer review notes

- **Real enough:** firsthand, contemporaneous incident with a concrete
  three-week timeline, a specific proxy-chain narrative, and a second,
  smaller same-week incident of the same shape. Passes.
- **Privacy:** de-identified per protocol §7 — operator name, platform
  name, and any account-identifying detail all removed or generalized.
  This is the richest and most detailed of the batch admitted in this
  round; flagged in its own submission notes as most worth extra
  scrutiny, and reviewed accordingly. Combination-risk checked and
  assessed as passing — an SMS-2FA login automation against an unnamed
  third-party platform describes a common automation architecture
  without naming the vendor, business, or any identifying technical
  specifics.
- **Fact vs. interpretation:** kept separate above (C vs. I) — the
  narrower claim ("competently-executed effort moving away from the
  problem," not "a hard bug") is explicitly distinguished from the
  broader "locked inference trajectory" interpretation.
- **Evidence:** E0, self-reported only, no attached log — evidence
  level tracks attachment, not narrative quality, though the level of
  procedural detail (the specific sequence of workarounds) is unusually
  concrete for E0.
- **Mapping:** New pattern candidate, **Trajectory Lock**, with two
  independent incidents in a single submission (the three-week saga and
  the same-week search-bug incident). Anti-mapping question is credible
  — distinguishes from "just a hard bug."
- **Confidence:** Case accepted; the pattern itself does not yet exist
  in `patterns/` — writing that file is the next step, out of scope for
  this admission. Whether the two incidents described in this one case
  file satisfy §10's "second independent incident" bar for `Emerging`
  (rather than being treated as one Accepted anchor) is a judgment call
  to make explicitly when the pattern file itself is drafted, not
  assumed here.
