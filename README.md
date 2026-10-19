# Picture Spell

A Wordle-style spelling game for a 1st grader. One file, no build: `index.html`.

## Run it

```
python3 -m http.server 8765 --bind 127.0.0.1 --directory ~/3_personal/word-test
```

Then open http://127.0.0.1:8765/ . It also works opened straight from the file, but Safari on iPad needs it served to play speech reliably.

## How it plays

- A picture (emoji) of an everyday thing, with one blank per letter. Tap **Start** once; after that each new word is spoken half a second after it appears, and the speaker button repeats it.
- Tap letters, then the orange check. Green = right spot, yellow = in the word but the wrong spot, gray = not in the word. Gray keys turn off.
- **Easy** turns off every key that is not in the word from the start. **Normal** turns keys off only after a wrong guess.
- Each guess is read aloud when it is checked. A win spells the word letter by letter, pauses, then says the word, with confetti and a star. Six misses reveal the word.
- **ABC / abc** switches tiles and keys between upper and lower case. Stars, mode, and case are remembered on that device.
- Physical keyboard works: letters, Backspace, Enter (Enter also starts and advances).
- The square button at the top right goes full screen on a desktop browser.

## Layout

- Phones: picture pinned at the top, keyboard pinned at the bottom, the guess grid scrolls between them and follows the active row.
- Desktop and landscape tablets (900px and wider): picture and grid on the left, big keyboard on the right, everything on one screen.
- Light and dark themes follow the system setting.

## Word list

About 150 words, 3 to 6 letters, one emoji each, chosen so a 6-year-old names the picture with that exact word. Edit the `WORDS` array near the top of the script to add or remove entries. The first word of each session is always 3 or 4 letters.

## What was tested (2026-10-18)

Headless Chromium, 36 checks, all passing:

- Viewports 390x664 (iPhone with Safari bars), 820x1180 (iPad), 1180x820 (iPad landscape), 1352x760 (desktop, light and dark). No horizontal scroll, keyboard and picture on screen at every size.
- Wordle scoring with repeated letters (APPLE, COOKIE, SPOON), key colors never downgrade, easy-mode key hiding, taps during the flip animation queued into the next row, win and lose flows, star count, case toggle persistence, speech order and timing with a stubbed speech engine.

Not tested: real audio on a real iPad or iPhone. The speech code paths ran against a stub, so listen for the letter pause and the half-second delay on the first play.

A four-lens code review (game logic, 6-year-old usability, layout and theming, word list) ran over the first build. Every finding was applied before this version; the word list lost ship, tie, yarn, jar, nest, castle, and guitar (ambiguous pictures or silent letters) and gained taco, pen, panda, web, swan, robot, and bunny.
