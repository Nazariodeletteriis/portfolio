# PuurSmile — AI Creative Naming

A system that watches an ad creative — frames and audio — and proposes a structured
name for it, in the company's own vocabulary, with the evidence that justifies every
term. A human approves or corrects.

## What it does

Ad creatives were named by hand and inconsistently. An audit of 1,700 existing names
found that roughly a third said nothing about what the video actually was, which made
performance reporting by creative angle unreliable.

The system ingests a creative from the team's existing tools, samples frames, detects
whether there is a voiceover, transcribes it, and proposes each part of the name with
a quote or a timestamp backing it. Nothing is published automatically: a reviewer
accepts or overrides in a console, and the system measures how often the proposal was
left untouched.

## My role

Sole developer: architecture, the ingestion pipeline, the model integration, the
review console, the accuracy reporting and the deployment.

## Stack

Next.js 15 (App Router) · TypeScript · PostgreSQL + Prisma · a separate worker
process · ffmpeg · Notion, Google Drive and Frame.io integrations · a vision-capable
LLM · Railway

## Engineering highlights

**The vocabulary is a constraint, not a suggestion.** Allowed terms are enforced
through a strict response schema generated from the company dictionary, so the model
cannot return a term that does not exist — and a second check runs on our side
anyway, because a guarantee shouldn't depend on a vendor's release notes.

**No evidence, no proposal.** A term that arrives without a quote or a timestamp is
discarded. A reviewer with nothing to check is a rubber stamp, which is the exact
failure this was built to prevent.

**Queue on PostgreSQL, no broker.** Jobs are claimed with `FOR UPDATE SKIP LOCKED`,
retried with a readable reason, and reclaimed if a worker dies mid-job. No Redis, no
extra infrastructure to run.

**Spend the tokens where the meaning is.** Frames are sampled densely over the first
seconds and sparsely after, because the creative angle is decided in the hook. Voice
detection runs locally through ffmpeg rather than paying a vendor to transcribe
silence.

**Measured, not assumed.** Every proposal records the prompt version behind it, and
a dedicated page reports how often reviewers kept each dimension as proposed — the
accuracy figure is what the approvers did, not an opinion about the model.

**Built for a European client.** Storage region and processor disclosure were design
constraints from the start, not an afterthought.

## Source code

Private — client work. Happy to walk through the architecture in a call.
