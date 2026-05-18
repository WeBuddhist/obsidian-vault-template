# CLAUDE.md — 🛤️ Railroads

Persistent operational instructions for an LLM agent working in this vault. Read before touching any file.

This file is the **operational quick-reference**. The canonical rules for each folder live in that folder's README:

- [`../1-SOURCES/About Sources.md`](../1-SOURCES/About%20Sources.md) — sources rules in full
- [`../2-RAILS/About Rails.md`](../2-RAILS/About%20Rails.md) — rails schema in full
- [`../3-TRANSFORMATIONS/About Transformations.md`](../3-TRANSFORMATIONS/About%20Transformations.md) — transformations rules in full

When this file and a folder README disagree, the folder README wins.

---

## 1. What this vault is

**Railroads** is a method for making AI-powered work on classical texts reliable. Instead of feeding a model raw commentary and hoping it synthesises correctly, we lay the **rails** first: structured, machine-readable context packages that resolve every ambiguity in a passage and cite the human source for each decision. Once the rails are laid, any model can run any transformation — translation, adaptation, lesson plan, daily reading, study guide, anything — without redoing the philological work.

Authority comes from the human commentary tradition, never from the LLM's parametric knowledge.

**One vault per text.** This vault is for **[name of text]**. For vault-specific conventions (addressing scheme, registered commentary IDs, language tracks), see [`Guidelines/vault-annex.md`](Guidelines/vault-annex.md).

---

## 2. Folder structure and citation chain

```
0-INBOX/        # drafts and scratch — not authoritative
1-SOURCES/      # human-produced material — read-only ground truth
  Text/         # root texts
  Commentaries/ # commentaries on the text
  Translations/ # existing translations (block-aligned with the root)
  References/   # dictionaries, secondary literature
  Audio/        # recitation and teaching recordings
2-RAILS/        # compiled interpretive context (primary work area)
  Sections/     # multi-commentary summaries per TOC node
  Verses/       # verse-level context files
  Local-Wiki/   # monolingual articles per key term
  Bilingual-Glossaries/ # bilingual descriptive glossaries per language pair
3-TRANSFORMATIONS/      # AI-generated outputs, organised in three categories
  Translations/ # language-by-language translation tracks
  Adaptations/  # audience-targeted retellings (children's, scholarly, …)
  Plans/        # calendar-driven study/practice arcs
4-SYSTEM/       # guidelines, skills, templates — read-only
```

### Citation chain — never skip a link

```
1-SOURCES/ → 2-RAILS/ → 3-TRANSFORMATIONS/
```

- `2-RAILS/` cites `1-SOURCES/` only — never another rail file, never parametric knowledge, never `3-TRANSFORMATIONS/`.
- `3-TRANSFORMATIONS/` cites `2-RAILS/` only — never reaching past the rails directly into the sources. (Plan tracks may also embed other completed `3-TRANSFORMATIONS/` outputs — recorded the same way in `context_packages:`.)

If a claim cannot be cited, do not make it. Leave the field blank and mark `status: draft`.

### Write permissions

| Folder | LLM may write? |
| ------------------- | ------------------------------------------------------ |
| `0-INBOX/` | yes — scratch only, never cited from elsewhere |
| `1-SOURCES/` | **no** — only metadata additions via skill workflows |
| `2-RAILS/` | yes — primary work area |
| `3-TRANSFORMATIONS/`| yes — only when explicitly instructed |
| `4-SYSTEM/` | **no** — rule changes require a human contributor |

The `1-SOURCES/` restriction is the most important. The folder receives human material once, has its block IDs and frontmatter added under controlled skills, and is then frozen. Adding interpretation here — even a paraphrase or a glossing parenthetical — corrupts the ground truth and breaks the citation chain.

---

## 3. Descriptive `2-RAILS/`, prescriptive `3-TRANSFORMATIONS/`

- **`2-RAILS/` is descriptive.** It distills and reformats what is already attested in `1-SOURCES/` — root text, commentaries, existing translations — without adding choices. Every claim cites a specific human source. The authority of a rail comes from the tradition it compiles, not from the LLM that compiled it.
- **`3-TRANSFORMATIONS/` is prescriptive.** It contains the choices that guide AI-powered output for *each particular track* — audience, register, the rendering chosen for every keyword, the per-session shape. Where `2-RAILS/` records what translators *have done*, `3-TRANSFORMATIONS/` records what *this* output *will do*.

---

## 4. File naming

- Lowercase, hyphenated, no diacritics in filenames. Diacritics fine inside file content and frontmatter.
- Language tag suffix on every file carrying language-specific material: `-pi` Pāli, `-sk` Sanskrit, `-bo` Tibetan, `-zh` Chinese, `-en` English. Add a script suffix when needed: `-sk-iast`, `-bo-wy`. Full tag list in [`../1-SOURCES/About Sources.md`](../1-SOURCES/About%20Sources.md) §12.
- Verse package files in `2-RAILS/Verses/` are named by block ID without the caret: `1-1.md`, `6-33.md`. Section files in `2-RAILS/Sections/` are named by node ID: `1.md`, `1-1.md`.
- Local-wiki files use `term_(disambiguating-phrase).md`.

---

## 5. Block IDs — the verse-level link

Every verse or discrete prose block in `1-SOURCES/` ends with an Obsidian block ID. This is the sole mechanism for cross-file references at the verse level across the vault.

```
[verse text here] ^1-1
```

- Format: `^chapter-verse` (most common), `^verse`, or `^book-chapter-verse` — declared per file in the `verse_id_format` frontmatter field.
- Numbers are not zero-padded. Use natural numbers (`^1-583`, not `^01-0583`).
- The vault annex ([`Guidelines/vault-annex.md`](Guidelines/vault-annex.md)) specifies the addressing scheme for the root text(s) of this vault.

Link form: `[[1-SOURCES/Text/[lang]-root-text.md#^1-1]]`
Transclude: `![[1-SOURCES/Text/[lang]-root-text.md#^1-1]]`

Use full paths in all `1-SOURCES/` and `2-RAILS/` files. Short wiki links are acceptable only inside `4-SYSTEM/` documentation.

---

## 6. `1-SOURCES/` — what you may and may not do

Files here are received material — formatted for navigation, never interpreted. Permitted additions only:

- Block IDs
- Frontmatter metadata
- Internal navigation links
- Editorial notes marked `[Ed:...]` (English, factual only)

Any interpretive claim — compound analysis, sense choice, syntactic reading — belongs in `2-RAILS/`, not here.

### Minimum frontmatter

```yaml
---
title:
author:
language:
file_type: root-text | commentary | translation | reference
lang_tag:
source_description: "where this text came from"
---
```

Add external IDs when available: `bdrc_work_id`, `cbeta_id`, `gretil_url`, `dsbc_url`, `suttacentral_id`, `acip_id`.

For commentaries and translations, also include `root_text:` (path) and `covers_verses:` (range, e.g. `1-1–1-1616`).

Full rules in [`../1-SOURCES/About Sources.md`](../1-SOURCES/About%20Sources.md).

---

## 7. `2-RAILS/` — what each subfolder produces

### `Sections/` — per-TOC-node summaries

Each node of the table of contents gets a summary in the original language drawn directly from each relevant commentary. Each commentary's summary is its own file under `Sections/Raw/<commentary>/`. The combined file `Sections/<node-id>.md` synthesises the per-commentary summaries and adds an English translation underneath.

Authoring skills: `section-summary-raw`, `section-summary-combined`.

### `Verses/` — per-verse context packages

One file per verse: `2-RAILS/Verses/<verse-id>.md`. Each package (1) transcludes the relevant commentary passages, (2) synthesises the commentators' interpretations in the original language, and (3) produces a **disambiguated restatement of the verse in the original language** — precise enough that no misreading or mistranslation is possible. Transformation skills work from this disambiguated version, not from the raw verse.

Only `status: complete` packages are used to generate transformations. Domain specialists set `complete` — the LLM never marks its own output complete.

Authoring skill: `verse-context`.

### `Local-Wiki/` — per-term articles

One page per attested sense ID within this text. Sense IDs are Wikipedia-style: `term (disambiguating phrase)`. Each article holds verbatim commentary quotations defining the term, a short contextual definition synthesised from them, and divergence flags where commentaries disagree. All content in the original language.

Authoring skill: `local-wiki-article`.

### `Bilingual-Glossaries/` — bilingual descriptive glossaries

One consolidated file per language pair: `[src]-[tgt].md`. Each entry maps a source lemma to every attested target-language rendering, frequency-ranked across all existing translations.

Raw inputs sit under `Bilingual-Glossaries/Raw/`: one interlinear gloss file per translation, and one per-translation raw bilingual glossary extracted from it. The consolidated file merges them.

Authoring skills: `interlinear-gloss`, `glossary-extract-raw`, `glossary-combine`.

---

## 8. Divergences — never flatten

When commentaries disagree, record the disagreement explicitly:

- Mark with ⚑ in any field where the divergence shows up.
- Add a `### Divergences` section attributing each position to its source.

If traditions teach genuinely incompatible doctrine on a verse, do not synthesise. Record both positions and add to frontmatter:

```yaml
transformation_note: "tradition must be specified for this verse"
```

---

## 9. `3-TRANSFORMATIONS/` — three categories, per-track governance

Three top-level categories, each a top-level subfolder:

- **`Translations/`** — language-by-language translations. Each track has `requirements.md` + `termbase.md` + the generated translation file(s).
- **`Adaptations/`** — audience-targeted retellings. Each track has `requirements.md` and optionally `termbase.md`.
- **`Plans/`** — calendar-driven study/practice arcs. Each plan has `requirements.md` plus calendar/days/communications/assets subfolders.

Every track is governed by binding contract files:

- **`requirements.md`** — style contract (audience, register, source-rail dependencies). Written in the target language.
- **`termbase.md`** — vocabulary contract (one chosen rendering per keyword). Required for Translation tracks, optional for Adaptation and Plan tracks.
- **`audience.md`** — audience profile (demographics, prior knowledge, use cases, motivations).

Do not generate from rails whose `status` is not `complete`.

Full rules in [`../3-TRANSFORMATIONS/About Transformations.md`](../3-TRANSFORMATIONS/About%20Transformations.md).

---

## 10. Style and language rules

- Analysis language is English throughout `2-RAILS/` (except per-commentary summaries and verse syntheses, which stay in the original language).
- Quote original-language terms in the appropriate romanisation or script — italicised on first use.
- **No parametric knowledge.** If you cannot cite a claim to a file in `1-SOURCES/`, do not include it.
- **No consensus flattening.** When commentaries disagree, say so.
- Present tense for analytical claims; past tense for historical statements.
- Use registered short IDs for commentaries throughout (e.g. the IDs in [`Guidelines/vault-annex.md`](Guidelines/vault-annex.md) §Commentaries).

---

## 11. Standard operations

**Ingest a passage**
1. Confirm the source is in `1-SOURCES/`.
2. Open or create the verse package in `2-RAILS/Verses/`.
3. Populate the synthesis, disambiguated restatement, and word/translation notes — each field cited.
4. Update or create local-wiki pages for any new sense IDs.
5. Flag divergences with ⚑.

**Lint a rails file**
- Any field in `2-RAILS/` without a `1-SOURCES/` citation → mark `status: draft`.
- Any ⚑ flag without a Divergences entry → add one.
- Any `status: complete` package that fails the checklist in `2-RAILS/About Rails.md` → revert to `partial`.

**Generate a transformation**
1. Confirm all relevant rails are `status: complete`.
2. Load `requirements.md`, `termbase.md`, and `audience.md` for the track.
3. For each batch: load section + verse rails → generate → record `context_packages:` in frontmatter → set `status: draft`.
4. Run `translation-qa` (or equivalent QA skill); iterate until no critical/major errors.
5. Domain specialist sets `status: complete`.
