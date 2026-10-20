# Copilot instructions

## Project shape

Cosmic Quiz is a dependency-free, static web page implemented entirely in `index.html`. The document contains its own CSS, quiz markup, question data, and browser-side JavaScript; there is no application framework, package manifest, or separate build pipeline.

The page is organized around three views inside the main card: the intro, the active quiz, and the results. The script keeps quiz state in `questionIndex`, `score`, and `answered`; `renderQuestion()` updates the active question and answer buttons, `chooseAnswer()` handles scoring and feedback, and `showResults()` selects the completion message. The `questions` array is the source of truth for quiz content and length.

## Commands and validation

There are no configured build, test, or lint commands, and no automated test suite. To run the app, open `index.html` directly in a browser (or serve the folder with any static file server). To validate a change, exercise the start, answer, next-question, results, and restart flows in the browser; check both correct and incorrect answers.

## Code conventions

- Keep this project self-contained in `index.html` unless a change clearly requires introducing a separate asset or toolchain.
- Add or revise quiz content as entries in `questions`; each entry uses `category`, `prompt`, `answers`, zero-based `correct`, and `fact`. The intro's question count and progress bounds are derived from `questions.length`.
- Keep DOM references tied to the existing element IDs. `renderQuestion()` rebuilds answer buttons for each question, while the start/restart/next controls are wired once after the DOM.
- Use `textContent` for question and feedback copy. Answer labels are inserted as text after creating their elements; preserve this behavior for content rather than interpolating question data into HTML.
- Preserve the existing accessibility patterns: native buttons, live regions for quiz/results feedback, progressbar value updates, visible keyboard focus, and reduced-motion CSS.
- Styling is in the page's `<style>` block and uses shared CSS custom properties in `:root` for theme colors, with responsive and light-color-scheme overrides nearby.
