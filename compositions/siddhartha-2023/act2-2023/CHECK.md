# Total Abstraction, Act 2 (2023): the score checked against the recording's pitch

Agent-written, 2026-11-27, by `build.py` (this file is generated: edit `build.py`). Nobody has listened.

Zach, chat, 2026-11-25 (verbatim): "the 2020 score is not accurate. the 2023 needs to be checked against the actual recording.
but yes the house style would be preferred at the end." Zach, 2026-11-27 (`vision/present.toml` ans-185, verbatim): "duration keeps
going. take opera and anthem into notation re-engrave".

## What this pass did

Before it, the score's pitches were reconciled with the pitch data only in the held tones, 2370-2647 s (277 s of the 1204 s): every tone
there is read straight from `pitches/tones.tsv` and `pitches/tape.tsv`, and stays as it was. Every other section was written from the
check's level map and whisper (`sections.md`, `transcript-words.tsv`) and carried no pitch, except two editorial notes that named
pitches with no times (section 14's hums, section 16's low sound).

This pass ran the held tones' own tracker (`portfolio/siddhartha-2023/check-2023/pitches/track.py`, through `pitches.py`'s tone rule)
over every other second of the piece, 1786-2370 and 2647-2990, on the board recording `Church_10_21_2023.wav`, with the OBS room
microphone as the independent witness (`pitches/outside.py`, output `pitches/outside.tsv`, 703 tones). So all 1204 s of the piece
are now checked against pitch data. The one exception is the opening thud (1807.9), whose energy (74-90 Hz) sits at the tracker's
75 Hz floor: it is marked "pitch unchecked" in the score.

A tone found there corrects the score, and is written on the new "pitch heard" staves, when:
- the tracker holds it steady: 1.5 s or more, with its 10th-90th percentile pitch within 60 cents (speech glides further);
- it is not mains hum (within 20 cents of a multiple of 60 Hz);
- its loudest partial stands at -30.5 dB or more, 6 dB over the loudest steady tone the tracker finds in the room before and after
  the piece (sections 0, 15 and 17: -36.5 dB). Under that line, a steady tone cannot be told from the room.

Confidence, for each tone written:
- **high**: -24.5 dB or more (12 dB over the room), within 6 dB of the loudest sound at the time, and the OBS holds the same pitch;
- **medium**: the OBS holds the same pitch (within 50 cents over 40% of the tone);
- **ambiguous**: the OBS holds nothing there, or only the octave. The head is in parentheses and the score marks it
  "[ambiguous: …]". The tone is on the board but not confirmed by a second microphone, or its octave is not settled.

50 tones were written: 5 high, 21 medium, 24 ambiguous.

In the spoken sections (3-8c) a steady pitch may be a spoken vowel held long, rather than a sung tone. The machine cannot tell which.
The words stay on their own staff, and the pitch staff only says that a steady pitch was there.

## Every correction

Bar = the bar of that score (each score restarts its bars; one bar is 8 s at ♩ = 30, 4 s at ♩ = 60; the score prints board times,
not bar numbers). Level = the tone's loudest partial, dB re full scale, channels' power summed.

| section | where | written before | heard (board) | OBS | confidence |
|---|---|---|---|---|---|
| 3 | recitation, bar 5 (from 1868 s) | recitation frame: × heads, no pitch | A4 +22, 1873.72–1875.52 s (1.80 s), -29.8 dB, 5.3 dB under the loudest | octave below only | ambiguous |
| 3 | recitation, bar 7 (from 1884 s) | recitation frame: × heads, no pitch | G3 −19, 1885.47–1886.97 s (1.50 s), -22.4 dB, 0.2 dB under the loudest | octave above only | ambiguous |
| 3 | recitation, bar 7 (from 1884 s) | recitation frame: × heads, no pitch | A4 −42, 1890.57–1892.12 s (1.55 s), -28.4 dB, 3.5 dB under the loudest | same pitch | medium |
| 3 | recitation, bar 9 (from 1900 s) | recitation frame: × heads, no pitch | G♯4 −12, 1902.77–1904.37 s (1.60 s), -18.7 dB, 4.1 dB under the loudest | same pitch | high |
| 3 | recitation, bar 9 (from 1900 s) | recitation frame: × heads, no pitch | B♭4 +22, 1903.72–1906.12 s (2.40 s), -30.3 dB, 11.5 dB under the loudest | same pitch | medium |
| 3 | recitation, bar 9 (from 1900 s) | recitation frame: × heads, no pitch | C4 +6, 1905.67–1907.52 s (1.85 s), -25.1 dB, 3.6 dB under the loudest | nothing | ambiguous |
| 4 | recitation, bar 11 (from 1914 s) | recitation frame continues: no pitch | B♭4 +8, 1915.17–1916.77 s (1.60 s), -23.4 dB, 8.4 dB under the loudest | nothing | ambiguous |
| 4 | recitation, bar 11 (from 1914 s) | recitation frame continues: no pitch | F♯5 +47, 1915.57–1919.42 s (3.85 s), -23.3 dB, 14.6 dB under the loudest | same pitch | medium |
| 4 | recitation, bar 11 (from 1914 s) | recitation frame continues: no pitch | F♯4 +48, 1917.72–1919.27 s (1.55 s), -24.7 dB, 11.0 dB under the loudest | same pitch | medium |
| 4 | recitation, bar 11 (from 1914 s) | recitation frame continues: no pitch | F♯4 +12, 1917.97–1919.47 s (1.50 s), -22.1 dB, 4.5 dB under the loudest | octave above only | ambiguous |
| 4 | recitation, bar 11 (from 1914 s) | recitation frame continues: no pitch | B4 +33, 1921.22–1922.72 s (1.50 s), -30.2 dB, 12.3 dB under the loudest | nothing | ambiguous |
| 4 | recitation, bar 12 (from 1922 s) | recitation frame continues: no pitch | A4 −1, 1928.67–1930.77 s (2.10 s), -16.1 dB, 4.2 dB under the loudest | same pitch | high |
| 4 | recitation, bar 12 (from 1922 s) | recitation frame continues: no pitch | A3 −13, 1929.27–1930.82 s (1.55 s), -20.4 dB, 4.3 dB under the loudest | octave above only | ambiguous |
| 4 | recitation, bar 17 (from 1962 s) | recitation frame continues: no pitch | F♯5 +19, 1965.82–1967.67 s (1.85 s), -30.3 dB, 14.4 dB under the loudest | nothing | ambiguous |
| 4 | recitation, bar 18 (from 1970 s) | recitation frame continues: no pitch | G♯4 −40, 1976.27–1978.12 s (1.85 s), -20.7 dB, 0.0 dB under the loudest | same pitch | high |
| 4 | recitation, bar 21 (from 1994 s) | recitation frame continues: no pitch | C♯4 −17, 1998.37–2000.02 s (1.65 s), -27.5 dB, 5.0 dB under the loudest | nothing | ambiguous |
| 4 | recitation, bar 22 (from 2002 s) | recitation frame continues: no pitch | G4 −20, 2003.57–2005.12 s (1.55 s), -26.8 dB, 4.4 dB under the loudest | same pitch | medium |
| 4 | recitation, bar 22 (from 2002 s) | recitation frame continues: no pitch | E♭4 +48, 2005.07–2007.07 s (2.00 s), -29.4 dB, 8.5 dB under the loudest | nothing | ambiguous |
| 4 | recitation, bar 24 (from 2018 s) | recitation frame continues: no pitch | F♯5 −4, 2018.07–2019.77 s (1.70 s), -29.2 dB, 11.8 dB under the loudest | nothing | ambiguous |
| 4 | recitation, bar 24 (from 2018 s) | recitation frame continues: no pitch | E5 −38, 2020.12–2021.92 s (1.80 s), -23.0 dB, 7.9 dB under the loudest | same pitch | medium |
| 4 | recitation, bar 25 (from 2026 s) | recitation frame continues: no pitch | B♭4 −16, 2028.52–2030.27 s (1.75 s), -26.1 dB, 7.3 dB under the loudest | same pitch | medium |
| 4 | recitation, bar 26 (from 2034 s) | recitation frame continues: no pitch | D5 −6, 2035.17–2036.72 s (1.55 s), -26.0 dB, 10.6 dB under the loudest | nothing | ambiguous |
| 5 | recitation, bar 29 (from 2057 s) | recitation frame continues: no pitch | A4 +23, 2060.42–2062.97 s (2.55 s), -25.6 dB, 5.8 dB under the loudest | nothing | ambiguous |
| 6a | homophony, bar 2 (from 2070 s) | × cell (speech), no pitch | B4 −27, 2071.02–2072.72 s (1.70 s), -25.9 dB, 9.5 dB under the loudest | same pitch | medium |
| 6a | homophony, bar 3 (from 2074 s) | × cell (speech), no pitch | E♭5 +24, 2076.32–2077.97 s (1.65 s), -30.1 dB, 12.2 dB under the loudest | same pitch | medium |
| 6a | homophony, bar 4 (from 2078 s) | × cell (speech), no pitch | D5 +6, 2080.92–2082.67 s (1.75 s), -27.4 dB, 13.0 dB under the loudest | octave below only | ambiguous |
| 6a | homophony, bar 5 (from 2082 s) | × cell (speech), no pitch | G4 +32, 2084.97–2087.07 s (2.10 s), -23.3 dB, 5.7 dB under the loudest | same pitch | high |
| 6a | homophony, bar 9 (from 2098 s) | × cell (speech), no pitch | E♭5 +14, 2098.82–2100.37 s (1.55 s), -26.4 dB, 11.4 dB under the loudest | same pitch | medium |
| 6a | homophony, bar 12 (from 2110 s) | × cell (speech), no pitch | G3 +43, 2113.42–2115.97 s (2.55 s), -20.5 dB, 5.0 dB under the loudest | same pitch | high |
| 6a | homophony, bar 13 (from 2114 s) | × cell (speech), no pitch | B♭4 −31, 2115.27–2116.82 s (1.55 s), -26.7 dB, 10.4 dB under the loudest | octave above only | ambiguous |
| 6a | homophony, bar 14 (from 2118 s) | × cell (speech), no pitch | G3 −4, 2121.17–2124.97 s (3.80 s), -26.3 dB, 1.3 dB under the loudest | nothing | ambiguous |
| 6a | homophony, bar 15 (from 2122 s) | × cell (speech), no pitch | G3 +21, 2125.32–2127.32 s (2.00 s), -22.1 dB, 1.2 dB under the loudest | octave above only | ambiguous |
| 6b | homophony, bar 21 (from 2143 s) | × word notes (speech), no pitch | D3 +23, 2145.27–2146.92 s (1.65 s), -28.7 dB, 0.0 dB under the loudest | same pitch | medium |
| 6b | homophony, bar 23 (from 2151 s) | × word notes (speech), no pitch | A3 −21, 2153.82–2155.47 s (1.65 s), -29.3 dB, 6.5 dB under the loudest | octave above only | ambiguous |
| 6b | homophony, bar 26 (from 2163 s) | × word notes (speech), no pitch | E♭5 −29, 2165.52–2167.17 s (1.65 s), -24.3 dB, 6.2 dB under the loudest | same pitch | medium |
| 8a | consonants, bar 4 (from 2198 s) | × word notes or rest, no pitch | G♯3 +6, 2198.72–2200.27 s (1.55 s), -22.7 dB, 0.0 dB under the loudest | octave above only | ambiguous |
| 8a | consonants, bar 7 (from 2210 s) | × word notes or rest, no pitch | D5 +16, 2211.67–2213.37 s (1.70 s), -21.4 dB, 6.5 dB under the loudest | nothing | ambiguous |
| 8b | consonants, bar 9 (from 2215 s) | framed cell (× heads), no pitch | G2 +13, 2217.72–2220.17 s (2.45 s), -27.1 dB, 0.0 dB under the loudest | same pitch | medium |
| 8b | consonants, bar 9 (from 2215 s) | framed cell (× heads), no pitch | A4 −4, 2218.52–2220.02 s (1.50 s), -26.0 dB, 8.3 dB under the loudest | same pitch | medium |
| 8b | consonants, bar 12 (from 2227 s) | framed cell (× heads), no pitch | B4 +5, 2227.42–2229.97 s (2.55 s), -30.2 dB, 8.9 dB under the loudest | octave above only | ambiguous |
| 8b | consonants, bar 13 (from 2231 s) | framed cell (× heads), no pitch | A4 −41, 2232.62–2234.17 s (1.55 s), -24.2 dB, 6.4 dB under the loudest | same pitch | medium |
| 8b | consonants, bar 14 (from 2235 s) | framed cell (× heads), no pitch | E3 −45, 2236.42–2238.47 s (2.05 s), -28.3 dB, 6.0 dB under the loudest | same pitch | medium |
| 8c | consonants, bar 20 (from 2256 s) | framed cell (× heads), no pitch | B♭4 −17, 2256.67–2258.22 s (1.55 s), -28.4 dB, 1.8 dB under the loudest | same pitch | medium |
| 8c | consonants, bar 27 (from 2284 s) | framed cell (× heads), no pitch | B4 +25, 2287.42–2289.87 s (2.45 s), -25.6 dB, 8.7 dB under the loudest | same pitch | medium |
| 8c | consonants, bar 28 (from 2288 s) | framed cell (× heads), no pitch | B♭3 −19, 2288.62–2290.27 s (1.65 s), -27.6 dB, 3.1 dB under the loudest | octave above only | ambiguous |
| 9 | vowels, bar 2 (from 2298 s) | framed cell (× heads), no pitch | G3 +30, 2301.37–2303.52 s (2.15 s), -26.5 dB, 1.2 dB under the loudest | nothing | ambiguous |
| 9 | vowels, bar 4 (from 2314 s) | framed cell (× heads), no pitch | A3 +3, 2317.17–2318.82 s (1.65 s), -30.0 dB, 0.1 dB under the loudest | same pitch | medium |
| 9 | vowels, bar 6 (from 2330 s) | framed cell (× heads), no pitch | G3 +24, 2335.72–2338.92 s (3.20 s), -30.4 dB, 0.0 dB under the loudest | nothing | ambiguous |
| 14 | denouement, bar 1 (from 2647 s) | framed cell (× heads); hums only in the editorial note, no times | B♭3 −3, 2650.37–2653.92 s (3.55 s), -29.4 dB, 0.0 dB under the loudest | same pitch | medium |
| 16 | denouement, bar 40 (from 2949 s) | cue: "a low, partly pitched sound (G3, A2–B♭2)", no pitch notated | G♯3 −37, 2953.52–2957.82 s (4.30 s), -24.7 dB, 0.0 dB under the loudest | same pitch | medium |

Tones written, by section: 0: 0, 1: 0, 2: 0, 3: 6, 4: 16, 5: 1, 6a: 9, 6b: 3, 7: 0, 8a: 2, 8b: 5, 8c: 3, 9: 3, 14: 1, 15: 0, 16: 1, 17: 0.

## Bars marked ambiguous (24)

| section | where | written before | heard (board) | OBS | confidence |
|---|---|---|---|---|---|

| 3 | recitation, bar 5 (from 1868 s) | recitation frame: × heads, no pitch | A4 +22, 1873.72–1875.52 s (1.80 s), -29.8 dB, 5.3 dB under the loudest | octave below only | ambiguous |
| 3 | recitation, bar 7 (from 1884 s) | recitation frame: × heads, no pitch | G3 −19, 1885.47–1886.97 s (1.50 s), -22.4 dB, 0.2 dB under the loudest | octave above only | ambiguous |
| 3 | recitation, bar 9 (from 1900 s) | recitation frame: × heads, no pitch | C4 +6, 1905.67–1907.52 s (1.85 s), -25.1 dB, 3.6 dB under the loudest | nothing | ambiguous |
| 4 | recitation, bar 11 (from 1914 s) | recitation frame continues: no pitch | B♭4 +8, 1915.17–1916.77 s (1.60 s), -23.4 dB, 8.4 dB under the loudest | nothing | ambiguous |
| 4 | recitation, bar 11 (from 1914 s) | recitation frame continues: no pitch | F♯4 +12, 1917.97–1919.47 s (1.50 s), -22.1 dB, 4.5 dB under the loudest | octave above only | ambiguous |
| 4 | recitation, bar 11 (from 1914 s) | recitation frame continues: no pitch | B4 +33, 1921.22–1922.72 s (1.50 s), -30.2 dB, 12.3 dB under the loudest | nothing | ambiguous |
| 4 | recitation, bar 12 (from 1922 s) | recitation frame continues: no pitch | A3 −13, 1929.27–1930.82 s (1.55 s), -20.4 dB, 4.3 dB under the loudest | octave above only | ambiguous |
| 4 | recitation, bar 17 (from 1962 s) | recitation frame continues: no pitch | F♯5 +19, 1965.82–1967.67 s (1.85 s), -30.3 dB, 14.4 dB under the loudest | nothing | ambiguous |
| 4 | recitation, bar 21 (from 1994 s) | recitation frame continues: no pitch | C♯4 −17, 1998.37–2000.02 s (1.65 s), -27.5 dB, 5.0 dB under the loudest | nothing | ambiguous |
| 4 | recitation, bar 22 (from 2002 s) | recitation frame continues: no pitch | E♭4 +48, 2005.07–2007.07 s (2.00 s), -29.4 dB, 8.5 dB under the loudest | nothing | ambiguous |
| 4 | recitation, bar 24 (from 2018 s) | recitation frame continues: no pitch | F♯5 −4, 2018.07–2019.77 s (1.70 s), -29.2 dB, 11.8 dB under the loudest | nothing | ambiguous |
| 4 | recitation, bar 26 (from 2034 s) | recitation frame continues: no pitch | D5 −6, 2035.17–2036.72 s (1.55 s), -26.0 dB, 10.6 dB under the loudest | nothing | ambiguous |
| 5 | recitation, bar 29 (from 2057 s) | recitation frame continues: no pitch | A4 +23, 2060.42–2062.97 s (2.55 s), -25.6 dB, 5.8 dB under the loudest | nothing | ambiguous |
| 6a | homophony, bar 4 (from 2078 s) | × cell (speech), no pitch | D5 +6, 2080.92–2082.67 s (1.75 s), -27.4 dB, 13.0 dB under the loudest | octave below only | ambiguous |
| 6a | homophony, bar 13 (from 2114 s) | × cell (speech), no pitch | B♭4 −31, 2115.27–2116.82 s (1.55 s), -26.7 dB, 10.4 dB under the loudest | octave above only | ambiguous |
| 6a | homophony, bar 14 (from 2118 s) | × cell (speech), no pitch | G3 −4, 2121.17–2124.97 s (3.80 s), -26.3 dB, 1.3 dB under the loudest | nothing | ambiguous |
| 6a | homophony, bar 15 (from 2122 s) | × cell (speech), no pitch | G3 +21, 2125.32–2127.32 s (2.00 s), -22.1 dB, 1.2 dB under the loudest | octave above only | ambiguous |
| 6b | homophony, bar 23 (from 2151 s) | × word notes (speech), no pitch | A3 −21, 2153.82–2155.47 s (1.65 s), -29.3 dB, 6.5 dB under the loudest | octave above only | ambiguous |
| 8a | consonants, bar 4 (from 2198 s) | × word notes or rest, no pitch | G♯3 +6, 2198.72–2200.27 s (1.55 s), -22.7 dB, 0.0 dB under the loudest | octave above only | ambiguous |
| 8a | consonants, bar 7 (from 2210 s) | × word notes or rest, no pitch | D5 +16, 2211.67–2213.37 s (1.70 s), -21.4 dB, 6.5 dB under the loudest | nothing | ambiguous |
| 8b | consonants, bar 12 (from 2227 s) | framed cell (× heads), no pitch | B4 +5, 2227.42–2229.97 s (2.55 s), -30.2 dB, 8.9 dB under the loudest | octave above only | ambiguous |
| 8c | consonants, bar 28 (from 2288 s) | framed cell (× heads), no pitch | B♭3 −19, 2288.62–2290.27 s (1.65 s), -27.6 dB, 3.1 dB under the loudest | octave above only | ambiguous |
| 9 | vowels, bar 2 (from 2298 s) | framed cell (× heads), no pitch | G3 +30, 2301.37–2303.52 s (2.15 s), -26.5 dB, 1.2 dB under the loudest | nothing | ambiguous |
| 9 | vowels, bar 6 (from 2330 s) | framed cell (× heads), no pitch | G3 +24, 2335.72–2338.92 s (3.20 s), -30.4 dB, 0.0 dB under the loudest | nothing | ambiguous |

## What the tracker does not find

- **Section 14, the hums.** The check (`sections.md`) names C4, B♭3, D4, E4 and C♯4. Over the room, the tracker holds only B♭3
  (2650.4-2653.9, −3 cents, OBS the same). It finds C4 at 2724.1 and 2773.1 at −47 and −55 dB, 17 and 24 dB under the room line,
  and no steady D4, E4 or C♯4 at all. The editorial note says so; the other hums are not written.
- **Section 16, the low sound.** The check names G3 and A2-B♭2. The tracker holds one steady tone, G♯3 −37 cents (63 cents over G3),
  2953.5-2957.8, at −24.7 dB, and the OBS holds it too. Near A2 and B♭2 it finds only lines that glide by 76 cents or more (B♭2 −47 and −27, A2 −47).
  The G♯3 is written; the A2-B♭2 lines are not.
- **Silence, room and rests** (sections 0, 2, 7, 15, 17): no steady tone over the room line. These bars are checked and stay rests.
  The tracker's steady tones there are the room's own (-36.5 dB at most) and mains hum, mostly at 120 Hz.

## What this pass did not check

- The words: their onsets are whisper's (`transcript-words.tsv`), as before. Whether the 6b homophony was spoken or chanted
  is not settled by pitch: its three steady tones (D3, A3, E♭5) last 1.65 s each, 8-12 s apart.
- The clap candidates on the Cues line (unchanged).
- The held tones 2370-2647 (unchanged; checked by the pitch pass, `pitches/README.md`).
- Pitches shorter than 1.5 s, and anything at the room's level. The tracker cannot separate a voice from the room there.
