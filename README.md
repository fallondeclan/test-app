# Quiz CLI

An interactive command-line quiz game for learning and reviewing JavaScript, Node.js, and general programming concepts. The application runs entirely in Node.js, uses built-in modules only, and provides category selection, configurable quiz length, shuffled questions, immediate feedback, explanations, progress tracking, and final score review.

## Project Overview

Quiz CLI is an educational terminal application implemented with native JavaScript ES modules. It demonstrates practical Node.js and JavaScript concepts through a playable quiz experience.

### Features

- Choose from JavaScript Basics, Node.js Fundamentals, and General Programming.
- Play all questions or select 3 or 5 questions when the category supports them.
- Receive immediate feedback and answer explanations.
- Track progress with a terminal progress bar.
- Review incorrect answers at the end of a round.
- Play multiple rounds without restarting.
- Use terminal colors and formatting without third-party packages.
- Load quiz content from `data/questions.json`, separate from application logic.

## Setup Instructions

### Prerequisites

- Node.js 18.0.0 or later
- npm, included with Node.js
- A terminal that supports standard ANSI color escape codes

### Installation

1. Clone or download the repository.
2. Open a terminal in the project directory.
3. Install the project setup:

   ```bash
   npm install
   ```

The project currently has no external runtime dependencies.

### Start the application

```bash
npm start
```

You can also run the entry point directly:

```bash
node index.js
```

### Run tests

```bash
npm test
```

This invokes Node.js's built-in test runner. No test files are currently included in the repository.

## Usage Examples

After starting the application, follow the terminal prompts:

```text
Choose a category:

  1. JavaScript Basics
  2. Node.js Fundamentals
  3. General Programming

Your choice (enter number): 1

How many questions?

  1. All questions
  2. 3 questions
  3. 5 questions

Your choice (enter number): 2

Starting quiz...

Press Enter to continue...
```

For each question, enter the number matching an answer option. The application reports whether it is correct, displays an explanation when available, and waits for Enter before continuing. At the end, it shows the category, score, percentage, performance message, and incorrect-answer review.

To play again, enter `y` when prompted:

```text
Would you like to play again? (y/n): y
```

Any response that does not start with `y` exits the application.

## File Structure

```text
.
├── index.js              # Application entry point and main interaction loop
├── package.json          # Project metadata and npm scripts
├── README.md             # Project documentation
├── data/
│   └── questions.json    # Categories, questions, options, answers, explanations
└── src/
    ├── colors.js         # ANSI color and formatting helpers
    ├── input.js          # Readline interface and prompt utilities
    └── quiz.js            # Quiz class, scoring, shuffling, progress, results
```

## Application Details

### Application flow

1. `index.js` creates a Node.js `readline` interface.
2. It reads and parses `data/questions.json` using `node:fs/promises`.
3. The user selects a category and quiz length.
4. A `Quiz` instance is created with the selected questions.
5. Questions are shuffled using the Fisher-Yates algorithm.
6. Each question is displayed with numbered options and progress information.
7. Answers are recorded and scored immediately.
8. Final results and incorrect-answer review are displayed.
9. The user can start another quiz or exit.
10. The readline interface is closed in a `finally` block, including after errors.

### Question data format

Each category under `categories` in `data/questions.json` contains a display `name` and a `questions` array. Each question contains:

- `question`: Question text.
- `options`: Answer choices.
- `answer`: Zero-based index of the correct option.
- `explanation`: Optional text shown after answering.

When editing questions, ensure `answer` refers to the correct zero-based position in `options`.

### Technical implementation

- ES module syntax is enabled by `"type": "module"` in `package.json`.
- Uses only Node.js built-ins: `fs/promises`, `url`, `path`, and `readline`.
- Uses Promises and `async`/`await` for interactive input.
- Encapsulates quiz state, scoring, answer history, and results in the `Quiz` class.
- Uses ANSI escape sequences for colors, with no color-library dependency.
- Resolves the data path relative to the module file.
- Re-prompts for invalid numeric selections.
- Displays performance messages based on the final percentage.

## Configuration and Content Updates

Edit `data/questions.json` to change quiz content. A new category should contain a `name` and `questions` array matching the existing structure. The category list is derived automatically from the keys under `categories`.

The application takes questions from the category list and shuffles the selected set when constructing the quiz. The 3- and 5-question choices appear only when enough questions are available.

## npm Scripts

| Command | Description |
| --- | --- |
| `npm start` | Launches the interactive quiz CLI. |
| `npm test` | Runs Node.js's built-in test runner. |

## Troubleshooting

- **Application does not start:** Verify Node.js with `node --version`; it must be version 18 or later.
- **Questions cannot be loaded:** Confirm `data/questions.json` exists and contains valid JSON.
- **Invalid selection:** Enter a number shown in the current menu.
- **No colors:** The quiz remains usable; the terminal may not support ANSI colors.
- **No tests run:** The script exists, but the repository currently contains no test files.

## Project Metadata

- Package name: `quiz-cli`
- Version: `1.0.0`
- License: MIT
- Runtime: Node.js `>=18.0.0`
- Module system: ES modules
- Original repository description: EliteA training

## License

This project is marked as licensed under the MIT license in `package.json`.
