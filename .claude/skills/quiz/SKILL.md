---
name: quiz
description: Create, run and grade SAA-C03 practice quizzes from this vault's notes. Use when the user says /quiz, "quiz me", asks for practice questions, a mock exam, a drill on a topic, or to grade a quiz run.
argument-hint: "[quick|drill <topic|domain> [N]|mock|grade <folder>] [chat|file] [full]"
---

# Quiz

`QUIZ.md` at the repo root is the spec: question rules, file templates, grading, missed-question and progress tracking. This skill is the procedure. Where they disagree, `QUIZ.md` wins.

## Arguments

- Mode: `quick` (default), `drill <topic|domain> [N]`, `mock`, or `grade <folder>`
- Delivery: `chat` (default) or `file`
- `full`: draw on the whole exam guide, not only topics that have notes

If the user's wording doesn't match an argument ("give me 15 S3 questions"), map it (`drill s3 15`) and say which mode you chose.

## Create a run

1. `git pull --rebase origin main`.
2. Read `QUIZ.md`, `Quizzes/reference/EXAM-GUIDE.md`, `Quizzes/reference/SAMPLE-QUESTIONS.md`, `Quizzes/PROGRESS.md` and `Quizzes/MISSED.md`.
3. Choose the questions:
   - Fill the past-miss slots for the mode from `MISSED.md` (§4).
   - Fill the remaining slots to match the domain mix, giving more weight to weak and long-untested notes from `PROGRESS.md`.
   - Read every note you will base a question on. Base each question on facts actually in the notes; label it beyond-notes when the deciding fact isn't in any note.
4. Write all questions and the full key **before** showing anything. Check each question against `QUIZ.md` §2: Does the qualifier decide it? Does each distractor fail for exactly one reason? Is the correct answer not the longest? Are correct letters spread evenly? Is every service in scope?
5. Create `Quizzes/<folder>/QUESTIONS.md` and `ANSWERS.md`, then commit and push (`quiz: <folder> created`).
6. File delivery: tell the user the folder path, that they should tick boxes in `QUESTIONS.md` and not open `ANSWERS.md`, and to run `/quiz grade <folder>` when done. Stop there.

## Run it in chat

- Show one question at a time, exactly as written in `QUESTIONS.md` (header `Q01/10`). Accept answers like `B`, `b`, `A,D` or `a d`.
- **Don't write any files during a chat quiz.** Keep the answers in the conversation. Write all the ticks to `QUESTIONS.md` (`- [x]`) in one go at the end, just before grading, or earlier only if the user asks. Why: the repo's stop hook flags uncommitted changes after every reply, so editing files mid-quiz would force a commit and push after each answer.
- **Quick and Drill**: reply with ✅ or ❌, the correct letter(s) and **one line** on why. Give the full explanation from `ANSWERS.md` (why each wrong option fails, the deciding keyword, the note link) only if the user replies `why`. Then show the next question.
- **Mock**: no feedback until the end. Note the `started` time at the first question and the `finished` time at the last (use `date`), and write both to the frontmatter at the end. Mention the time remaining every 10 questions, counting down from 130 minutes.
- Never reveal or hint at the key before the user answers. If the user says `skip`, leave the question unticked (it counts as wrong). If they say `stop`, grade what's been answered and count the rest as unanswered.

## Grade

Follow `QUIZ.md` §6 for both chat runs (once the last answer is in) and `grade <folder>`:

1. Grade strictly from the ticks in `QUESTIONS.md` against the key in `ANSWERS.md`.
2. Write `RESULTS.md` and `REVIEW.md`, and update `MISSED.md` and `PROGRESS.md`. Append any note contradictions to `NOTE-ISSUES.md`.
3. Commit and push to `main` (`quiz: <folder> graded (<score>)`).
4. In chat, show the score, the per-domain breakdown, the missed concepts with their `[[note]]` links, and the folder path. Keep it short. The files hold the detail.

## Guardrails

- Never edit notes. Only `Quizzes/` is written.
- Never use exam dumps or reproduce real exam questions. Don't reuse the official sample questions as quiz questions.
- A run that has `RESULTS.md` is graded. Don't regrade it unless asked, and if you do, overwrite `RESULTS.md` and `REVIEW.md` and adjust the trackers.
