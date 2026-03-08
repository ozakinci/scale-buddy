# ScaleBuddy - Music Theory Reference Tool

<p align="center">
  <img src="https://img.shields.io/badge/Version-2.1.0-blue" alt="Version">
  <img src="https://img.shields.io/badge/License-MIT-green" alt="License">
  <img src="https://img.shields.io/badge/Status-Active-success" alt="Status">
</p>

<p align="center">
  <strong>A comprehensive, single-file web application for music theory reference</strong>
</p>

<p align="center">
  <a href="#features">Features</a> •
  <a href="#usage">Usage</a> •
  <a href="#scales">Scales</a> •
  <a href="#chords">Chords</a> •
  <a href="#contributing">Contributing</a> •
  <a href="#license">License</a>
</p>

---

## 🎵 What is ScaleBuddy?

**ScaleBuddy** is a lightweight, single-file web application that serves as a comprehensive music theory reference tool. It helps musicians, composers, and students quickly explore scales, triads, and chords for any root note.

### Key Features

- **40+ Scales** across 8 categories (Diatonic, Pentatonic, Symmetric, Jazz, World, Exotic, and more)
- **30+ Chords** including triads, seventh chords, extended chords, and classical chords
- **Roman Numeral Analysis** for scale degree triads
- **Proper Enharmonic Spelling** based on scale context (e.g. Bb instead of A# in flat-based scales)
- **Offline-Capable** - works without internet connection
- **Modern UI** with responsive design
- **Auto-Updating** - instant results as you select options

---

## 🚀 Quick Start

### Option 1: Local Usage (No Installation Required)

1. Download the `index.html` file
2. Open it directly in any modern web browser (Chrome, Firefox, Safari, Edge)
3. Select a root note and scale from the dropdown menus
4. View the results instantly!

### Option 2: Live Demo

Visit the live demo at:  
**https://ozakinci.github.io/ScaleBuddy/**

---

## 📖 Usage

### Basic Workflow

1. **Select Root Note** - Choose from 17 options covering all pitch classes including enharmonic equivalents (C, C#/Db, D, D#/Eb, E, F, F#/Gb, G, G#/Ab, A, A#/Bb, B)
2. **Select Scale Type** - Choose from 40+ scales organized by category
3. **View Results** - Three sections appear automatically:

#### Scale Notes Section
Shows all notes in the selected scale with Roman numerals in a table, followed by scale degree function names.

**Example (C Major):**
```
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│  C  │  D  │  E  │  F  │  G  │  A  │  B  │  ← Notes (amber)
├─────┼─────┼─────┼─────┼─────┼─────┼─────┤
│  I  │ ii  │ iii │  IV │  V  │ vi  │vii° │  ← Roman numerals (gray)
└─────┴─────┴─────┴─────┴─────┴─────┴─────┘

C Tonic
D Supertonic
E Mediant
F Subdominant
G Dominant
A Submediant
B Leading Tone
```

#### Scale Triads Section
Shows triads for each scale degree with Roman numeral analysis.

**Example (C Major):**
```
I C - E - G (C Major)
ii D - F - A (D Minor)
iii E - G - B (E Minor)
IV F - A - C (F Major)
V G - B - D (G Major)
vi A - C - E (A Minor)
vii° B - D - F (B Diminished)
```

#### Scale Chords Section
Lists all possible chord types built from the selected root note. The enharmonic spelling of each chord's notes is adjusted to match the selected scale context.

**Example (C Major chords, partial):**
```
Cadd2 C - D - E - G
Cadd4 C - E - F - G
Cmaj7 C - E - G - B
Cmin7 C - Eb - G - Bb
... (30+ chords total)
```

### Tips

- **Unselected Dropdowns** are highlighted with an amber tint as a reminder
- **Results auto-update** when both dropdowns are selected
- **No results** appear if only one dropdown is selected
- **Works offline** - no internet connection required
- **Mobile-friendly** - responsive design for all screen sizes

---

## 🎼 Scales Included

ScaleBuddy includes **40+ scales** organized into 8 categories:

### Diatonic Modes
- Major (Ionian)
- Dorian
- Phrygian
- Lydian
- Mixolydian
- Natural Minor (Aeolian)
- Locrian

### Minor Variants
- Harmonic Minor
- Melodic Minor (Ascending)
- Neapolitan Minor
- Neapolitan Major

### Pentatonic & Blues
- Major Pentatonic
- Minor Pentatonic
- Blues Scale

### Symmetric Scales
- Whole Tone
- Diminished (Half-Whole)
- Diminished (Whole-Half)
- Augmented
- Tritone

### Jazz & Contemporary
- Major Bebop
- Minor Bebop
- Dominant Bebop
- Prometheus
- Enigmatic

### Gypsy & Eastern European
- Hungarian Minor
- Hungarian Gypsy
- Double Harmonic (Gypsy)
- Phrygian Dominant

### World & Exotic
- Balinese
- Japanese (In Sen)
- Hirajoshi
- Iwato
- Yo
- Chinese
- Mongolian
- Persian
- Arabian
- Byzantine
- Oriental

### Chromatic
- Chromatic

---

## 🎸 Chords Included

ScaleBuddy includes **30+ chords** organized into 6 categories:

### Basic Triads
- Major
- Minor
- Diminished
- Augmented
- sus2
- sus4
- Power (5th)

### Sixth Chords
- Major 6th
- Minor 6th
- 6/9

### Seventh Chords
- Major 7th
- Dominant 7th
- Minor 7th
- Minor Major 7th
- Half-Diminished (m7b5)
- Fully Diminished 7th
- 7(b5)
- 7(#5)
- 7(b9)
- 7(#9)
- 7sus2
- 7sus4

### Extended Chords
- 9th
- Major 9th
- Minor 9th
- 11th
- Minor 11th
- 13th
- Minor 13th

### Added Tone Chords
- add2
- add4
- add9
- add11
- add13

### Altered Chords
- Altered (7alt)

### Special/Classical Chords
- Neapolitan (N6)
- Italian 6th
- French 6th
- German 6th
- Augmented Major 7

---

## 🛠️ Technical Details

### Technology Stack
- **HTML5** - Semantic structure
- **CSS3** - Modern styling with gradients, animations, and responsive design
- **Vanilla JavaScript** - No frameworks or build tools required

### Architecture
Single-file application (`index.html`) containing:
- HTML structure
- CSS styles (in `<style>` tag)
- JavaScript logic (in `<script>` tag)

### Data Structure
All music theory data is hard-coded for offline capability:

```javascript
// Scale definitions using W/H interval patterns
// W = whole step (2 semitones), H = half step (1 semitone), 3H = augmented 2nd (3 semitones), etc.
const SCALE_PATTERNS = {
  major: ['W', 'W', 'H', 'W', 'W', 'W', 'H'],
  minor: ['W', 'H', 'W', 'W', 'H', 'W', 'W'],
  harmonicMinor: ['W', 'H', 'W', 'W', 'H', '3H', 'H'],
  // ... 40+ scales
};

// Scale degree chord formulas
const SCALE_DEGREE_CHORDS = {
  major: ['Major', 'Minor', 'Minor', 'Major', 'Major', 'Minor', 'Diminished'],
  minor: ['Minor', 'Diminished', 'Major', 'Minor', 'Minor', 'Major', 'Major'],
  // ... formulas for all scales
};

// Roman numeral patterns
const ROMAN_NUMERALS = {
  major: ['I', 'ii', 'iii', 'IV', 'V', 'vi', 'vii°'],
  minor: ['i', 'ii°', 'III', 'iv', 'v', 'VI', 'VII'],
  // ... patterns for all scales
};

// Chord definitions (semitones from root)
const CHORDS = {
  'Major': [0, 4, 7],
  'Minor': [0, 3, 7],
  // ... 30+ chords
};
```

### Core Functions
- `getScaleNotes()` - Calculates scale notes using W/H patterns with proper enharmonic spelling
- `getScaleTriads()` - Generates triads for each scale degree using predefined formulas
- `getAllChordsForScale()` - Lists all chord types built from the root, with enharmonic spelling applied
- `applyEnharmonicSpelling()` - Applies flat/sharp preference derived from the parent scale to all chord notes, including those outside the scale
- `patternToSemitones()` - Converts W/H patterns to semitone intervals

---

## 🤝 Contributing

Contributions are welcome! Please follow these guidelines:

### How to Contribute

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/amazing-feature`)
3. **Commit your changes** (`git commit -m 'Add amazing feature'`)
4. **Push to the branch** (`git push origin feature/amazing-feature`)
5. **Open a Pull Request**

### Adding New Scales

1. Research the scale interval pattern (W/H pattern)
2. Add to `SCALE_PATTERNS` object in `index.html`
3. Add to `SCALE_DEGREE_CHORDS` object with chord qualities for each degree
4. Add to `ROMAN_NUMERALS` object with Roman numerals for each degree
5. Add to `CHORD_FUNCTIONS` object with function names for each degree
6. Add to `SCALE_NAMES` object for display name
7. Add to the appropriate `<optgroup>` in the HTML dropdown
8. Test the scale with various root notes, paying attention to enharmonic spelling

**Example:**
```javascript
// In SCALE_PATTERNS object
myNewScale: ['W', 'H', 'W', 'W', 'H', 'W', 'W'],

// In SCALE_DEGREE_CHORDS object
myNewScale: ['Minor', 'Diminished', 'Major', 'Minor', 'Minor', 'Major', 'Major'],

// In ROMAN_NUMERALS object
myNewScale: ['i', 'ii°', 'III', 'iv', 'v', 'VI', 'VII'],

// In CHORD_FUNCTIONS object
myNewScale: ['Tonic', 'Supertonic', 'Mediant', 'Subdominant', 'Dominant', 'Submediant', 'Subtonic'],

// In SCALE_NAMES object
myNewScale: 'My New Scale Name',

// In HTML dropdown
<option value="myNewScale">My New Scale Name</option>
```

### Adding New Chords

1. Research the chord interval pattern (semitones from root, in ascending order)
2. Add to `CHORDS` object in `index.html`
3. Test the chord with various root notes, including flat-based roots

**Example:**
```javascript
// In CHORDS object
'My New Chord': [0, 4, 7, 10, 14],
```

### Why W/H Interval Patterns

The system uses **W/H interval patterns** instead of semitone arrays because:

1. **Mathematically Verifiable** - W/H patterns can be verified directly against music theory sources
2. **Easier to Maintain** - Adding new scales only requires the pattern, not pre-calculated semitones
3. **Consistent Roman Numerals** - Roman numerals are derived from scale degree formulas, not calculated
4. **Proper Chord Qualities** - Chord qualities for each degree are predefined, eliminating calculation errors

**Example - Major Scale:**
- **Semitone array**: `major: [0, 2, 4, 5, 7, 9, 11]` (hard to verify at a glance)
- **W/H pattern**: `major: ['W', 'W', 'H', 'W', 'W', 'W', 'H']` (immediately verifiable)

### Code Style

- Use camelCase for JavaScript variables and functions
- Use kebab-case for HTML IDs and classes
- Keep functions focused and well-commented
- Follow the existing code organization pattern

### Testing

1. Open `index.html` in a browser
2. Test all scale categories with both sharp and flat root notes
3. Test edge cases (chromatic scale, diminished scales, whole tone with Eb root)
4. Verify enharmonic spelling is correct (e.g. Bb not A# in flat-based scales)
5. Check responsive design on mobile

---

## 📚 Music Theory Sources

Scale and chord interval patterns are based on authoritative music theory references:

### Scales
- [Wikipedia: List of musical scales and modes](https://en.wikipedia.org/wiki/List_of_musical_scales_and_modes) - Primary source for W/H patterns
- "The Jazz Theory Book" by Mark Levine
- "The Complete Musician" by Steven Laitz

### Chords
- [Wikipedia: List of chord names](https://en.wikipedia.org/wiki/List_of_chord_names)
- "The Chord Scale Theory & Jazz Harmony" by Bert Ligon
- "Harmony and Voice Leading" by Aldwell & Schachter

---

## 🔧 Troubleshooting

### Issue: Dropdowns not updating
**Solution:** Make sure both root note and scale type are selected. If only one is selected, no results will appear.

### Issue: Scale sounds wrong
**Solution:** The scale patterns have been verified against authoritative music theory sources. If you believe there's an error, please check the pattern against Wikipedia's scale list and open an issue.

### Issue: Scale not found
**Solution:** Check the spelling of the scale name in the dropdown. All scales are listed in the HTML `<optgroup>` tags.

### Issue: Browser compatibility
**Solution:** The app works in all modern browsers (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+). For older browsers, some CSS features may not work.

---

## 📝 Version History

### v2.1.0 (March 2026)
- **Bug Fix**: Fixed `harmonicMinor` scale pattern - was identical to natural minor (augmented 2nd between degrees 6-7 was missing)
- **Bug Fix**: Fixed `hirajoshi` scale pattern - interval sum was 11 semitones instead of 12
- **Bug Fix**: Rewrote `applyEnharmonicSpelling()` to correctly handle notes outside the parent scale. Previously, chord notes whose pitch class did not appear in the scale (e.g. A# in Eb Whole Tone) kept their sharp spelling regardless of scale context. Now flat/sharp preference is inferred from the parent scale and applied consistently
- **Bug Fix**: Fixed `Neapolitan (N6)` chord definition - was `[0,3,7]` (minor) instead of `[0,4,7]` (major)
- **Bug Fix**: Fixed `German 6th` chord interval order - intervals are now sorted ascending for correct note display
- **Cleanup**: Removed duplicate `7sus4` entry (was defined twice; second silently overwrote first)
- **Cleanup**: Removed redundant `Suspended 2nd` / `Suspended 4th` entries (exact duplicates of `sus2` / `sus4`)
- **UI**: Updated color scheme to dark navy/slate with warm amber accents and orange-tinted background

### v2.0.1 (January 18, 2026)
- **Critical Bug Fix**: Fixed `patternToSemitones()` function missing root note (0 semitones)
- **Issue Resolved**: Scale notes were displaying incorrect enharmonic spellings (E# instead of E, B# instead of B)
- **Root Cause**: Function was not including the initial 0 semitone for the root note
- **Solution**: Initialize semitones array with [0] and remove octave with slice(0, -1)
- **Verification**: All 40+ scales now display correct note names and enharmonic spellings

### v2.0 (January 2026)
- **Improved Scale Generation**: Replaced semitone arrays with W/H interval patterns
- **Enhanced Accuracy**: All scale patterns verified against authoritative sources
- **Simplified Maintenance**: Data-driven approach for easier updates
- **Better Roman Numerals**: Predefined patterns eliminate calculation errors
- **Updated Documentation**: Added detailed contributing guidelines for new scales

### v1.0 (Initial Release)
- Basic scale and chord reference tool
- 40+ scales and 30+ chords
- Roman numeral analysis
- Enharmonic spelling
- Modern UI with responsive design

---

## 🎯 Roadmap

Future features may include:

- [ ] Audio playback of scales and chords
- [ ] Chord progression generator
- [ ] Staff notation display
- [ ] Keyboard diagram visualization
- [ ] Mobile app version
- [ ] Advanced search/filtering
- [ ] User presets/saved combinations
- [ ] Export functionality (PDF, MIDI)

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2026 Tayfun Ozakinci

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## 🙏 Acknowledgments

- Built with ❤️ for musicians and music students everywhere
- Inspired by the need for a quick, offline music theory reference
- Thanks to the music theory community for authoritative sources

---

## 📞 Support & Contact

If you encounter any issues or have questions:

1. Check the [Troubleshooting](#troubleshooting) section
2. Review the [Contributing](#contributing) guidelines
3. Open an issue on GitHub

**Contact:**
- **Author**: Tayfun Ozakinci
- **GitHub**: https://github.com/ozakinci
- **Project**: https://github.com/ozakinci/ScaleBuddy
- **Issues**: https://github.com/ozakinci/ScaleBuddy/issues

---

**Made with 🎵 for musicians by musicians**

*ScaleBuddy - Your comprehensive music theory companion*