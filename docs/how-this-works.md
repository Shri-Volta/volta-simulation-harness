# How this works

A plain-English orientation for someone opening this repository for the first time.
Read this before the security model or the delivery contract.

## The problem this solves

Coding agents have made building cheap. When building is cheap, the expensive mistake moves
upstream: you build the wrong thing quickly instead of the wrong thing slowly.

So the scarce skill is no longer "can you build it". It is "should you, and how would you know".

That skill is the one nobody can practise. You can write code all day. You cannot practise a
discovery conversation, because every real one is with a real person whose time and goodwill you
spend once. Get it wrong and you do not get another attempt at that relationship.

This harness makes discovery repeatable and safe to get wrong. The people are fictional and
frozen. You can interview them badly a hundred times.

## Who it is for

Three different people use this, and they use different parts of it.

| Person | What they do | What they use |
| --- | --- | --- |
| **Case author** | Writes a fictional problem: the people, what each of them knows, and the evidence that exists | A text editor and `npm run case:validate` |
| **Student** | Investigates the problem, decides what to do, and defends the decision | A command-line tool, inside their own Git repository |
| **Reviewer** | Reads what the student did and judges it | A web page, the staff workbench |

The student side is deliberately a command-line tool rather than a web application. A student is
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

## What a session actually looks like

The student asks one specific question at a time and gets an authored answer back. Some answers
release an official fact with a source attached. Some answers are real but release nothing, for
example a person saying they have never measured that.

Two rules make the exercise work:

- **You cannot cite a fact you were not given.** Inventing a plausible number is rejected.
- **Arithmetic is recomputed, not trusted.** A calculation whose result does not follow from its
  inputs is refused before it is recorded.

Asking costs simulated time, so discovery has a budget. Choosing not to build, with a stated
reason, is a complete and valid answer.

## What success means

Two different things, and it is worth being clear which one is being discussed.

**Delivery success** is what the [delivery contract](delivery-contract.md) measures: a case can be
authored and approved, a student can complete an attempt blind, a reviewer can evaluate and reopen
it, official facts stay identical across two configured models, and protected material never
reaches the student.

**Learning success** is the point of the exercise: a student who has practised here makes a better
call on a real engagement. Nothing in this repository measures that. It is judged by the people
running the programme.

## What this is not

- Not a tutor. It never tells the student whether they are right.
- Not an assessor of quality. The tool checks that an answer is complete and reproducible.
  A human judges whether it was any good.
- Not a case generator. The harness runs cases; a person writes them.
- Not connected to anything real. No message is sent and no real system is changed.

## Where to go next

- Try it: `npm ci`, then `npm run pilot:local`. See the [README](../README.md).
- Write a case: [persona and buyer requirements](../packages/authoring/PERSONA-GENERATION.md).
- Understand the boundaries: [security model](security-model.md).
