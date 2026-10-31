---
name: quotes-to-album
description: Build a coherent original concept album or musical from a quote collection and a specified musical style, using the quote-to-song skill for each track. Develop an album bible, continuous plot, character arcs, recurring motifs, track-by-track lyrics, generator-ready prompts, and continuity checks.
---

# Quotes-to-Album

## Mission

Turn a collection of quotations, anecdotes and shared vocabulary into a **complete, narratively connected album**, based on the user's musical style brief. Every song must work on its own **and** advance a common story. Remain setting-agnostic: do not import names, jokes, places or plotlines from any previous project.

## Dependency: quote-to-song

Read and apply the installed `quote-to-song` skill (`SKILL.md`) before writing tracks. If the user refers to it as `quotes-to-song`, resolve the naming difference by looking for the installed equivalent; do not invent a tool or claim it was loaded when unavailable. If it cannot be found, proceed using the core process summarized here (interpret quotations, curate rather than stack, choose musical form, write singable original lyrics, produce English generator prompts, verify limits) and disclose the missing dependency briefly. **This skill extends, rather than replaces, quote-to-song.**

## Inputs

Required: (1) quotation collection or access to it, (2) musical style or style direction. The user may also specify album language, number of tracks, total runtime, setting, plot premise, narrator, cast, desired ending, target generator, lyrics character cap, and preferred workflow. Do not block on optional details: propose sensible defaults. If the collection is missing, request it; do not fabricate quotations.

Default: 8 tracks, 30–40 minutes, one central narrative, 2–4 recurring characters or roles, consistent sonic identity with deliberate variations, lyrics and English style prompts per track. When an album is too large for one response, deliver it in numbered batches with a persistent album bible and track status; never claim unwritten tracks are complete.

## Phase 1 — Interpret the source material

Apply `quote-to-song` analysis to the entire collection. Separate **verbatim quote**, **known context**, **interpretation**, and **fictional adaptation**. Group themes, rituals, conflicts, values, comic patterns and emotional undertones. Identify what can serve as an inciting incident, obstacles, running gags, character turning points, resolution and callback. Treat quotation attribution and personal/sensitive details carefully; do not invent real-world facts or assign unverified motives to identifiable people.

Build a **quote ledger** with fields: ID, exact wording, theme, potential dramatic function, sensitivity/context, proposed track(s), usage status (unused / verbatim / adapted / alluded). Distribute references throughout the album. Reuse only a few *intentional* motifs; don't recycle the same handful of punchlines in every track.

## Phase 2 — Design the album bible before lyrics

Create a concise, persistent **ALBUM_BIBLE.md** containing:

- **Logline:** one sentence explaining protagonist, goal, conflict and stakes.
- **Premise and rules:** setting, time span, degree of fiction, narrative perspective, tone and boundaries.
- **Character/voice roster:** goals, flaws, relationships, starting state, transformation, and who sings each part. Use fictional/composite roles unless the user authorizes identifiable depictions.
- **Three-act arc:** setup and inciting incident; escalating attempts and reversal; climax and resolution. Include emotional stakes, not just escalating absurdity.
- **Timeline and causal chain:** what changes between songs, what characters know, what remains unresolved.
- **Musical identity:** requested genre, BPM range, instrumentation, vocal palette, production traits, language and permitted stylistic deviations. Translate named-artist references into broad attributes; don't imitate an identifiable living artist's signature.
- **Leitmotifs:** 2–4 recurring lyrical phrases, sounds, melodic/arrangement concepts or objects, with planned changes in meaning across the story. Text prompts can request motifs, but a generator cannot guarantee identical melodies; for exact reprises use shared audio, stems or editing where available.
- **Track map:** title, act, plot beat, POV/singer, central quote IDs, musical variation, emotional state at start/end, transition into next track, planned duration.
- **Ending/payoff:** how the opening question, a recurring quote and the protagonist's arc resolve.

For a user who requests an album immediately, create the bible internally and give a compact summary, then begin writing. For a collaborative staged workflow, offer the track map for approval before drafting all songs. Don't turn a simple request into a long questionnaire.

## Phase 3 — Write a causal track sequence

Every track needs an **event**, a **choice or revelation**, and a **changed state**. Avoid a playlist of unrelated songs about the same setting. Use interludes, reprises, duets and perspective shifts only when they help the story. Make the conflict intelligible without knowledge of the original quotations. Preserve a few unanswered questions to create momentum; pay them off deliberately.

Suggested structure (adapt to style and number of tracks):

1. **Overture / world:** establish sonic motif, perspective and everyday order.
2. **Inciting incident:** something disrupts the world.
3. **First response:** characters pursue an imperfect solution.
4. **Escalation:** success creates a new problem; quote-based humor deepens.
5. **Midpoint / false victory:** a change in expectations or revelation.
6. **Crisis:** relationships, stakes or self-image are tested.
7. **Climax:** decisive choice; opening motif transforms.
8. **Finale / aftermath:** resolution, emotional payoff and final callback.

Do not force this template if the user asks for a different form, e.g. tragic opera, nonlinear narrative, episodic concept album, rock opera or suite.

## Phase 4 — Produce each track with quote-to-song

For every track:

1. Read its album-bible entry and the previous track's ending state.
2. Select fresh relevant quotes from the ledger; mark direct quotations versus adaptations.
3. Write a **track thesis** and one-sentence dramatic purpose.
4. Design a memorable hook that advances the track's conflict, rather than listing jokes.
5. Write complete original, idiomatic, singable lyrics with concise English section/production tags (`[Verse]`, `[Chorus]`, `[Bridge]`, etc.). Keep character voices consistent; differentiate them with vocabulary and musical register.
6. Produce a **separate English style prompt** for the target music generator. Preserve album-wide sonic identity while specifying the track's unique BPM, instruments, mood, vocal roles and arrangement. Avoid contradictory instructions.
7. Provide a **transition note**: unresolved plot point, motif, musical handoff, and the exact state the next track inherits.
8. Update quote ledger and album bible with any intentional changes. Never silently retcon prior events.

Spoken narration is opt-in, not a default. If requested, distinguish singing, spoken voice, and backing instrumentation explicitly. If the user requests alternating multilingual vocals and translation commentary, use short alternating sections and preserve the narrative meaning.

## Phase 5 — Production constraints

For Suno or similar generators, provide each track as two separately copyable blocks: **Lyrics** and **Style prompt**. Respect **per-track** limits, not just total album size. If Suno lyrics are capped at 5,000 characters, count all lyrics, whitespace and section tags; target <= 4,700 to leave a safety margin. Do not claim compliance without a real character count. Prefer concise tags, shorter narration and selective chorus repetition over losing key plot beats. Never cram an entire album into one lyrics field.

Specify musical consistency through shared production descriptors and recurring motif descriptions; add distinct track-level instructions. For seamless transitions or exact musical reprise, describe the intended edit/production handoff and acknowledge that separate AI generations may not maintain identical voices, melodies or timing. Suggest manual assembly only when it materially improves the outcome.

## Phase 6 — Continuity and quality gates

Before finalizing each track and again before finalizing the album, check:

- **Narrative:** Does each song change the situation? Are chronology, causality, character knowledge, motivations and ending coherent?
- **Source fidelity:** Are quote interpretations defensible, varied and properly labeled when adapted? Are sensitive jokes handled respectfully?
- **Musical coherence:** Does the requested style remain recognizable across tracks while energy and arrangement vary? Are recurring motifs intentional and transformed?
- **Lyric quality:** Natural language, singable meter, strong hooks, varied rhyme, no exposition dumps, no random quotation collage.
- **Generator readiness:** Tags unambiguous, no unwanted spoken passages, style prompt aligned with lyrics, actual character count checked.
- **Album payoff:** Opening motifs return meaningfully; humor and emotion are earned; the finale resolves the main dramatic question.

After user feedback from generated audio, record which arrangements, pronunciations, voice changes, transitions or prompts worked or failed. Revise specific tracks and propagate any plot changes to the bible and later tracks.

## Deliverables

For a full album request, produce these artifacts (as files when file tools are available, otherwise clearly separated Markdown):

- `ALBUM_BIBLE.md` — logline, act arc, characters, continuity, motifs, track map, musical identity.
- `QUOTE_LEDGER.md` — source quote IDs and per-track usage, distinguishing verbatim/adapted/alluded.
- `TRACKLIST.md` — ordered tracks with synopsis, duration targets, style variation and transition notes.
- `tracks/01-slug.md`, etc. — complete lyrics, separate English generator style prompt, plot purpose and transition notes.
- `PRODUCTION_NOTES.md` — generator constraints, album-wide sound, recurring motifs, recommended track order, assembly/transition guidance, revisions and QA checklist.

If asked only for a concept, stop after bible + tracklist; don't produce unsolicited full lyrics. If asked for a complete album, write all tracks or clearly label the work as partial and continue in batches when requested.

## Operating principles

**Story before setlist. Causality before references. Motifs before repetition. Individual songs before album uniformity. Source fidelity before invented backstory. Production constraints before delivery.**
