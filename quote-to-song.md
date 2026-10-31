---
name: quote-to-song
description: Transform collections of quotations, anecdotes, running jokes, and group-specific language into original, coherent, singable songs. Analyze themes and social dynamics, select varied source material, develop a musical concept, write lyrics, and optionally produce generator-ready style prompts, translations, and alternate edits.
---

# Quote-to-Song

## Purpose

Create original songs from a collection of quotations. Treat quotes as evidence of a shared world, not as a checklist of punchlines. Discover recurring themes, humor, relationships, conflicts, values, and emotional subtext, then transform these insights into memorable lyrics with musical direction.

Be independent of any particular organization, fandom, community, person, or scenario. Never import names, running jokes, or anecdotes from previous projects unless the current user supplies or explicitly requests them.

## Inputs

Accept any combination of:
- A raw quote collection (text, files, chat excerpts, notes, screenshots if readable).
- Background on the speakers, community, or setting.
- Desired subject, message, mood, genre, language, duration, and target music generator.
- Examples of previously successful or unsuccessful songs.
- Output constraints such as a maximum character count.

Start with the material available. Ask only when a missing detail would materially block the task; otherwise choose creative defaults and state important assumptions briefly.

## Workflow

### 1. Parse and understand the collection

Identify distinct quotations and, where available, their speakers and context. Preserve exact wording internally; do not confuse an original quotation with an interpretation. If the source is incomplete, mark the context as unknown rather than inventing a backstory.

For each useful quote, assess:
- **Literal meaning:** What is actually being said?
- **Possible subtext:** What does it suggest about shared habits, values, tension, or relationships?
- **Comic mechanism:** Absurdity, understatement, hyperbole, technical jargon, wordplay, incongruity, reversal, etc.
- **Musical potential:** Hook, call-and-response, narrative incident, verse detail, bridge revelation, or outro callback.
- **Accessibility:** Will outsiders understand it? Can the lyric supply context naturally?
- **Sensitivity:** Does it involve private information, an identifiable individual, protected traits, trauma, or a joke that might humiliate its subject?

Distinguish confident interpretations from speculative ones. Do not diagnose personalities or attribute private motives based on jokes.

### 2. Build a thematic map

Cluster the collection into a few useful themes: e.g., technical optimism, everyday mishaps, rituals, food, shared language, mutual support, creative chaos, or the tension between grand ambitions and trivial outcomes. These are examples, not predefined categories.

Identify recurring contrasts that could drive a song, such as:
- Expert knowledge versus ridiculous outcomes.
- Serious language applied to mundane events.
- Individual quirks versus collective belonging.
- Outward chaos versus inner reliability.
- Playfulness versus a sincere emotional core.

Form a one-sentence **song thesis**: what is the song really about? This should guide the choice of quotations, narrative progression, and refrain.

### 3. Curate quotations deliberately

Choose quotes that support the thesis, fit the rhythm, and complement one another. Do not simply insert the funniest lines in sequence.

Maintain variety across a multi-song project. Prefer underused quotes when earlier songs repeatedly relied on the same ones. Track usage within the available conversation or supplied catalog; never claim to have a complete history if it is unavailable.

Use quotes in three ways:
1. **Verbatim** when the wording is intrinsically musical or important.
2. **Adapted** when grammar, rhyme, meter, or translation requires it.
3. **Alluded to** when a direct quote would interrupt the song.

Never present an adapted or invented line as an exact quotation. Preserve the essential meaning of quotes unless the user explicitly requests surreal reinterpretation.

### 4. Design the musical concept before writing

Choose a genre and arrangement that enhance the material, rather than defaulting to the same sound every time. Define:
- Working title and language.
- Approximate BPM, groove, energy, and instrumentation.
- Vocal character, number of voices, and delivery.
- Narrative viewpoint and emotional trajectory.
- Main hook and chorus concept.
- Section structure and expected length.

Consider surprising genre/theme pairings when appropriate: a dramatic ballad about a small mishap, dance-pop about collective rituals, or cabaret about procedural absurdity.

If the user references a living artist, translate the request into broad musical attributes (groove, production, instrumentation, vocal dynamics, genre) rather than reproducing a recognizable artist's signature style or lyrics.

### 5. Write a coherent song

A useful default structure is:
`[Intro] → [Verse 1] → [Pre-Chorus] → [Chorus] → [Verse 2] → [Chorus] → [Bridge] → [Final Chorus] → [Outro]`

Vary structure when the genre demands it. A song should have progression:
- **Opening:** Establish the setting and invite curiosity.
- **Verses:** Introduce specific details, anecdotes, and escalating connections.
- **Chorus:** Express one strong, repeatable idea, not a catalog of references.
- **Bridge:** Add a meaningful reversal, vulnerability, or new perspective when appropriate; do not force sentimentality.
- **Ending:** Pay off a motif, return to an earlier image, or leave a memorable final line.

Favor vivid concrete images, internal rhythm, natural phrasing, and hooks that are easy to sing. Avoid clumsy rhyme, forced syntax, repetitive filler, and exposition that sounds like documentation. The listener should enjoy the song even without recognizing the source quotes.

### 6. Prepare generator-ready output

When the user intends to use a music generator, provide two separate copyable outputs:

**Lyrics**
- Include clear section markers such as `[Verse]`, `[Chorus]`, `[Bridge]`.
- Use concise English production cues in brackets if the generator accepts them.
- Keep sung words separate from stage directions.
- Do not add spoken sections by default. Spoken narration is opt-in; some generators turn it into shouting or exaggerated announcements.
- If a requested spoken segment is intentional, specify voice, language, delivery, and instrumental backing explicitly.

**Style prompt**
- Write a concise English production description covering genre, BPM, groove, instrumentation, vocal character, mood, dynamics, and key exclusions.
- Describe the sound concretely rather than relying on an artist's name.
- Avoid contradicting the lyric structure (e.g., "no speech" while the lyrics request a narrator).

Respect hard character limits by counting the actual lyrics including section markers. When close to a limit, shorten repeated choruses, commentary, and production cues before removing the story's essential beats. Do not claim a text is under a limit without checking it.

### 7. Multilingual songs and translations

Write idiomatic lyrics in the requested language. Prioritize natural syntax, singability, stress, and cultural fit over literal word-for-word conversion. Check that jokes and metaphors survive translation; adapt them when necessary without changing their core meaning.

For a requested **translation**, preserve the original song's meaning, structure, and tone; do not silently rewrite the story. Label a freer singable adaptation as an adaptation.

For alternating foreign-language singing and native-language commentary, use short alternating segments with explicit tags for singing, instrumental backing, and narration. Spoken commentary should summarize accurately and be shorter than the sung source. Check the combined character budget.

When a music generator mispronounces a recurring term, substitute a pronounceable synonym only if meaning and user constraints allow it.

### 8. Review and improve

Before delivery, verify:
- The song has a clear thesis, progression, and memorable hook.
- The quotations are diverse, contextualized, and not merely stacked.
- Adapted lines do not masquerade as verbatim quotations.
- The rhyme, stress, and phrasing are singable in the chosen language.
- The emotional register fits the brief; humor does not erase human warmth.
- The musical prompt matches the lyric arrangement.
- No unrequested spoken passages or intrusive stage directions appear.
- Names, private facts, and sensitive anecdotes are handled respectfully.
- Any stated hard length limit has been checked.

If the user reports generator results, treat that feedback as an empirical constraint. Revise the specific failure mode (pronunciation, spoken-vocal behavior, song length, pacing, genre realization) without discarding what worked.

## Output conventions

For a straightforward song request, output:
1. **Title and brief concept** (one or two sentences).
2. **Complete lyrics** with generator-friendly section tags.
3. **English style prompt** ready to copy.
4. **Optional short note** on an unusual creative choice, only if useful.

For an initial large quotation collection without a specific song request, provide a concise thematic analysis and two to four genuinely distinct song concepts; then invite selection. If the user asks to proceed immediately, choose the strongest concept and write the song.

For a request to analyze quotations only, stop after analysis; do not force a song.

## Creative principles

- **Meaning before quotation count.** More source quotes do not automatically make a better song.
- **Specificity before generic praise.** Small authentic details make a shared world believable.
- **Contrast creates humor.** Let lofty language collide with ordinary events.
- **Sincerity should be earned.** A heartfelt bridge works best when earlier scenes establish real connection.
- **Musicality matters.** Lyrics are intended to be performed, not merely read.
- **Experiment, observe, iterate.** Music generators are probabilistic; adapt to actual results.
- **Originality and respect.** Create new melodies and lyrics, avoid reproducing copyrighted songs, and don't make people the targets of gratuitous ridicule.
