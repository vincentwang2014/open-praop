# Contributing to Open PRAOP

## The one-line rule

> **Tell us what happened. You do not need to know what Open PRAOP calls
> it.**

You do not need to learn Open PRAOP's terminology before submitting. Your
job is to report the event. Classifying it — mapping it to an existing
pattern, deciding it's new, deciding it doesn't fit anywhere — is the
maintainer's job, not yours.

"I don't know what this is called, but here's what happened" is a
completely valid submission.

## What you can submit

- **A Case** — something that actually happened, in AI-assisted work.
  Failures, near-misses, and things that worked unusually well are all in
  scope. See `cases/TEMPLATE.md`.
- **A Practice** — a concrete recommendation, but only if it traces back
  to a case (yours or an existing one). A practice with no evidence link
  goes to Discussion, not straight into `practices/`. See
  `practices/TEMPLATE.md`.
- **A Playbook** — a workflow combining several practices. See
  `playbooks/TEMPLATE.md`.

## Before you submit: de-identify

Open PRAOP does not need your full raw material. Keep a private, complete
version for yourself if you want one; what you submit should have
identity and secrets removed while preserving the causal chain (what
happened, why, what changed).

**Remove entirely** (do not hash, do not obfuscate — delete): names,
emails, phone numbers, API keys, passwords, auth tokens, account numbers,
customer identifiers, private repo URLs, private IPs, internal endpoints,
unauthorized company or client names.

**Generalize** where the specific value isn't load-bearing for
understanding the failure: a person's name → "the operator"; a specific
credential name → "the credential" / "the authentication token"; a cloud
provider or internal project codename → a generic description of its
role; an exact dollar figure → a range, if the mechanism doesn't depend
on the precise number.

**Combination check:** even with every individual detail generalized, ask
whether someone who knows your company or industry could still
reconstruct who's involved from what's left. If yes, generalize further.

**Keep:** the original task, the timeline, what the AI/system actually
did, the cause/effect chain, the impact, what was tried, and the outcome.
De-identification should never cost you the failure shape — that's the
whole point of the submission.

If you can't share supporting evidence (logs, screenshots, commits)
publicly, that's fine — write "Evidence retained privately" rather than
omitting the evidence question. See §8 of the protocol for how evidence
levels work; a case with no attached artifact is still accepted, just
tagged `E0`.

## Submission format

Fill out `cases/TEMPLATE.md` (or the relevant practice/playbook
template). Two sections worth flagging:

- **What Happened Afterward** — pick one of: Resolved and verified /
  Improved but not fully verified / Failed / Recurring / Pending /
  Unknown. Writing a fix does not automatically mean "Resolved" — only
  mark that if the fix was actually verified against a recurrence.
- **Anti-Mapping Question** — "why might this case *not* be the pattern
  you think it is?" If you don't know, write "Unknown." This exists to
  cut down confirmation bias, not to make you defend your own
  classification.

## Workflow

```text
Read this guide
        ↓
Choose: Case / Practice / Playbook
        ↓
Fill the template
        ↓
De-identify (see above)
        ↓
Submit a PR or Issue
        ↓
Maintainer review
```

Maintainer review follows the six-step process in §13 of the protocol
(real-enough check, privacy check, fact/interpretation separation,
evidence tagging, mapping, accept-without-over-promoting), plus a
second-review gate for anything that changes Open PRAOP's own state
(pattern/practice promotion, contested/active/deprecated status changes).
Routine intake — accepting a well-formed, de-identified case — can happen
with one reviewer. You don't need to track this yourself; it's what
happens after you submit.

## License for contributions

Open PRAOP content is licensed under CC BY-SA 4.0 (see `LICENSE`). By
submitting a contribution (a case, practice, playbook, or edit) for
inclusion in this repository, you represent that you have the right to
submit it, and you agree that, if accepted, it may be distributed under
CC BY-SA 4.0 on the same terms as the rest of the repository. You keep
the rights to your own original contribution — this is a license grant
to the project, not a transfer of ownership.

## What accepting your case does and doesn't mean

Accepting your case means the event is clear enough to enter the case
library. It does **not** mean any pattern your case might support gets
promoted automatically. Evidence and theory are reviewed separately —
see §10's Anchor-or-Demote rule. A pattern needs more than one
compelling case to move past `Observed`.
