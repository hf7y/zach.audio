# Total Abstraction, Act 2, as performed 2023-10-21

`act2-2023.ly` is a machine-derived draft of what was performed on the night, built for Zach to check.
It comes only from the machine passes over the church board recording in
`portfolio/siddhartha-2023/check-2023/`. **Nobody has listened** to the recording for it.
It is written in the abc house style (`lib/core` + `lib/project`). `act2-2023.pdf` has 14 pages.

Agent-written, 2026-11-26. The sung and spoken words in the score are the Notion page
`compositions/siddhartha-2023/scores/Draft_Act_2.pdf`, exactly as `mutool draw -F txt` prints it. They are printed in
upright roman. Every other printed word is agent text, printed in *[square brackets, italic]*; the `.ly` header says so in a comment.

## The brief (Zach, chat, 2026-11-25, verbatim)

> the 2020 score is not accurate. the 2023 needs to be checked against the actual recording. but yes the house style would be preferred at the end.

Asked to build the score from the check: "build it"

On the held tones: "free, separate subagent attempt to transcribe and notate just pitches."

On the tape: "in the score as fixed media, but also transcribed"

## Files

| file | what |
|---|---|
| `build.py` | writes `act2-2023.ly` from the check's tables. Edit this file, not the `.ly` |
| `act2-2023.ly` | the score (generated) |
| `act2-2023.pdf` | compiled, LilyPond 2.24.4, 14 pages |

## Compile

```
python3 build.py
lilypond -I /mnt/d/gardien-media/mandark/Documents/abc act2-2023.ly
```

`-I` points at the abc tree, so `\include "lib/includes.ily"` loads `lib/core` and `lib/project` read-only.
The compile prints three "page compressed" warnings (pages 3, 5 and 14). The PDF is fine despite them.

## Sources

| what | from |
|---|---|
| section times, levels, what each stretch is | `check-2023/sections.md`, `levels.tsv` |
| held tones, sections 10, 12, 13 (S, A, T, B staves) | `check-2023/pitches/tones.tsv`: all 166 sung tones, read by `parse_pitch_table` |
| tape, section 11 (two Tape staves) | `check-2023/pitches/tape.tsv`: all 96 tones of `Vowels.wav`, on the board clock (`board_in`, `board_out`) |
| the two octave calls, the low sweep | `check-2023/pitches/README.md` |
| word onsets (homophony, single words) | `transcript-words.tsv` (board witness) |
| lines heard in order 2066-2143 | `transcript.tsv` |
| clap/plosive candidates | `sections.md` "Claps" (the 11 strongest isolated broadband transients) |
| sung/spoken text | `Draft_Act_2.pdf` via `mutool draw -F txt` |
| notation devices | `/mnt/d/gardien-media/mandark/Documents/abc/lib/` (`core/notation.ily`, `core/frame-engraver.ily`, `project/timing.ily`, `project/style.ily`) |

**The held tones and the tape come from the pitch pass (PR #364), not from the check's first reading.** The first build used
`sections.md`'s tone list and `vowels_vs_board.tsv`, because `pitches/` had not landed. Those readings stay in `sections.md`, `held-tones.tsv`
and `vowels_vs_board.tsv`. Every other section is unchanged.

## Sections

Times are master seconds on `Church_10_21_2023.wav` (board clock), as in `sections.md`; the score prints them as M:SS.mmm via `\cueTime`,
and page 1 lists them (`\cueTimeline`). Numbers follow the 17-section outline in `discrepancies.md`; 6 and 8 are split.

| # | board s | length | Notion heading (where the check's reading puts it) | notated as |
|---|---|---|---|---|
| 0 | 1786-1807.9 | 21.9 s | | timed rest (`\cueGapTo`) |
| 1 | 1807.9-1809 | 1.1 s | | cue event: the low thud |
| 2 | 1809-1836 | 27 s | | timed rest (`\cueGapTo`); the clicks at 1814.9 and 1827.5 on the Cues line |
| 3 | 1836-1906 | 70 s | Phrase 1 | prose with timings: S A T B enter in frames at the level steps 1837, 1842, 1855, 1863 |
| 4 | 1906-2041 | 135 s | (Phrases 2-3?) | frames continue: "all eight lines, overlapping" |
| 5 | 2041-2066 | 25 s | | frames continue; transients double |
| 6a | 2066-2143 | 77 s | Phrase 4 | prose with timings: the Phrase 1 lines in the order heard, at their times |
| 6b | 2143-2180 | 37 s | "All in unison" | text with rhythm: lines 3-8 in sequence, one × note per word at its whisper onset, 0.25 s grid |
| 7 | 2180-2186 | 6 s | | timed rest (`\cueGapTo`) |
| 8a | 2186-2215 | 29 s | A: Consonants | text with rhythm: single words at their onsets, 0.5 s grid; arrow "[words] → [consonants]" |
| 8b | 2215-2240 | 25 s | | framed cell: the lines losing their vowels |
| 8c | 2240-2290 | 50 s | | framed cell: the Notion page's blanked text, printed in full above the score |
| 9 | 2290-2370 | 80 s | B: Vowels | framed cell: the Notion page's vowel text, printed in full above the score |
| 10 | 2370-2416 | 46 s | | pitched: every tone of `tones.tsv`, S A T B by register, chords on the 0.25 s grid, cents of 25 or more under |
| 11 | 2382.68-2644.8 | 262.1 s | | two small Tape staves (C4 and up; below C4): every tone of `tape.tsv` as chords, fixed media |
| 12 | 2416-2638 | 222 s | | pitched: as 10 |
| 13 | 2638-2647 | 9 s | | pitched: C♯4 with C4 and the low tones at the end, al niente |
| 14 | 2647-2786 | 139 s | C: Denouement | framed cell with "Fricatives s, v, h, f" and "Decrescendo al niente" (Notion text), an al niente hairpin over 139 s |
| 15 | 2786-2949 | 163 s | | timed rest (`\cueGapTo`), 20 bars + 3 s |
| 16 | 2949-2962 | 13 s | | cue events: the low sound (2949), house lights (2953) |
| 17 | 2962-2990 | 28 s | | timed rest (`\cueGapTo`), then `\cueTotalTime` = 49:50 |

## How it was built, and the house-style devices

- **Clock.** Each group of sections is one `\score` with its own `\cueStartTime` taken from the recording, like a reel whose start
  comes from the picture edit. One bar = 8 s at ♩ = 30 (4 s at ♩ = 60 in the homophony and consonant scores). The bar ticks are a time grid.
  Each section starts on a bar; a section's short last bar comes from `\set Timing.measureLength`.
  Every section start and most notes carry `\cueTime`, so any note can be checked against the recording.
- **Timed rests** are `\cueGapTo` (timing.ily), with each voice's earlier music in the score as the preceding argument.
- **Prose with timings** uses `\ss` (no staff lines) and the frame engraver: a boxed two-note cell, then an extender line for as long
  as the recitation lasts. `\daln` and `\aln` mark the entries and the final decrescendo, and `\arrowSpan` marks words → consonants.
- **Spacing** is the house proportional spacing (1/8). The mostly empty scores (opening, recitation, vowels, denouement) and sections 6a and 8b
  use 1/4, half the width. The held tones (10-13) use 1/16, twice the width, because their chords change every 2 s on average.
  `style.ily` allows a reel-level exception, and a comment in `build.py` says so.
- **Library gaps, filled with LilyPond built-ins** (commented in the `.ly`): cross noteheads for speech, unpitched sound and claps
  (`NoteHead.style = #'cross`, `\xNote`); a triangle head for the thud and the lights; one-line staves; `\RemoveEmptyStaves` for the
  Cues and Tape staves; chords for divisi.
- **Held tones** (`tones.tsv`, 166 tones). Each tone is written at its `note`, the nearest equal-tempered note (A4 = 440). It runs from `t_in`
  to `t_out`, rounded to 0.25 s. Tones go to S, A, T or B **by register only**: G4 and up to S (82 notes), C4-F♯4 to A (33), G3-B3 to T (12),
  below G3 to B (28).
  - Where tones overlap on a staff they are a chord. A new chord starts at every entry or exit, and the notes that carry on are tied.
    The staves are stemless and dotless, so a tone's length is how far its tie runs on the time grid. Rests mark silences of 2 s or more.
  - Two overlapping tones on the same note are one notehead with both cents joined by "&". There are 11 such pairs, so 166 tones make 155 noteheads.
    The widest pair is A5 +45 & −21 at 2596.6, 66 cents apart: perhaps two groups on one written note.
  - Tones 8 dB or more under the loudest sound (`rel_db` ≤ −8, 95 notes) have small heads. A `\cueTime` stands over each tone of the
    loudest line (`rel_db` ≥ −3).
  - Cents (`cents`) are printed under a tone when they are 25 or more, with the note's name when it is in a chord.
  - **The rub at 2379-2404.** Every B and B♭ entering in that span has its cents printed, even under 25. Over the S chord at 2380.25 a note reads
    "the rub: B♭4 +46 against B4 −23, 31 cents apart". `pitches/README.md` calls it a quarter tone. By its own cents it is 31 cents.
  - **Unison spread.** A measured spread (`spread_c` as a plain number) of 38 cents or more is printed over the tone: C3 40 (2421), E5 38 (2478),
    C♯5 44 and B4 38 (2523), B♭5 53 (2592) and A4 45 (2604). The coarser "N lines" spreads of 38 or more (35 tones) are only `%` comments
    in the `.ly`, before the chord where the tone enters.
  - The dal niente hairpin now runs on A, from D4 at 2376 to F♯4 at 2415.5, the first full-strength tone. The al niente hairpin
    is on A from C♯4 at 2639.
- **Tape** (`tape.tsv`, 96 tones). The tape uses the same chord writing, on two small stemless staves: C4 and up (treble) and below C4 (bass).
  Its range is B2-E6, too wide for the old single treble-8 staff. Same-note overlaps merge (12 pairs, so 84 noteheads). Tones at `rel_db` ≤ −8
  are small. No cents are printed. The upper staff carries the cues "Vowels.wav starts" (2382.68) and "Vowels.wav ends" (2644.8).
  The chords were checked against the chord list in `pitches/README.md`, and all 14 of its chords are there: B2, then E3; C3 C4 G4 C5 with E4 E5;
  D3 D4 F♯4 A4; C♯3 with A4 G4 G5; B2 B3 F♯4 B4; E3 E4 B4; E4 E5 F4 over E3; C3 F4 F5; D3 D4 E4 A4 E5; C♯3 E4 E5 B5 E6, then G♯4;
  B2 B4; E3 E4 D4; B3 B4; F4, then F♯4.

## What is uncertain, and what could not be notated

- **Voice count and who sang what.** A board mix cannot count voices or separate them. The recitation's four entries are placed at
  level steps, but the order S A T B is notional. The homophony, consonants, vowels and fricatives are on one "S A T B" staff.
  The held tones are assigned to staves by register only.
- **Claps vs plosives.** The detector cannot tell them apart. The 11 candidates are on the Cues line with "?". The Notion page's "Play with claps"
  is printed, but no clap is notated as certain.
- **Free pitches.** The pitches are machine estimates from the pitch pass's tracker, which groups partials into tones (method in `pitches/README.md`).
  Whether the singers chose these pitches freely, were led, or followed a plan is not on the board. Times are rounded to 0.25 s.
  The faint rows (small heads) may include another voice's partial or the room's tail. The median is 3 pitches at once.
- **The tape's role.** `Vowels.wav` is placed at board 2382.681 by GCC-PHAT, 15-20 dB under the voices. Its staves are the file's own tones,
  tracked from the clean file. The pitch pass finds that most low sung tones are **not** the tape. It left 13 board tones that match the tape out of
  `tones.tsv`, and the remaining low tones are on B and T. The tape's staves are a reference, not something to perform.
- **The two octave calls.** Two tones are an octave lower here than in the check's first reading:

  | board s | the check | here | why (`pitches/README.md`) |
  |---|---|---|---|
  | 2416-2424 | F♯5 | **F♯4** (A staff), loudest partial F♯5 | Lines at F♯4, F♯5, C♯6 and F♯6 start and stop together, and F♯5's level moves with F♯4's (correlation 0.94 over 11 s). C♯6 cannot be a partial of F♯5, so the fundamental is F♯4. |
  | 2460-2468 | G♯5 | **G♯4** (S staff), loudest partial G♯5 | The same test: the G♯4 line carries the G♯5 line. |

  Why they differ: the check took the winners of a harmonic sum on 2 s spectra, with the board's two channels averaged. The channels are largely
  in opposite polarity, so averaging cancels much of what they share. The pitch pass sums the channels' powers and takes a line as a partial of a
  lower one only when the two move together. A choir holding octaves can also move together, so these are the weakest kind of row.
  The Zoom recorder splits: it hears F♯4 at 2416 (this octave) and G♯5 at 2461 (the check's). Each is marked in the score
  "octave call: the check hears …". Also at 2387-2403, the check's "B4 / B3 low" is B3 here, with B4 its loudest partial.
- **Not notated:** the words inside the dense recitation (1906-2041). Whisper hears all eight lines overlapping but cannot say who said what when,
  so only "lines of Phrase 1, any order" in frames is written. The eroding text of 8b and the vowel/consonant alternation of 9 are notated only as framed cells,
  because no rhythm or pitch can be recovered from them. The fricatives' brief hums (C4, B♭3, D4, E4, C♯4) appear only in the editorial note,
  with no times. In the held tones, the tones that run past 2647 (B♭3 to 2648.8, E♭3 and B♭2 to 2647.8) are cut at the section's end.
  Cents are printed, not notated: there are no quarter-tone accidentals. The coarse "N lines" spreads are comments only. The 0.25 s rounding
  gives any tone shorter than 0.125 s a length of 0.25 s. The source of the thud (1807.9) and of the low sound with the house lights (2949-2962) is unknown.
  Section 6a's 2087-2111 is marked "[unclear]". Whisper's "At first" at 2190.77 has no Notion word, so that note has no lyric.
- **First places to listen**: as in the check, 1807.9; 2041-2066 and 2240-2290 (claps); 2290-2416; 2949-2962. In the held tones, from `pitches/README.md`:
  - 2416 and 2461: the two octave calls (F♯4 or F♯5; G♯4 or G♯5).
  - 2379-2404: the rub (B♭4 +46 against B4 −23), and whether the B3 under it is a voice or the octave below the B4.
  - 2484-2491: the low sweep (G♯2 B♭2 G♯2 G2), marked in the score "a voice, a thud or handling?".
  - Whether the low voices doubled the tape's basses.
