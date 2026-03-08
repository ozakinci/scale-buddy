# ScaleBuddy - AI Coding Instructions

## Project Overview
**ScaleBuddy** is a lightweight, single-file web application serving as a comprehensive music theory reference tool. Users select a root note and scale from dropdown menus to instantly view:
- **Scale Notes** - All notes in the selected scale, shown in a table with Roman numerals and degree function names
- **Scale Triads** - Triads for each scale degree with Roman numeral analysis
- **Scale Chords** - All chord types built from the selected root note, with enharmonic spelling adjusted to match the scale context

**Tech Stack:** Vanilla HTML, CSS, JavaScript (no frameworks, no build tools)  
**Architecture:** Single `index.html` file containing all structure, styles, and logic  
**Deployment:** GitHub Pages via GitHub Actions

---

## Core Requirements

### 1. Input Interface
Two dropdown menus that auto-update the display when both are selected:

**Root Note Dropdown:**
- All 17 options covering all pitch classes including enharmonic equivalents
- Natural notes: C, D, E, F, G, A, B
- Sharps: C#, D#, F#, G#, A#
- Flats: Db, Eb, Gb, Ab, Bb
- C# and Db are separate options (they sound the same but trigger different enharmonic spelling)

**Scale Dropdown:**
- Scales organized into logical groups using `<optgroup>` tags
- Groups: Diatonic Modes, Minor Variants, Pentatonic & Blues, Symmetric Scales, Jazz & Contemporary, Gypsy & Eastern European, World & Exotic, Chromatic
- All scales sourced from authoritative music theory references

### 2. Display Sections
Three sections appear below the dropdowns when both are selected:

**Scale Notes Section:**
- Displays a two-row table: note names (top row) and Roman numerals (bottom row)
- Below the table: scale degree function names (e.g., "C Tonic", "D Supertonic")
- Uses proper enharmonic spelling based on scale context (e.g., Bb not A# in flat-based scales)
- Formatting: amber for note names, gray monospace for Roman numerals and function names

**Scale Triads Section:**
- Shows triads for each scale degree with Roman numeral analysis
- Format: `Roman numeral  note - note - note (Root Quality)` e.g. `I  C - E - G (C Major)`
- Uses proper notation: uppercase for major, lowercase for minor, ° for diminished, + for augmented
- Compact format with blank lines between entries
- Formatting: amber for Roman numerals, gray monospace for notes and chord names

**Scale Chords Section:**
- Lists all chord types built from the selected root note, sorted alphabetically
- Enharmonic spelling of each chord's notes is adjusted to match the selected scale context
- Each chord shows: chord name and its notes
- Compact format with blank lines between entries
- Formatting: amber for chord names, gray monospace for notes

### 3. UI/UX Requirements
- **Dark theme** - deep navy/slate container on a warm burnt orange background
- **Amber accent color** for all headings, labels, and highlighted elements
- **Easy navigation** - intuitive layout with grouped dropdowns
- **Auto-updating** - display updates immediately when both dropdowns are selected
- **Subtle highlighting** - unselected dropdowns get an amber tint border as a reminder
- **No display** - results are hidden if only one dropdown is selected
- **Offline-capable** - works without internet connection
- **Responsive** - works on mobile via CSS grid collapse to single column

---

## Music Theory Data

### Notes
The `NOTES` array contains only the 12 chromatic pitches using sharp spellings:
```javascript
const NOTES = ['C', 'C#', 'D', 'D#', 'E', 'F', 'F#', 'G', 'G#', 'A', 'A#', 'B'];
```

Flat spellings are resolved via a separate lookup:
```javascript
const ENHARMONIC_EQUIVALENTS = {
  'Db': 'C#', 'Eb': 'D#', 'Gb': 'F#', 'Ab': 'G#', 'Bb': 'A#'
};
```

The `getNoteIndex(note)` function handles both sharp and flat spellings by checking `ENHARMONIC_EQUIVALENTS` as a fallback.

### Scale Patterns
Scales are defined as **W/H interval patterns**, not semitone arrays. This makes them easier to verify and maintain.

```
W  = whole step   = 2 semitones
H  = half step    = 1 semitone
3H = augmented 2nd = 3 semitones
4H = major 3rd    = 4 semitones
5H = perfect 4th  = 5 semitones
```

```javascript
const SCALE_PATTERNS = {
  major:        ['W', 'W', 'H', 'W', 'W', 'W', 'H'],
  minor:        ['W', 'H', 'W', 'W', 'H', 'W', 'W'],
  harmonicMinor:['W', 'H', 'W', 'W', 'H', '3H', 'H'],  // augmented 2nd between degrees 6-7
  // ... all scales
};
```

**Do not use semitone arrays for scale definitions.** Always use W/H patterns.

### Scales Included

**Diatonic Modes:**
Major (Ionian), Dorian, Phrygian, Lydian, Mixolydian, Natural Minor (Aeolian), Locrian

**Minor Variants:**
Harmonic Minor, Melodic Minor (Ascending), Neapolitan Minor, Neapolitan Major

**Pentatonic & Blues:**
Major Pentatonic, Minor Pentatonic, Blues Scale

**Symmetric Scales:**
Whole Tone, Diminished (Half-Whole), Diminished (Whole-Half), Augmented, Tritone

**Jazz & Contemporary:**
Major Bebop, Minor Bebop, Dominant Bebop, Prometheus, Enigmatic

**Gypsy & Eastern European:**
Hungarian Minor, Hungarian Gypsy, Double Harmonic (Gypsy), Phrygian Dominant

**World & Exotic:**
Balinese, Japanese (In Sen), Hirajoshi, Iwato, Yo, Chinese, Mongolian, Persian, Arabian, Byzantine, Oriental

**Chromatic:**
Chromatic

### Chords
Chords are defined as semitone intervals from root, in ascending order:

```javascript
const CHORDS = {
  'Major':        [0, 4, 7],
  'Minor':        [0, 3, 7],
  'sus2':         [0, 2, 7],
  'sus4':         [0, 5, 7],
  'Major 7th':    [0, 4, 7, 11],
  // ... all chords
};
```

**Important:** Intervals must be in strictly ascending order. Out-of-order intervals produce incorrect note display.

### Chords Included

**Basic Triads:** Major, Minor, Diminished, Augmented, sus2, sus4, Power (5th)

**Sixth Chords:** Major 6th, Minor 6th, 6/9

**Seventh Chords:** Major 7th, Dominant 7th, Minor 7th, Minor Major 7th, Half-Diminished (m7b5), Fully Diminished 7th, 7(b5), 7(#5), 7(b9), 7(#9), 7sus2, 7sus4

**Extended Chords:** 9th, Major 9th, Minor 9th, 11th, Minor 11th, 13th, Minor 13th

**Added Tone Chords:** add2, add4, add9, add11, add13

**Altered Chords:** Altered (7alt)

**Special/Classical Chords:** Neapolitan (N6), Italian 6th, French 6th, German 6th, Augmented Major 7

---

## Implementation Architecture

### Data Structure (current)
```javascript
// 1. Raw note lookup
const NOTES = ['C', 'C#', 'D', 'D#', 'E', 'F', 'F#', 'G', 'G#', 'A', 'A#', 'B'];
const SCALE_DEGREES = ['C', 'D', 'E', 'F', 'G', 'A', 'B'];
const ENHARMONIC_EQUIVALENTS = { 'Db':'C#', 'Eb':'D#', 'Gb':'F#', 'Ab':'G#', 'Bb':'A#' };

// 2. Scale patterns (W/H strings, NOT semitone arrays)
const SCALE_PATTERNS = { major: ['W','W','H','W','W','W','H'], ... };

// 3. Per-scale metadata
const SCALE_NAMES = { major: 'Major (Ionian)', ... };
const SCALE_DEGREE_CHORDS = { major: ['Major','Minor','Minor','Major','Major','Minor','Diminished'], ... };
const ROMAN_NUMERALS = { major: ['I','ii','iii','IV','V','vi','vii°'], ... };
const CHORD_FUNCTIONS = { major: ['Tonic','Supertonic','Mediant','Subdominant','Dominant','Submediant','Leading Tone'], ... };

// 4. Chord definitions (semitones from root, ascending)
const CHORDS = { 'Major': [0,4,7], ... };
```

### Core Functions
```javascript
// Resolve a note name (including flats) to a semitone index 0-11
function getNoteIndex(note) { ... }

// Convert W/H pattern array to semitone offsets from root
function patternToSemitones(pattern) { ... }

// Build scale note array with correct enharmonic spelling
function getScaleNotes(rootNote, scaleType) { ... }

// Build all diatonic triads using SCALE_DEGREE_CHORDS and ROMAN_NUMERALS
function getScaleTriads(rootNote, scaleType) { ... }

// Build all chord types from root, apply enharmonic spelling from scale context
function getAllChordsForScale(rootNote, scaleType) { ... }

// Apply flat/sharp preference (derived from parent scale) to a list of notes.
// Notes whose semitone appears in the scale use the scale's spelling.
// Notes outside the scale use the scale's flat/sharp preference.
function applyEnharmonicSpelling(notes, parentScale) { ... }

// Re-render all three output sections and show results
function updateDisplay() { ... }
```

### Enharmonic Spelling (critical)
`applyEnharmonicSpelling()` works in two passes:
1. Build a `semitone → spelling` map from the parent scale notes
2. Count flats vs sharps in the parent scale to determine preference
3. For each chord note: use the scale's spelling if the semitone is in the scale; otherwise apply the flat/sharp preference

This ensures that e.g. Eb Whole Tone produces Bb (not A#) for chord tones that fall outside the scale.

---

## Developer Workflow

### Standard Sequence (always follow this order)

**1. Pull before making changes**
```bash
git pull origin main
git status
```

If `git status` shows uncommitted changes, decide first:
```bash
# Option A: commit first
git add . && git commit -m "wip: description" && git pull origin main

# Option B: stash, pull, reapply
git stash && git pull origin main && git stash pop

# Option C: discard (only if changes are not needed)
git reset --hard HEAD && git pull origin main
```

**2. Make changes**
Keep browser console open (F12) while editing to catch JavaScript errors immediately.

**3. Test before committing** (see Testing Checklist below)

**4. Commit and push**
```bash
git add .
git commit -m "<type>: <short description>

- Detail 1
- Detail 2"

git push origin main
```

**5. Verify deployment**
Wait 1-2 minutes for GitHub Actions, then visit https://ozakinci.github.io/ScaleBuddy/

**If something goes wrong:**
```bash
git log --oneline -5    # see recent commits
git revert HEAD         # safely undo last commit
git diff HEAD~1 HEAD    # see what changed
```

### Commit Message Format
```
feat: Add keyboard diagram visualization
fix: Correct enharmonic spelling for flat-root scales
docs: Update README with v2.1.0 changes
chore: Remove duplicate chord definitions
refactor: Simplify applyEnharmonicSpelling logic
```

---

## Testing Checklist (Before Every Commit)

### Functionality
- [ ] No JavaScript errors in browser console
- [ ] Both dropdowns trigger display update on change
- [ ] Results section hidden when only one dropdown is selected
- [ ] All three result sections render without errors

### Scale Notes
- [ ] Note names use correct enharmonic spelling for the root (Bb not A# for Eb scales)
- [ ] Roman numeral count matches scale note count
- [ ] Degree function names present for all scale degrees

### Scale Triads
- [ ] Roman numerals use correct case (uppercase major, lowercase minor, ° diminished, + augmented)
- [ ] Triad notes match the scale (root, 3rd, 5th in scale context)

### Scale Chords
- [ ] All chord types are listed
- [ ] Chord notes use correct enharmonic spelling (consistent with scale context)
- [ ] No chord appears twice

### Specific Checks
- [ ] C Major: C D E F G A B
- [ ] Eb Whole Tone: Eb F G Bb... (Bb not A#)
- [ ] A Harmonic Minor: A B C D E F G# (raised 7th present)
- [ ] B Diminished triad: B D F (not B C# E#)
- [ ] Test at least one scale from each category
- [ ] Test root notes: C, C#, Db, Eb, F#, Ab, Bb (both sharp and flat roots)
- [ ] Test edge cases: Chromatic (12 notes), Pentatonic (5 notes), Diminished (8 notes)

**If ANY check fails, do not commit. Fix first.**

---

## Adding New Scales

When adding a new scale, all 6 data objects must be updated consistently:

```javascript
// 1. SCALE_PATTERNS - W/H interval pattern (must sum to 12 semitones)
myScale: ['W', 'H', 'W', 'W', 'H', 'W', 'W'],

// 2. SCALE_NAMES - display label
myScale: 'My Scale Name',

// 3. SCALE_DEGREE_CHORDS - chord quality per degree
myScale: ['Minor', 'Diminished', 'Major', 'Minor', 'Minor', 'Major', 'Major'],

// 4. ROMAN_NUMERALS - Roman numeral per degree
myScale: ['i', 'ii°', 'III', 'iv', 'v', 'VI', 'VII'],

// 5. CHORD_FUNCTIONS - degree function name per degree
myScale: ['Tonic', 'Supertonic', 'Mediant', 'Subdominant', 'Dominant', 'Submediant', 'Subtonic'],

// 6. HTML dropdown - add to appropriate <optgroup>
<option value="myScale">My Scale Name</option>
```

**Always verify the W/H pattern sums to exactly 12 semitones before committing.**

## Adding New Chords

```javascript
// In CHORDS object - intervals must be in ascending order
'My Chord': [0, 3, 7, 10, 14],
```

Test with both sharp-root and flat-root notes to verify enharmonic spelling is correct.

---

## Conventions

### Naming
- JavaScript: camelCase (`getScaleNotes`, `patternToSemitones`)
- HTML IDs/classes: kebab-case (`root-note`, `scale-result`)
- Scale names: Title Case with mode in parentheses where relevant (e.g., `Major (Ionian)`)
- Chord names: Standard notation (`Major`, `Minor 7th`, `Half-Diminished (m7b5)`)

### Data Format
- **Scale intervals:** W/H pattern strings, never raw semitone arrays
- **Chord intervals:** Semitone integers from root, always in ascending order
- **Note names:** Uppercase letter with optional # or b (`C#`, `Db`, `Bb`)

### Robustness
- Handle missing scale/chord data gracefully (don't crash, show nothing)
- Don't expose raw JavaScript errors to the user
- Validate both dropdowns before rendering

### Accessibility
- Semantic HTML elements
- Keyboard-navigable dropdowns
- Sufficient color contrast (amber on dark slate passes WCAG AA)

---

## Research Sources

### Scales
- [Wikipedia: List of musical scales and modes](https://en.wikipedia.org/wiki/List_of_musical_scales_and_modes)
- "The Jazz Theory Book" - Mark Levine
- "The Complete Musician" - Steven Laitz

### Chords
- [Wikipedia: List of chord names](https://en.wikipedia.org/wiki/List_of_chord_names)
- "The Chord Scale Theory & Jazz Harmony" - Bert Ligon
- "Harmony and Voice Leading" - Aldwell & Schachter

Cross-reference at least 2 sources before adding any new scale or chord. Verify W/H patterns sum to 12.

---

## Future Roadmap
- [ ] Audio playback of scales and chords
- [ ] Chord progression generator
- [ ] Staff notation display
- [ ] Keyboard diagram visualization
- [ ] Mobile app version
- [ ] Advanced search/filtering
- [ ] User presets/saved combinations
- [ ] Export functionality (PDF, MIDI)