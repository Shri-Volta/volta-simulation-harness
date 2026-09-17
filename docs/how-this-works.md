# How this works

What I understood after coming to this repository cold, installing it, authoring a case and
playing an attempt through to submission. Written as orientation for the next person who arrives
the same way. Corrections welcome — I am confident about what the harness does and much less so
about why particular decisions were made.

## Who uses it

Three people use this, and they use different parts of it.

| Person | What they do | What they use |
| --- | --- | --- |
| **Case author** | Writes a fictional problem: the people, what each of them knows, and the evidence that exists | A text editor and `npm run case:validate` |
| **Student** | Investigates the problem, decides what to do, and defends the decision | A command-line tool, inside their own Git repository |
| **Reviewer** | Reads what the student did and judges it | A web page, the staff workbench |

The student side is a command-line tool rather than a web application because a student is
expected to be working in their own repository with their own coding agent, and the tool has to
work the same way whichever editor or agent that is. The assignment is a folder.

## The journey

```text
AUTHOR     write the case ──> validate ──> approve ──> provision a private repository
                                                                    │
STUDENT    <── invited to their own repository ─────────────────────┘
           clone it, read START-HERE.md, sign in
                │
                ├── interview the people        (costs simulated time)
                ├── request existing evidence   (costs simulated time)
                ├── collect new evidence        (costs simulated days)
                └── record facts, assumptions, contradictions and unknowns
                │
           decide: continue · pivot · buy · collect more evidence · stop
                │
                ├── if the decision is to build: write real code, commit it
                └── submit ──> everything freezes, permanently
                                                                    │
REVIEWER   <── reads the whole timeline ────────────────────────────┘
           judges four competencies by hand. No score is generated.
           may reopen the attempt, which creates attempt 2
```

The author never meets the student, and the reviewer sees only what the student deliberately
recorded.

## What a session looks like

The student asks one specific question at a time and gets an authored answer back. Some answers
release an official fact with its source attached. Some answers are real but release nothing — for
example, a person saying they have never measured that.

Two rules do most of the work:

- **You cannot cite a fact you were not given.** Citing an unreleased fact ID is refused, so a
  plausible invented number cannot enter the record.
- **Arithmetic is recomputed, not trusted.** A calculation whose result does not follow from its
  stated inputs is refused before it is recorded.

Asking costs simulated time, so discovery has a budget. Choosing not to build, with a stated
reason, is a complete answer.

## What it is not

- It does not tell the student whether they are right.
- It checks that an answer is complete and reproducible. A human judges whether it was any good.
- It runs cases; it does not generate them. A person writes the case.
- It is not connected to anything real. No message is sent and no real system is changed.

## Where to go next

- **Try it:** `npm ci`, then `npm run pilot:local`. Keep that terminal open — it runs the service
  behind every student command — and use a second terminal for the student commands it prints.
- **Write a case:** [persona and buyer requirements](../packages/authoring/PERSONA-GENERATION.md),
  with `packages/authoring/test/fixtures/non-assessed-bicycle-library` as a complete worked example
  of the file layout.
- **Understand the boundaries:** [security model](security-model.md) and
  [delivery contract](delivery-contract.md).
