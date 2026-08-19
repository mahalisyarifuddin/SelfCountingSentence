**English** | [Bahasa Indonesia](README-id.md)

# SelfCountingSentence
Self-counting sentences, simplified.

## Introduction
SelfCountingSentence is a single-file, browser-based generator for **self-referential sentences** (also called autograms): sentences that correctly state how many letters they contain. Designed for linguists, puzzle enthusiasts, students of formal language, and anyone curious about self-reference, this tool completes an opening clause with a spelled-out count that is true of the finished sentence.

The interface and the generated count phrase support **fifteen languages**: English, Bahasa Indonesia, Español, العربية, Français, Português, اردو, Русский, Deutsch, Tiếng Việt, Kiswahili, Türkçe, Tagalog, فارسی, and Italiano.

## How It Works
You type an opening clause. The generator appends a language-specific tail — a spelled-out number plus the grammatically correct word for “letters” — and searches for a number *n* such that the complete sentence contains exactly *n* letters.

1. **Letter count**: Only Unicode letters (`\p{L}`) are counted. Spaces, punctuation, hyphens, and combining marks (for example Arabic harakat) are ignored, so *thirty-one* contributes nine letters, not ten.
2. **Language tail**: Each language has its own number speller and its own agreement rules for the counted noun (singular/plural, gender, Arabic *tamyīz*, Russian paucal forms, and so on).
3. **Fixed-point search**: If the opening clause has *b* letters and the tail for *n* has *t(n)* letters, a solution is any *n* where *n = b + t(n)*. The scan starts at *b* and tries up to **1000** successive candidate counts, so a miss reports a full 1000 iterations rather than giving up after a small neighbourhood. Long pasted paragraphs are counted once; only the short tail is re-spelled.
4. **Stability**: The smallest *n* that satisfies the identity is returned, together with how many candidates were examined. If none exists in the feasible range, the tool reports that no stable sentence could be generated.

Because the opening clause never changes during the search, the input is counted once and only the winning tail is assembled into a full sentence. Number words run through the hundreds of millions, so a very long clause still gets an exact spelled count rather than a “more than nine thousand” fallback.

## Quick Start
1. Download `SelfCountingSentence.html`.
2. Open it in any modern browser (Chrome, Edge, Firefox, Safari).
3. Optionally open **Settings** to choose a language and theme (Auto, Light, or Dark).
4. Type an opening clause, or click **Example** to use the built-in phrase for the current language.
5. Click **Generate sentence**, or press Ctrl+Enter (⌘↩ on a Mac).
6. Read the completed sentence and the iteration count.

Verified examples of the built-in phrases:

- English: *This sentence has thirty-one letters.*
- Bahasa Indonesia: *Kalimat ini memiliki tiga puluh enam huruf.*
- Español: *Esta oración tiene treinta y cinco letras.*
- Français: *Cette phrase compte trente lettres.*
- Deutsch: *Dieser Satz hat dreißig Buchstaben.*
- Kiswahili: *Sentensi hii ina herufi thelathini.*
- Türkçe: *Bu cümlede yirmi bir harf.*
- Tagalog: *Ang pangungusap na ito ay may apatnapu't apat na titik.*
- فارسی: *این جمله دارای بیست و دو حرف.*
- Italiano: *Questa frase contiene trentasette lettere.*

## Key Features
- **Fifteen languages**: English, Indonesian, Spanish, Arabic, French, Portuguese, Urdu, Russian, German, Vietnamese, Swahili, Turkish, Tagalog, Persian, and Italian — each with a native number speller.
- **Grammatical agreement**: Feminine numerals in Spanish, French, Italian, and Portuguese; German singular after any numeral ending in *ein*; Russian *буква / буквы / букв*; full Arabic *tamyīz*; Urdu sentence-final *۔*; Tagalog ligature linkers (*-ng* / *-g* / *na*); Swahili noun-first ordering (*herufi ...*); Turkish and Persian singular counted nouns (*harf* / *حرف*).
- **Unicode-aware counting**: Letters from any script count; combining marks do not.
- **RTL layout**: Arabic, Urdu, and Persian flip the whole interface, not just the result.
- **Dark/Light Theme**: Automatic or manual theme selection.
- **Example button**: Fills the language-specific starter phrase and generates immediately.
- **Long input**: The opening clause is a resizable text area, so you can paste a paragraph. Number words go through the hundreds of millions.
- **Single HTML file**: No installation, no dependencies, works completely offline.
- **Responsive design**: Works on desktop, tablet, and mobile devices.

## Use Cases
- **Puzzles and wordplay**: Building autograms and self-descriptive sentences.
- **Language teaching**: Demonstrating number words and noun agreement.
- **Linguistics**: Comparing how different languages encode counted nouns.
- **Education**: Introducing fixed-point search and self-reference with a concrete, checkable example.

## Understanding the Search
The sentence is always:

    <opening clause> + " " + <number words> + " " + <letters-word> + <terminator>

Only the tail depends on *n*, so:

    letters(sentence) = letters(clause) + letters(tail(n))

A solution is a fixed point of that function. Most opening clauses have one; some (for example a very short English fragment whose tail lengths skip the required total) have none, and the tool says so rather than returning a false count.

The search walks up to 1000 candidate values of *n* starting at *b*, so the smallest solution in that window wins and an unsuccessful run really does spend the full budget. Tails are memoised per language, so switching language or pressing Generate again reuses previous counts.

## Supported Languages

| Language | Example starter | Counted noun |
| --- | --- | --- |
| English | This sentence has | letter / letters |
| Bahasa Indonesia | Kalimat ini memiliki | huruf |
| Español | Esta oración tiene | letra / letras (feminine numerals) |
| العربية | هذه الجملة فيها | حرف / حرفان / أحرف / حرفًا |
| Français | Cette phrase compte | lettre / lettres (feminine numerals) |
| Português | Esta frase tem | letra / letras (feminine numerals) |
| اردو | اس جملے میں | حرف / حروف |
| Русский | В этом предложении | буква / буквы / букв |
| Deutsch | Dieser Satz hat | Buchstabe / Buchstaben |
| Tiếng Việt | Câu này có | chữ cái |
| Kiswahili | Sentensi hii ina | herufi |
| Türkçe | Bu cümlede | harf |
| Tagalog | Ang pangungusap na ito ay may | titik (with ligatures -ng / -g / na) |
| فارسی | این جمله دارای | حرف |
| Italiano | Questa frase contiene | lettera / lettere (feminine numerals) |

## Privacy & Data
All calculations happen locally in your browser. No data is sent to any server. The tool is completely offline once loaded.

## License
MIT License. See LICENSE for details.

## Contributions
Contributions, issues, and suggestions are welcome. Please open an issue to discuss ideas or submit a PR.
