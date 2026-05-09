# Content Format

This document defines the content format for the Formation Quest Library.

The quest library contains shared curriculum templates. It should not contain private student data.

The app imports these templates into a household database. Once imported, parents may locally edit templates without changing the upstream library.

## Core Vocabulary

Use these terms consistently:

- Daily Practice
- Quest
- Misogi
- Evidence
- Portfolio Item
- Formation Profile
- Archetype
- Theme
- Parent Review
- Student Reflection

Avoid these terms unless explicitly needed:

- assignment
- task
- badge
- grade
- leaderboard
- streak
- points

## Directory Structure

Recommended structure:

```text
docs/
  content-format.md
schemas/
  quest.schema.yaml
  misogi.schema.yaml
quests/
misogi/
archetypes/
themes/
memory/
rubrics/
parent-guides/
```

## Quest Files

A Quest is a one-week formative challenge that produces visible evidence and can be reviewed by a parent.

Each Quest should be concrete enough that the student knows exactly when it is finished.

### Required Quest Fields

Every Quest must include:

- id
- title
- archetype
- theme
- duration
- difficulty
- estimated_time
- tags
- why_it_matters
- instructions
- deliverables
- evidence_required
- finished_means

### Recommended Quest Fields

Quests may also include:

- source_module
- source_modules
- parent_notes
- safety_notes

### Quest ID Format

Use this format:

```text
quest.<archetype_or_domain>.<short_slug>.v<version>
```

Example:

```text
quest.aviator.aviation_control_surfaces_sketch.v1
```

Once published and imported, do not change the `id`.

### Quest Filename Format

Use lowercase, hyphenated filenames.

Good:

```text
aviation-control-surfaces-sketch.yaml
ham-radio-phonetic-alphabet.yaml
fungi-presentation-for-young-children.yaml
```

Avoid:

```text
Quest1.yaml
Kicker Quest FINAL.yaml
2026-05-05-placekicker.yaml
```

## Sample Quest

```yaml
id: quest.naturalist_teacher.fungi_presentation_for_young_children.v1
title: "Fungi: Teaching the Hidden Kingdom"
archetype: Naturalist-Teacher
theme: Creation and Wonder
duration: 1 week
difficulty: 3
estimated_time: 240
source_module: Nature Study
tags:
  - science
  - fungi
  - public-speaking
  - teaching
  - nature
  - service
why_it_matters: >
  Fungi are one of the hidden kingdoms of creation. Teaching young children about fungi
  trains the student to understand a subject well enough to make it simple, concrete,
  and full of wonder.
instructions:
  - Learn or review the basic life cycle of mushrooms: spores, mycelium, fruiting body, and spore release.
  - Prepare a short presentation for early childhood or kindergarten students.
  - Use simple language and concrete images.
  - Include at least one object, picture, drawing, or safe demonstration.
  - Teach three main ideas: mushrooms are fungi, much of the fungus is hidden as mycelium, and fungi help break things down so new life can grow.
  - Prepare 3 to 5 questions to ask the children.
  - Practice the presentation at least once for a parent.
  - After the presentation, write a short reflection on what went well, what surprised you, and what you would improve.
deliverables:
  - Simple presentation outline
  - Drawing, photo, object, or demonstration aid
  - 3 to 5 questions for the children
  - Practice presentation for parent
  - Final presentation
  - Short reflection afterward
evidence_required:
  - text
  - image
  - parent_observation
finished_means: >
  The student prepares and practices an age-appropriate fungi presentation, teaches the class
  using simple language and at least one visual or tactile aid, asks the children questions,
  and submits a short reflection afterward.
parent_notes: >
  For young children, the presentation should be concrete, visual, and brief.
  The student should not try to impress them with vocabulary. He should help them wonder.
safety_notes: >
  Only bring mushrooms or mushroom-growing materials that a parent and teacher approve.
  Do not allow children to eat, touch, or smell unknown wild mushrooms.
```

## Misogi Files

A Misogi is a 1 to 3 month formative challenge that builds real skill, courage, service, and portfolio-worthy evidence.

A Misogi should be difficult but attainable. It should produce a final artifact, demonstration, performance, service project, or presentation.

### Required Misogi Fields

Every Misogi must include:

- id
- title
- archetype
- theme
- duration_weeks
- difficulty
- formation_goal
- description
- weekly_milestones
- linked_quest_ideas
- final_artifact
- final_demonstration
- evidence_required
- parent_review_rubric

### Recommended Misogi Fields

Misogi files may also include:

- estimated_total_hours
- source_modules
- tags
- why_it_matters
- portfolio_description
- parent_notes
- safety_notes

### Misogi ID Format

Use this format:

```text
misogi.<archetype_or_domain>.<short_slug>.v<version>
```

Example:

```text
misogi.aviator.aviation_heritage_trial.v1
```

Once published and imported, do not change the `id`.

### Misogi Filename Format

Use lowercase, hyphenated filenames.

Good:

```text
aviation-heritage-trial.yaml
household-engineer-trial.yaml
household-readiness-medic-trial.yaml
```

Avoid:

```text
Misogi1.yaml
Big Challenge FINAL.yaml
```

## YAML Formatting Rules

To keep imports clean, follow these rules for every Quest and Misogi file.

### 1. Quote titles or field values that contain colons

Good:

```yaml
title: "Fungi: The Hidden Kingdom"
```

Bad:

```yaml
title: Fungi: The Hidden Kingdom
```

### 2. Do not include blank lines inside YAML lists

Good:

```yaml
instructions:
  - Prepare a short presentation.
  - Practice it once for a parent.
  - Give the presentation.
```

Bad:

```yaml
instructions:
  - Prepare a short presentation.

  - Practice it once for a parent.

  - Give the presentation.
```

### 3. Every Quest must include `tags`

Good:

```yaml
tags:
  - science
  - communication
  - teaching
```

Bad:

```yaml
# missing tags field
```

### 4. Keep `instructions`, `deliverables`, and `evidence_required` as YAML lists

Good:

```yaml
deliverables:
  - Presentation outline
  - Visual aid
  - Student reflection
```

Bad:

```yaml
deliverables: Presentation outline, visual aid, student reflection
```

### 5. Prefer simple lowercase tag names with hyphens if needed

Good:

```yaml
tags:
  - public-speaking
  - household-service
  - nature-study
```

Avoid inconsistent capitalization:

```yaml
tags:
  - Public Speaking
  - household service
  - NatureStudy
```

### 6. Use block scalars for longer text fields

For multi-sentence fields, prefer `>`.

Good:

```yaml
why_it_matters: >
  Clear communication matters when conditions are difficult, noisy, stressful, or urgent.
  Learning the phonetic alphabet trains precision, calm speech, and disciplined attention.
```

### 7. Add blank lines before array fields after block scalars

When an array field follows a block scalar field (like `why_it_matters: >`), add a blank line to ensure proper YAML parsing.

Good:

```yaml
why_it_matters: >
  This is a multi-line text field.
  It can span several lines.

instructions:
  - First instruction.
  - Second instruction.
```

Bad:

```yaml
why_it_matters: >
  This is a multi-line text field.
  It can span several lines.
instructions:
  - First instruction.
  - Second instruction.
```

### 8. Escape quotes in strings using single quotes

If a string contains double quotes, wrap the entire string in single quotes.

Good:

```yaml
instructions:
  - 'Create a chart with "Risks" and "Benefits" columns.'
```

Bad:

```yaml
instructions:
  - Create a chart with "Risks" and "Benefits" columns.
```

### 9. Keep field names stable

Use:

```yaml
why_it_matters:
finished_means:
parent_notes:
safety_notes:
evidence_required:
```

Do not invent alternate field names like:

```yaml
why_it_is_important:
completion_standard:
notes_for_parent:
required_evidence:
```

### 10. Run schema validation before importing when possible

Quest files should validate against:

```text
schemas/quest.schema.yaml
```

Misogi files should validate against:

```text
schemas/misogi.schema.yaml
```

## Pre-Import Checklist

Before importing a Quest or Misogi:

- [ ] File is valid YAML.
- [ ] Title is quoted if it contains a colon.
- [ ] No blank lines inside list fields.
- [ ] Required fields are present.
- [ ] Quest includes `tags`.
- [ ] `instructions` is a YAML list.
- [ ] `deliverables` is a YAML list.
- [ ] `evidence_required` is a YAML list.
- [ ] `finished_means` clearly defines completion.
- [ ] File passes schema validation.

## Content Quality Rules

Good content should:

- send students into the world to observe, make, serve, read, practice, write, speak, repair, or contemplate
- produce visible evidence
- include a clear standard of completion
- connect skill to character and service
- be concrete enough for a student to begin without confusion
- preserve parent authority and judgment
- include safety notes where appropriate

Avoid content that:

- creates busywork
- depends mainly on screens
- has vague completion standards
- rewards performance theater over real formation
- asks the student to research endlessly without making or presenting something
- bypasses parent review
- uses gamified language such as points, badges, streaks, or levels

## Evidence Types

Recommended evidence types include:

- text
- image
- image_or_pdf
- audio
- video
- audio_or_video
- audio_or_video_or_parent_observation
- file
- file_or_link
- link
- parent_observation

Use simple evidence names. If a Misogi requires richer artifacts, descriptive evidence names are acceptable, such as:

- project_notebook
- aircraft_sketch
- glider_test_data
- final_reflection

## Versioning

Use version suffixes in stable IDs:

```text
.v1
.v2
.v3
```

If a template has only minor spelling or formatting fixes, keep the same ID.

If the meaning, deliverables, duration, or completion standard changes substantially, create a new version.

Example:

```text
quest.aviator.aviation_control_surfaces_sketch.v1
quest.aviator.aviation_control_surfaces_sketch.v2
```

## Guiding Principle

These templates should help students become stronger, wiser, more useful, and more capable of loving what is good.

The app and the library exist to serve formation, not to manufacture activity.
