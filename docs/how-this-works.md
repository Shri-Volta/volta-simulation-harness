# How this works

What I understood after coming to this repository cold, installing it, authoring a case and
playing an attempt through to submission. Written as orientation for the next person who arrives
the same way. Corrections welcome — I am confident about what the harness does and much less so
about why particular decisions were made.

## The objective

Each simulation gives one student a realistic problem with **no prescribed solution**, and asks
them to decide whether it warrants a build, a smaller experiment, a purchase, more evidence, a
pivot or a stop — and to defend that decision with objective success and failure criteria.

What is being practised is judgment, not construction. A student is not marked on what they build.
They are marked on four things: whether the problem was worth acting on, whether the evidence was
sufficient and honestly separated from assumption, whether the proposed response was proportionate,
and whether success and failure were defined so that someone else could tell which had happened.

The people and evidence are fictional and frozen, so the same problem can be investigated badly,
then investigated again. Deciding not to build is a complete answer when the evidence supports it.

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

## How work moves between them

![Work moves from the case author through the harness to the student, whose frozen submission goes
to the reviewer. The reviewer may reopen the attempt. Protected case truth never crosses to the
student side.](images/handoff.svg)

The author never meets the student, and the reviewer sees only what the student deliberately
recorded. Everything to the right of the dashed line runs on released facts alone.

## The student's journey

![Seven stages in sequence: invited, set up, discover, record, decide, submit, await review.
Discovering and recording repeat until the evidence is enough.](images/stages.svg)

Discovery and recording repeat. Everything before submission is revisable; nothing after it is.

### 1. Invited

A private repository is created and the student is invited to it. They accept, clone it and open
`START-HERE.md`. The assignment is a folder — work in it with whatever editor or coding agent you
prefer.

### 2. Set up

A service starts and holds the simulation; a separate command-line tool talks to it. Start the
service in one terminal and leave it running, then sign in from a second terminal. **The first
terminal is the simulation** — closing it ends the session.

### 3. Discover

People answer from a frozen script. Some answers release an official fact with its source
attached; some are real answers that release nothing, for example a person saying they have never
measured that. Ask one specific thing at a time, request evidence sources, and schedule collection
where it is offered.

Every question spends simulated time. If an answer comes back empty, rephrase once, then record it
as an unknown and decide whether you can proceed without it.

### 4. Record

Reasoning becomes part of the submission as you go, not at the end. Log facts with citations, plus
assumptions, contradictions and unknowns, and add estimates and calculations.

Two rules do most of the work here:

- **You cannot cite a fact you were not given.** Citing an unreleased fact ID is refused, so a
  plausible invented number cannot enter the record.
- **Arithmetic is recomputed, not trusted.** A calculation whose result does not follow from its
  stated inputs is refused before it is recorded.

### 5. Decide

The attempt moves from discovery to a proposed response: a decision, a response plan with a
missing-data plan, objective criteria, and one claim per competency. Continue, pivot, buy, collect
more evidence and stop are all valid conclusions.

### 6. Submit

The case version, official events, released evidence, recorded reasoning and selected files freeze
together. `status` lists exactly what is still missing beforehand. Submission is permanent; further
changes need the attempt reopened, which creates attempt 2.

### 7. Await review

A reviewer reads the whole timeline and judges four competencies by hand. No score is generated,
and overall *effective* requires all four to be judged effective.

## Use cases

### UC-1 · Author a case

| | |
| --- | --- |
| **Actor** | Case author |
| **Goal** | Turn a realistic problem into a frozen, interviewable simulation |
| **Precondition** | A problem shape in mind. No real client material is used |
| **Trigger** | A cohort or engagement needs a practice problem |

**Main flow**

1. Frame the recurring problem without prescribing a solution.
2. Identify the economic, functional and technical buyers; write a private profile and jobs for each.
3. Write every fact once, with its source, in a single index.
4. Author routes: the phrasings that release each fact, with priorities and exclusions.
5. Author evidence and collection methods with their time and resource costs.
6. Write evaluation anchors and three calibration answers — strong, middling, weak.
7. Run `case:validate`; fix what it rejects; repeat.

**Alternate flows**

- *Validation fails* — schema errors name the field; cross-reference errors name the broken link.
- *Route validation fails* — the author's own test cases are re-simulated on import and must pass.

**Postcondition** — a case directory with three digests. Any material change produces a new version
and clears approval.

### UC-2 · Complete an attempt

| | |
| --- | --- |
| **Actor** | Student |
| **Goal** | Decide whether the problem warrants action, and defend it |
| **Precondition** | Assigned to a private repository; the case is approved and frozen |
| **Trigger** | Invitation accepted |

**Main flow**

1. Sign in, pairing the folder to the assignment.
2. `status` — brief, constraints, people, sources, and what submission requires.
3. Interview people and request evidence; answers may release official facts with provenance.
4. Collect new evidence where authored; simulated days pass.
5. Record facts with citations, plus assumptions, contradictions and unknowns.
6. Record estimates and calculations; the service recomputes the arithmetic.
7. Assess requirements; record a decision, a response plan and objective criteria.
8. Claim all four competencies; submit.

**Alternate flows**

- *Question matches nothing* — an explicit unavailable result; no facts released, no state change.
- *Unreleased fact cited* — refused; only released facts can be cited.
- *Arithmetic inconsistent* — refused before recording; nothing is saved.
- *Command retried* — the same operation ID returns the existing result rather than duplicating it.
- *Risky action* — staff review is suggested, never required; sandbox work continues.
- *Attempt already submitted* — further actions are refused until the attempt is reopened.

**Postcondition** — an immutable submission, reproducible from its recorded inputs.

### UC-3 · Evaluate an attempt

| | |
| --- | --- |
| **Actor** | Reviewer |
| **Goal** | Judge effectiveness, and say why |
| **Precondition** | A submission exists; the reviewer is authorised for that case |
| **Trigger** | Submission accepted |

**Main flow**

1. Open the assignment; read the timeline with fact IDs and provenance.
2. Read the recorded reasoning: ledger, estimates, calculations, criteria, claims.
3. Rate each of the four competencies with a written rationale.
4. Overall *effective* only where all four are effective. No score is generated.
5. Optionally reopen the attempt, creating attempt 2.

**Alternate flows**

- *Replay* — re-render a response against the frozen facts; wording may differ, the facts cannot.
- *Correction* — creates a linked new record; earlier records and digests stay recoverable.

**Postcondition** — an immutable evaluation attached to that submission.

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
