# Grammar Adventure for Penny — Product Requirements Document

## 1. Overview
A single-page HTML app (runs locally in browser on Mac, no install needed) that teaches English grammar to a 5.5-year-old preparing for Primary 1 (Singapore syllabus) through playful, game-style interactions. No formal "lessons" — concepts are taught implicitly through repetition, feedback, and fun visuals.

## 2. Goals
- Make grammar practice feel like play, not homework
- Build foundational skills for Primary 1, following a 12-unit grammar syllabus (see section 6a), starting with Unit 1: Common & Proper Nouns and Unit 2: Singular & Plural Nouns
- Easy for a parent to run on Mac by double-clicking a file (open in Chrome/Safari)
- Easy to extend with new units later

## 3. Target User
- Penny, age 5.5, pre-reader/early reader — needs large text, audio cues optional, simple instructions (can be read aloud by parent initially)
- Parent (Julian) operates/launches the app, may sit alongside

## 4. Platform & Tech
- Single self-contained `index.html` (HTML/CSS/JS, no build step, no server)
- Opens directly in a browser on Mac (double-click)
- Works offline
- Cute cartoon/animal theme: bright colors, friendly character mascot (e.g., a panda or fox guide), simple illustrations (emoji or SVG to avoid needing image assets)
- Responsive enough for laptop screen + trackpad/mouse; touch-friendly if used on iPad too

## 5. Interaction Modes
Mix of interaction types across activities, so it stays varied:
- **Tap/click** — select correct picture/word from options
- **Drag & drop** — sort items into bins (e.g., "naming words" vs "not naming words")
- **Typing** — type a missing word (with on-screen letter hints)
- **Circling/highlighting** — click to circle the correct word(s) in a sentence (visually highlights on click)
- **Drawing** (stretch) — simple canvas where Penny can draw the noun she picks (optional, lower priority)

## 6. Structure
- **Home screen**: mascot greets Penny, shows unit selection as big friendly buttons ("Unit 1: Naming Words", "Unit 2: A, An, The & More")
- **Each unit**: a sequence of 5–8 short game-style activities (rounds), each ~1–2 minutes
- Instant feedback: correct = cheerful animation/sound + mascot celebration; incorrect = gentle encouragement, show correct answer, try again
- End of unit: a simple "star rating" or sticker reward screen (no harsh scoring — keep it positive/low-stakes)
- Progress is NOT required to be saved across sessions initially (stretch goal: localStorage to remember stars earned)

## 6a. Full Syllabus Roadmap (Word Valley map)
Based on the reference grammar workbook's table of contents. Each unit becomes one chapter/location in Word Valley with its own companion animal. Units 1-2 are built first (v1); the rest follow the same engine/template.

| # | Unit (workbook topic) | Word Valley location | Companion | Progress mechanic |
|---|---|---|---|---|
| 1 | Common & Proper Nouns | Lily Pad Pond | Frog | Hop across lily pads |
| 2 | Singular & Plural Nouns | Hurdle Meadow | Bunny | Hop over fence hurdles |
| 3 | Possessive Nouns | Echo Cave | Bat | Fly between glowing crystals |
| 4 | Personal Pronouns | Mirror Lake | Otter | Swim between floating rings |
| 5 | Possessive Pronouns | Treasure Cove | Crab | Scuttle across stepping shells |
| 6 | Indefinite Pronouns | Mystery Forest | Owl | Glide between tree branches |
| 7 | Demonstrative Pronouns | Lookout Hill | Eagle | Soar between cloud platforms |
| 8 | Interrogative Pronouns | Question Falls | Parrot | Hop across waterfall rocks |
| 9 | The Articles (a, an, the) | Sunflower Field | Bee | Buzz between flowers |
| 10 | Subject-Verb Agreement | Bridge Crossing | Turtle | Cross floating bridge planks |
| 11 | Action Verbs | Race Track | Cheetah | Dash between track markers |
| 12 | Verbs - Am, Is, Are | Sky Harbor | Bluebird | Hop between cloud steps |

## 7. Unit 1: Common Nouns & Proper Nouns
Concept: naming words (common nouns) vs. special names that need a capital letter (proper nouns) — e.g., "park" vs. "Changi Airport", "boy" vs. "Mr Wong"

Based on a reference workbook with 3 worksheets — each worksheet becomes one "level" (one stretch of lily pads) within the chapter, each with its own interaction style so the unit feels varied:

### Level 1 — "Everyday word or special name?" (from Worksheet 1)
Source: 10 words (park, Mr Wong, girl, boy, computer, water bottle, Changi Airport, Pastor Tay, Mrs Ismail, etc. — swap "gun" for a kid-friendly item like "kite")
- Interaction: one word shown at a time on a big card; Fennick asks "Is this an everyday word or someone/somewhere's special name?"; Penny taps one of two large lily-pad buttons — "Naming word" vs "Special name" (with a capital-letter icon)
- Correct → frog hops to next lily pad; card flips to reveal a fun fact/picture for proper nouns (e.g., Changi Airport = plane icon)

### Level 2 — "Fill the gap" (from Worksheet 2)
Source: 10 sentences with a missing noun and a word bank (rabbits, scarf, boy, car, sister, May Lin, clinic, mother, Mr Wong, children)
- Interaction: sentence shown with a blank and a picture hint; word choices appear as draggable lily pads at the bottom — Penny drags (or taps) the correct word into the blank
- Sentence is read aloud; correct word animates into place and the sentence is read again with the word filled in

### Level 3 — "Sort the nouns" (from Worksheet 3)
Source: word list (mouse, book, pen, magnifying glass, skateboard, Mr Heng, Beijing, Orchard Road, cap, Joan, zebra, school) sorted into 3 categories: Person/Animal, Thing, Place
- Interaction: each word appears one at a time as a card with a small picture; three labeled baskets/lily groups ("Person or Animal", "Thing", "Place") sit at the bottom; Penny drags or taps the card toward the matching basket
- Frog hops forward with each correct placement; this level has more rounds (12 items) so hops are slightly smaller/more frequent

### Level 4 — "Capital letter hunt"
- Interaction: a short sentence is shown containing one proper noun written in lowercase (e.g., "we went to changi airport"); Penny taps the word(s) that need a capital letter; tapped letters animate to uppercase
- Reinforces the common/proper distinction from Levels 1-3 in context (within a sentence, not just isolated words)

### Level 5 — "Mixed pond review"
- Interaction: a quick-fire mix of question styles from Levels 1-4 (one tap-to-classify, one fill-the-gap, one sort, one capital-letter-hunt), randomly drawn — like a "boss level" before the chapter ends
- Acts as a light recap/check; same low-pressure feedback rules apply (no visible scoring, just hops forward)

General notes for all levels:
- Each unit has **5 levels**, each its own stretch of lily pads/hurdles with its own progress tracker (e.g., "Level 1: pad 3 of 10")
- **Level length is flexible, not fixed** — the number of pads/hurdles in a level simply equals the number of questions/items in that level's data array (e.g., Level 1 = 10 words → 10 pads; Level 3 = 12 items → 12 pads; Level 5 "mixed review" can be shorter, e.g., 4-6 items). Don't hardcode a count of 5 or 8 — the progress track renders dynamically from `data.length`
- Completing all questions in a level completes that level's stretch; completing all 5 levels completes the chapter and triggers the chapter-end celebration
- Content lists above are starting data; easy to localize/adjust names (e.g., swap in Penny's family/friends' names) since each level is just a data array — adding/removing items from the array automatically resizes the path

## 8. Unit 2: Singular & Plural Nouns
Concept: one thing (singular) vs more than one (plural) — regular -s/-es plurals first, a few common irregulars (e.g., child/children, mouse/mice) as a stretch

Five levels, each its own stretch of fence hurdles for the bunny:

### Level 1 — "One or many?"
- Interaction: a picture is shown (1 cat vs 3 cats); Penny taps the "one" hurdle or the "many" hurdle to match the picture
- Builds the core singular/plural distinction before introducing spelling

### Level 2 — "Add the -s"
- Interaction: a picture + singular word is shown (e.g., "cat"); Penny taps/drags letter tiles ("s") onto the end of the word to build the plural ("cats"); word is read aloud before and after
- Covers simple -s first, then -es for words ending in s/x/ch/sh (e.g., box → boxes) as later rounds

### Level 3 — "Sort it out"
- Interaction: word+picture cards appear one at a time; two hurdle baskets labeled "one" and "more than one"; Penny drags or taps each card to the matching basket
- Mix of regular plurals and a couple of irregulars (e.g., child/children) introduced visually here first

### Level 4 — "Spot the plural"
- Interaction: a short sentence is shown (e.g., "The children play with two balls"); Penny taps the word(s) in the sentence that are plural; tapped words highlight
- Reinforces recognizing plurals in context, including irregulars

### Level 5 — "Mixed meadow review"
- Interaction: quick-fire mix of question styles from Levels 1-4 (one/many picture, add -s, sort, spot-the-plural), randomly drawn — "boss level" before the chapter ends
- Same low-pressure feedback; bunny reaches the carrot patch at the end for the chapter celebration

## 9. Animation & Motion
- Lightweight CSS/JS animations (no Flash — deprecated/unsupported; replicate the effect with CSS keyframes, transitions, and simple SVG animation)
- Mascot bounces, waves, or jumps on correct answers; shakes gently/looks sad on incorrect
- Items animate when dragged, dropped, or tapped (scale/wiggle for feedback)
- Confetti or star-burst animation on unit completion
- Transitions between activities (slide/fade) to keep it feeling dynamic
- Keep animations short (<1s) so pacing stays snappy for a 5-year-old's attention span

## 10. Visual & Audio Style
- Cartoon mascot (consistent character) gives instructions and reactions, using simple text + large emoji/SVG faces
- Color palette: bright pastels, rounded buttons, large kid-friendly font (e.g., Comic Sans MS or similar rounded font)
- Optional sound effects (chime for correct, soft "try again" for incorrect) — togglable, default on
- All text large (min ~24px) and short — sentences Penny can have read to her or sound out

## 8a. Story & Narrative Framing
An overarching story ties units together so Penny feels like she's on one continuing adventure, not separate drills.

**Premise**: "Word Valley" is missing its words — a mischievous cloud (Grumble) has scattered them across the valley. Penny's guide, Fennick the fox, asks for her help to find and sort the words and restore each part of the valley.

- Each unit = one "chapter"/location in the valley, with its own short story intro (2-3 simple sentences + illustration, narrated/read aloud). See section 6a for the full 12-chapter map.
  - **Unit 1 (Common & Proper Nouns)**: "Lily Pad Pond" — naming words have fallen into the pond as lily pads; Fennick (as a frog companion for this chapter) hops across by picking real naming words and spotting special names (capital letters)
  - **Unit 2 (Singular & Plural Nouns)**: "Hurdle Meadow" — some words in the meadow are "one" and some have multiplied into "many"; a bunny companion hops each fence hurdle when Penny correctly sorts singular vs plural
- Recurring character: Fennick the fox is the constant narrator/guide across all chapters; each chapter introduces a companion animal matching that chapter's progress mechanic (see roadmap table in 6a)
- Story beats per chapter: intro scene (sets up the problem) → activities (the "journey") → chapter-end scene (problem resolved, valley area restored/brightens, reward stars/stickers awarded, Fennick celebrates)
- Light continuity: completed chapters visually "restore" on the home map (e.g., pond turns clearer blue, meadow gets flowers) so Penny can see her overall progress across the valley
- Keep story text minimal and read-aloud friendly (short sentences, large text, optional narration audio)
- Future units extend the same valley map with the remaining locations/companions in the roadmap (section 6a)

## 9a. Progression Mechanic — "Race to the goal"
Inspired by toddler learning apps (bold flat colors, thick rounded borders, chunky buttons, big friendly characters): each activity round = one obstacle/step on a visual path. Answering correctly moves the character forward one step, building visible momentum within a unit.

- **Per-unit theme**: Unit 1 (common & proper nouns) = frog hopping across lily pads on a pond; Unit 2 (singular & plural nouns) = bunny hopping over fence hurdles to reach a carrot patch. Each future unit gets its own themed track per the roadmap in 6a (reuses same mechanic/engine).
- **Progress track**: persistent strip across bottom or top of activity screen, showing one stepping stone/hurdle per question in the current level (not a fixed count — could be as few as 4 or as many as 12, depending on the level's data), with the character on the current one. For longer levels, the strip can scroll/compress (smaller dots) so it still fits on screen.
- Correct answer → short hop/jump animation, character lands on next stone, stone lights up/changes color
- Incorrect answer → character wobbles in place (no backward movement — stays low-stakes), retry same question
- Reaching the final stone triggers the unit-complete celebration (confetti, stars, character does a big victory jump)
- Visual style overall: bold flat saturated colors, thick (3-4px) rounded outlines on cards/buttons, large chunky text on banner-style buttons (yellow banner with dark outline, like reference apps), oversized friendly character with big eyes

## 10a. UX Design

### Screen Flow
1. **Home / Map screen** — mascot + two big "island" buttons: "Unit 1: Naming Words" and "Unit 2: Little Helper Words" (locked/unlocked styling not needed for v1 — both open)
2. **Unit intro card** — 1 short sentence + picture from mascot setting up the game (e.g., "Help me find the naming words!"), then "Start" button
3. **Activity screens** — one activity per screen, full-width, minimal chrome
4. **Round-end feedback** — immediate, overlays on same screen (no full navigation), auto-advances after ~1.5s or on tap
5. **Unit-end reward screen** — stars/stickers + "Back to Map" and "Play Again" buttons

### Layout Principles
- One task per screen — no scrolling, no competing elements
- Persistent but unobtrusive top bar: back-to-map button (top-left), progress dots (top-right, e.g., ●●●○○ for 5 rounds)
- Primary interactive area takes ~70% of screen, centered
- Buttons/tap targets minimum 80x80px — generous spacing to avoid mis-taps
- Mascot occupies a consistent corner (bottom-left) so Penny knows where to look for guidance/feedback

### Navigation & Controls
- No reading-heavy menus — icons + minimal text, with optional read-aloud (speech synthesis or pre-recorded audio) for instructions
- Single primary action per screen, clearly highlighted (color + size)
- "Back to map" always accessible but small/unobtrusive (won't be mis-tapped)
- No timers or countdowns — Penny works at her own pace

### Feedback & Tone
- Correct: bright color flash (green-ish), mascot cheer animation, short positive phrase ("Yes!", "Great job!") shown as large text + spoken
- Incorrect: neutral color (not red/harsh), mascot gentle nudge ("Almost! Try again"), answer not revealed immediately — let her retry once or twice before showing it
- No visible "wrong" counters or scores during play — keep it pressure-free; stars are the only summary, shown at the end

### Accessibility for Early Readers
- All instructions paired with icons/pictures, not text-only
- Large, high-contrast, dyslexia-friendly font (e.g., rounded sans-serif)
- Color is never the only signal (pair with shapes/icons for colorblind-friendliness)
- Optional audio narration toggle in a small settings icon (top-right corner)

### Parent Controls (lightweight)
- Small gear icon: toggle sound on/off, restart unit, jump to specific activity (for parent to skip/repeat as needed)

## 11. Extensibility (for future units)
- Code structured so each unit is a self-contained data + activity module (e.g., JS object/array defining activities), added to a central unit list
- Common reusable activity "engines": multiple-choice tap, drag-sort, click-to-highlight, type-the-word, build-a-phrase
- Remaining units 3-12 from the roadmap (section 6a) can reuse these engines with new content data and their own Word Valley location/companion
- Future stretch goals (not in v1): progress saving via localStorage, printable worksheet export, difficulty levels, voice narration

## 12. Out of Scope (v1)
- User accounts / multi-child profiles
- Cloud sync
- Detailed analytics/reporting for parent
- Formal "lesson" screens with explicit grammar explanations

## 13. Success Criteria
- Penny can complete Unit 1 and Unit 2 independently (or with minimal parent help) and wants to play again
- Julian can open the file on Mac with a double-click, no setup
- Adding a new unit later takes adding a data file + wiring it into the home menu, not rewriting the engine
