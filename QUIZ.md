# QUIZ.md: SAA-C03 quiz spec

This file is the spec any agent follows to create, run and grade practice quizzes for the AWS Certified Solutions Architect – Associate (SAA-C03) exam from the notes in this vault. Claude Code runs it through `.claude/skills/quiz/SKILL.md` (`/quiz`). Other agents read this file directly.

References (read both before writing questions):
- `Quizzes/reference/EXAM-GUIDE.md`: domains, weights, task statements, in- and out-of-scope services
- `Quizzes/reference/SAMPLE-QUESTIONS.md`: the 10 official sample questions with pattern notes. This is the style bar.

## 1. Sources and grounding

- **The notes are the content.** Every `.md` file at the vault root is a study note. Its filename is its topic. Skip notes that hold no testable content (e.g. `Outline`, `Certifications Roadmap`, demo walkthroughs, command cheat sheets).
- **The exam guide is the structure.** It sets domain weights, task statements and which services may appear. Never write a question on an out-of-scope service.
- **No exam dumps.** Never reproduce or reconstruct real exam questions from dump sites. Write original questions in the official style.
- **Beyond-notes facts are allowed but labelled.** Ground questions in note facts where possible. When the fact that decides the correct answer is not in any note, mark the question `beyond-notes: yes` in the `ANSWERS.md` key. Wrong options may use general AWS knowledge freely.
- **Notes are read-only.** Never edit a note. If a note contradicts current AWS behaviour, don't build a question on the doubtful fact. Log it in the run's `REVIEW.md` and in `Quizzes/NOTE-ISSUES.md` (note, claim, why it looks wrong, suggested fix).
- **Domains are inferred per run** from each note's filename and contents. There's no static map. The domain given to each question is recorded in the key.

## 2. Question rules

Match the official style (see `SAMPLE-QUESTIONS.md` → *Style takeaways*):

- **Stem**: 2–6 sentences giving business context, the current architecture and the constraints, then one question line. Use official AWS short service names.
- **Every question is exam level.** Each is a scenario where you apply a concept. Never ask "What does X do?"
- **Qualifiers**: most questions hinge on one: *MOST cost-effective*, *LEAST operational overhead*, *MOST secure*, *highest availability*, *without downtime*, *minimal latency*, *with the fewest changes to the application*. Make the qualifier the thing that separates two otherwise workable options.
- **Types**:
  - Multiple choice: 4 options (A–D), 1 correct
  - Multiple response: 5 options (A–E) with 2 correct, or 6 options (A–F) with 3 correct; the stem ends "(Select TWO.)" or "(Select THREE.)"
  - About 20% of each run is multiple response
- **Distractors**: each one is a real, plausible AWS action that fails for exactly one identifiable reason:
  1. violates a stated constraint (cost, downtime, "private IP", "keys on premises", "cannot be interrupted")
  2. fixes the wrong component (scales the front end when the database is the bottleneck)
  3. doesn't work that way (writing to a Multi-AZ standby, a privilege that doesn't exist)
  4. only partly meets the requirement (one AZ for one tier, encrypts eventually rather than "at all times")
  5. works but loses on the qualifier (more expensive, more operational overhead)
- **Options** are similar in length and detail. The correct answer is not the longest. Spread correct letters roughly evenly across a run.
- **Combine notes on purpose.** Aim for at least a third of the questions to span two notes (e.g. S3 Replication + KMS, IAM Roles + Organizations/SCP, VPC Subnets + NAT Gateway + Route tables).
- **One concept tag per question**: kebab-case, specific enough to identify the fact tested, e.g. `s3-replication-not-retroactive`, `sse-c-keys-on-prem`, `ec2-hibernate-preserves-ram`. Missed-question tracking and progress use these tags, so reuse an existing tag from `Quizzes/MISSED.md` when testing the same concept.

## 3. Scope

- **Default**: questions draw on topics that have a note. Where the notes can't fill a domain's quota, use beyond-notes questions (labelled) on in-scope services rather than skewing the mix.
- **Full exam** (`full` argument): the whole exam guide. Every question whose topic has no note gets `beyond-notes: yes`, and `REVIEW.md` lists them under **Gaps: no note for X**.

## 4. Modes

| Mode | Questions | Mix | Past misses | Feedback |
|---|---|---|---|---|
| `quick` (default) | 10 | domain weights: 3 / 3 / 2 / 2; about 2 multiple response | up to 3 slots for active misses | after each question |
| `drill <topic\|domain>` | 10 (or N if given) | all on that topic or domain | that topic's active misses first, then new questions | after each question |
| `mock` | 65 | 19 / 17 / 16 / 13; about 13 multiple response | variants only, never word for word | only at the end; 130-minute budget |

Domain numbers: 1 Secure, 2 Resilient, 3 High-Performing, 4 Cost-Optimized.

**Including past misses**: take active entries from `Quizzes/MISSED.md`, oldest last attempt first. For each, either re-ask the original question word for word or write a **variant** (same concept tag, new scenario, new options). Rules:
- Quick and Drill: alternate. If the entry's last attempt was word for word, use a variant next.
- Mock: always a variant.
- Every entry needs at least one correct variant before it can be resolved (§7).

## 5. Run folder

```
Quizzes/
  PROGRESS.md              # scoreboard, links to runs
  MISSED.md                # active and resolved misses by concept tag, links into runs
  NOTE-ISSUES.md           # note contradictions found while writing or grading
  reference/               # exam guide + sample questions (read-only)
  YYYY-MM-DD-HHMM-<mode>[-<topic>]/
    QUESTIONS.md           # created with the quiz
    ANSWERS.md             # created with the quiz: key, rubric, explanations
    RESULTS.md             # created at grading; its existence means the run is graded
    REVIEW.md              # created at grading
```

- Folder names: lowercase, local time, topic slug in kebab-case (e.g. `2026-10-18-1530-drill-s3`, `2026-10-19-0900-mock`, `2026-10-20-2010-quick-full`).
- Markdown filenames are UPPERCASE.
- `PROGRESS.md`, `MISSED.md` and `NOTE-ISSUES.md` only summarise and link. Question text and explanations live only in run folders.
- **The answer key is written when the quiz is created**, so any later agent can grade from the files alone without knowing how the quiz was made.
- **Mode**: `chat` (default) or `file`. Both modes produce the same files. In chat mode the agent keeps your answers in the conversation and writes all the ticks to `QUESTIONS.md` at the end, just before grading (or earlier if you ask). It writes nothing mid-quiz, because the repo's stop hook flags uncommitted changes after every reply and would otherwise force a commit and push after each answer. In file mode you tick them in Obsidian, then ask for grading (`/quiz grade <folder>`).

### `QUESTIONS.md` template

```markdown
---
mode: quick            # quick | drill | mock
topic:                 # drill topic/domain, or "full"; blank for default scope
delivery: chat         # chat | file
created: 2026-10-18T15:30
started:               # mock only: when the first question was shown
finished:              # mock only: when the last answer was given
---

# Quiz 2026-10-18-1530-quick

Tick your answer(s). Multiple-response questions say how many to select.

## Q01

A company stores compliance documents in an S3 bucket in us-east-1 ... (stem)

Which solution meets these requirements with the LEAST operational overhead?

- [ ] A. ...
- [ ] B. ...
- [ ] C. ...
- [ ] D. ...

## Q02

... (Select TWO.)

- [ ] A. ...
- [ ] B. ...
- [ ] C. ...
- [ ] D. ...
- [ ] E. ...
```

Questions carry no domain, topic or retry hints. Those go only in `ANSWERS.md`.

### `ANSWERS.md` template

```markdown
# Answers 2026-10-18-1530-quick

## Key

| Q | Answer | Type | Domain | Task | Notes | Concept tag | Beyond notes | Origin |
|---|---|---|---|---|---|---|---|---|
| Q01 | B | MC | 1 Secure | 1.3 | [[S3 Replication]], [[Key Management Service (KMS)]] | s3-replication-sse-kms-config | no | new |
| Q02 | A, D | MR2 | 2 Resilient | 2.2 | [[EC2 Architecture and Resilience]] | ec2-az-failure-isolation | no | retry: [[Quizzes/2026-10-15-2100-quick/QUESTIONS#Q04]] verbatim |
| Q03 | C | MC | 3 High-Performing | 3.3 | — | aurora-replica-reader-endpoint | yes | variant of `rds-read-replica-offload` |

Grading: all-or-nothing. A question is correct only if the ticked set equals the answer set exactly.

## Explanations

### Q01: B
**Deciding keyword:** "LEAST operational overhead"
**Why B:** ... (1–3 sentences on the mechanism, citing the note fact)
**Why not A:** ... (the one reason it fails)
**Why not C:** ...
**Why not D:** ...
**Review:** [[S3 Replication]] → "Most encryptions work, SSE-KMS needs extra config"
```

`Origin` is `new`, `retry: <link> verbatim`, or `variant of <concept-tag>`.

### `RESULTS.md` template

```markdown
# Results 2026-10-18-1530-quick

Graded: 2026-10-18T15:52 · Score: 7/10 (70%) · Time: 22 min

| Q | Your answer | Correct | Result | Domain | Concept tag |
|---|---|---|---|---|---|
| Q01 | B | B | ✅ | 1 Secure | s3-replication-sse-kms-config |
| Q02 | A | A, D | ❌ | 2 Resilient | ec2-az-failure-isolation |

## By domain
| Domain | Correct | Total | % |
|---|---|---|---|
| 1 Secure | 3 | 3 | 100% |
...
```

Mock runs add the time used against 130 minutes and an **estimated** result. AWS scaling isn't public, so report the raw percentage and say whether it's in passing territory (≥ 72% raw is a rough heuristic only).

### `REVIEW.md` template

```markdown
# Review 2026-10-18-1530-quick

## Missed concepts
- **ec2-az-failure-isolation** (Q02): you picked A only and missed D. Re-read [[EC2 Architecture and Resilience]] → "..."

## Notes to revisit
- [[EC2 Architecture and Resilience]]

## Gaps: no note for X
- Aurora replicas / reader endpoints (Q03, beyond notes)

## Note issues
- (none) / [[Note]]: claim → why it looks wrong (also logged in NOTE-ISSUES.md)
```

## 6. Grading procedure (any agent, files only)

1. Read the run's `QUESTIONS.md` (ticked boxes are `- [x]`) and `ANSWERS.md` (key). Don't regenerate or second-guess the key. If the key looks wrong, grade by it anyway and flag the problem in `REVIEW.md`.
2. Score each question all-or-nothing. Unticked counts as wrong. The wrong number of ticks counts as wrong.
3. Write `RESULTS.md` and `REVIEW.md` from the templates.
4. Update `Quizzes/MISSED.md` (§7) and `Quizzes/PROGRESS.md` (§8).
5. Commit and push (§9).

## 7. `Quizzes/MISSED.md`

One row per concept tag, in two sections:

```markdown
# Missed questions

## Active
| Concept tag | Domain | Notes | First missed | History | Correct since last miss |
|---|---|---|---|---|---|
| ec2-az-failure-isolation | 2 | [[EC2 Architecture and Resilience]] | [[Quizzes/2026-10-18-1530-quick/QUESTIONS#Q02]] | ❌ 10-18 orig · ✅ 10-20 verbatim | 1 (0 variant) |

## Resolved
| Concept tag | Domain | Resolved | History |
|---|---|---|---|
```

- A wrong answer adds the tag to **Active**, or appends to its history and resets "correct since last miss" to 0.
- A correct answer on a tag that's already active increments the count and records whether it was word for word or a variant.
- **Resolved**: 2 correct answers since the last miss, at least 1 of them a variant. Move the row to **Resolved** with the date.
- A tag first answered correctly is never added.

## 8. `Quizzes/PROGRESS.md`

```markdown
# Progress

## By domain (all graded runs)
| Domain | Correct | Total | % | Exam weight |
|---|---|---|---|---|
| 1 Secure | | | | 30% |
| 2 Resilient | | | | 26% |
| 3 High-Performing | | | | 24% |
| 4 Cost-Optimized | | | | 20% |

## By note
| Note | Correct | Total | % | Last tested |
|---|---|---|---|---|

## Runs
| Run | Mode | Score | Weakest domain |
|---|---|---|---|
| [[Quizzes/2026-10-18-1530-quick/RESULTS\|2026-10-18-1530-quick]] | quick | 7/10 | 2 Resilient |
```

When picking new (non-retry) questions, give more weight to notes and domains with the lowest percentages and to notes not tested recently.

## 9. Committing

Quiz runs go straight to `main`. Pull first, then at creation (after `QUESTIONS.md` and `ANSWERS.md` are written) and again after grading:

```bash
git pull --rebase origin main
git add Quizzes/
git commit -m "quiz: <folder> created"   # or "quiz: <folder> graded (7/10)"
git push origin main
```

Never stage changes to notes. Quizzes never modify notes.
