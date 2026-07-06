# Word Valley — Lily Pad Pond

A single-file, browser-based English practice game (`index.html`) for young learners. Fennick the fox and a frog guide the player ("Penny") across lily pads, unlocking a new pond level for each grammar/spelling topic. No build step — open `index.html` in any browser to play.

Progress is saved per-level in `localStorage` (`wv_unit1_completed`); completing every level unlocks the "Lily Pad Pond is restored!" chapter-end screen.

## How it works

- **Map screen** — one card per level. Levels with sub-exercises expand into a list of tappable exercise rows; each row jumps straight to that exercise.
- **Level screen** — shows the current prompt, a progress track (dots) for question-by-question exercises, the exercise itself, and live feedback text.
- **Result screen** — appears after each exercise, showing a score breakdown and a running total, with a button to continue.
- **Chapter end** — plays once all 6 levels are marked complete.
- A 🎵 button in the top bar toggles background music; correct answers trigger a chime + spoken praise (Web Speech API), wrong answers get a gentle "wobble" + buzz.

## Levels

### Level 1 — Nouns
*Sort and find the nouns!*
1. **Sort It!** — Drag-and-drop: sort noun cards (with pictures) into People / Animals / Things / Places. *(static — every noun needs a matching picture)*
2. **Find the Noun** — Tap the noun in each sentence. *(static — every sentence needs a matching picture)*
3. **Word Search** — Drag across a letter grid to find hidden fruit words. *(static — hand-placed letter grid + pictures)*
4. **Fill the Blank** — Type the missing noun to complete each sentence. **Randomised** — 6 sentences are drawn fresh from a 14-sentence bank each time you (re)enter the level.

### Level 2 — Common Noun vs Proper Noun
*Tap each word: is it a common noun or a proper noun?*
1. **Common or Proper?** — Multiple choice per word. **Partially randomised** — "park" and "Mr Wong" stay fixed (they have matching pictures); the other 8 words (5 common + 3 proper) are drawn fresh from an emoji word bank each time.
2. **Colour the Nouns** — Pick a highlighter colour and click all the proper nouns in a word cloud. **Fully randomised** — 13 words (9 common + 4 proper) drawn fresh from a text-only bank.
3. **Paint the Candies** — Pick a colour key (common vs proper) and paint each candy in a jar correctly. **Fully randomised** — 12 words (7 common + 5 proper) drawn fresh from a text-only bank.

### Level 3 — Singular & Plural Nouns
*Learn when to add -s or -es!*
0. **Lesson** — Teaching screen covering the -s and -es rules with examples. *(static — it's instructional content, not a quiz)*
1. **Add -s** — Type the plural form for words that just take -s. **Partially randomised** — apple/classroom/teacher stay fixed (matching pictures); 3 more words are drawn fresh from an emoji bank.
2. **Add -es** — Type the plural form for words ending in s/sh/ch/x. **Fully randomised** — all 10 words drawn fresh from a 15-word emoji bank.
3. **Pick the Plural** — Multiple choice: choose the correctly spelled plural. **Partially randomised** — same 3 picture words stay fixed; 7 more are drawn fresh from an emoji bank.
4. **How Many?** — Given a count and a picture, choose singular or plural. **Partially randomised** — same 3 picture words stay fixed (with a random count 1–6 each time); 9 more emoji words (also random counts) are drawn fresh from a bank.

Randomisation happens once per level visit (in `startLevel()`), so the words stay put for the whole playthrough but change the next time you open that level from the map. See `buildLevel0Data` / `buildLevel1Data` / `buildLevel2Data` and the `*_POOL` / `*_BANK` constants above them in `index.html` for the word pools.

### Level 4 — Days of the Week
*Learn the days of the week in order!*
1. **Put Them in Order** — Drag-and-drop: place 7 shuffled day chips into 1st–7th slots in the correct weekly order.
2. **Missing Letters** — Fill in the missing letters in the middle of each day's name (e.g. `M__day` → "on", `Th__sday` → "ur").

### Level 5 — Weekly Spelling (tricky words: *come, find, my, there, took*)
*Practise this week's tricky words!*
1. **Unscramble It!** — Tap scrambled letter tiles in the right order to spell each word (e.g. `MECO` → "come"). Includes a 🔊 button that speaks the target word aloud (auto-plays on each new word, tap to repeat).
2. **Sound It Out** — Tap 🔊 to hear the word spoken aloud (auto-plays), then pick the correctly spelled word from 3 options (e.g. hearing "my" → choose between `my` / `mi` / `mye`). Falls back to a written fake-phonetic clue (e.g. "MI") if the browser has no speech synthesis support.
3. **Fill the Blank** — Type the correct word to complete each sentence (word bank provided).

### Level 6 — Telling Time
*Read the hands on an analog clock!*
1. **On the Hour** — Read times where the minute hand points to 12.
2. **Quarter Hours** — Read times at :15, :30, :45.
3. **Every 10 Minutes** — Read times at 10-minute intervals.
4. **Every 5 Minutes** — Read times at 5-minute intervals.
5. **Exact Time** — Read the clock to the nearest minute.

## Code layout (`index.html`)

Everything lives in one file:
- `<style>` — all visual styling (pond theme, cards, choice buttons, per-exercise-type CSS).
- Data blocks (`level0Data` … `level5Data`, `levelClockData`) — one array per level, each entry an exercise-type object (`type: 'drag' | 'classify' | 'jumble' | 'phonetic' | ...`).
- `LEVELS` — assembles the levels in play order, each with a `title`, `sub`, `prompt`, and its `exercises` list (label + sub + `startIdx` into that level's data array).
- Render functions (`renderDrag`, `renderClassify`, `renderJumble`, `renderPhonetic`, `renderDayOrder`, `renderDayBlank`, `renderClockRead`, etc.) — one per exercise type, each responsible for building the DOM and wiring up answer checking.
- `handleResult` / `advance` / `levelComplete` / `finishExercise` — shared flow control: score tracking, moving to the next question/exercise/level.
- Audio section — Web Audio API background melody + chime/buzz feedback, plus `speakWord`/`speakWordSupported` (Web Speech API) used for the Level 5 pronunciation buttons.

To add a new exercise type: add a data block, register it in `LEVELS`, add a `render<Type>` function, and add a dispatch line in `renderQuestion()`.
