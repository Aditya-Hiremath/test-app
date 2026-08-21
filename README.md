# quiz-cli

## Project Description

`quiz-cli` is a Node.js command-line quiz game for learning JavaScript and general programming concepts.

It loads multiple-choice questions from a local JSON file, lets the user choose a quiz category and question count, and then runs an interactive quiz session with scoring, explanations, and a review of missed questions.

The application is a small single-process CLI program with no external service dependencies.

## Features

- Interactive command-line quiz flow
- Category-based question selection
- Adjustable question count:
  - all questions
  - 3 questions
  - 5 questions
- Randomized question order
- Multiple-choice answers by numeric selection
- Immediate correct/incorrect feedback
- Explanations shown after questions when available
- Score tracking
- Progress indicator
- Final results summary with performance message
- Review of incorrect answers
- Play-again loop
- ANSI-colored terminal output

## Technology Stack

- **Language:** JavaScript
- **Runtime:** Node.js `>=18.0.0`
- **Module system:** ES Modules
- **CLI input:** Built-in `node:readline`
- **File I/O:** Built-in `node:fs/promises`
- **Package manager:** npm
- **Testing:** Node test runner via `node --test`
- **External runtime dependencies:** None

## Project Structure

The repository snapshot shows the application nested under `test-app/test-app/`.

```text
test-app/
└── test-app/
    ├── README.md
    ├── package.json
    ├── index.js
    ├── data/
    │   └── questions.json
    └── src/
        ├── colors.js
        ├── input.js
        └── quiz.js
```

### Important files

- **`index.js`** — application entry point; loads quiz data, shows the banner, prompts for category and question count, starts the quiz, and handles restart/fatal errors
- **`src/quiz.js`** — quiz engine; shuffles questions, tracks score, renders progress, evaluates answers, and shows final results
- **`src/input.js`** — terminal interaction helpers built on `readline`
- **`src/colors.js`** — ANSI color utilities for terminal styling
- **`data/questions.json`** — quiz content source
- **`package.json`** — project metadata and scripts

## Prerequisites

- **Node.js 18.0.0 or newer**
- **npm**

## Setup Instructions

1. Clone the repository.
2. Change into the application directory:

   ```bash
   cd test-app/test-app
   ```

3. There are no external runtime dependencies, so no additional setup is required before running the app.

## Configuration

This project does not use environment variables, a `.env` file, or external configuration.

### Quiz content

All quiz content is stored in:

- `data/questions.json`

### Data model

Each category in `questions.json` includes:

- `name`
- `questions[]`

Each question includes:

- `question`
- `options`
- `answer` as a zero-based index
- optional `explanation`

### Available categories

The current quiz content includes:

- **JavaScript Basics**
- **Node.js Fundamentals**
- **General Programming**

## How to Run

From the application directory (`test-app/test-app/`), run:

```bash
npm start
```

This uses:

```bash
node index.js
```

You can also run the app directly with:

```bash
node index.js
```

## Testing

The repository declares a test script in `package.json`:

```bash
npm test
```

This runs:

```bash
node --test
```

At the time of analysis, no test files were present in the repository snapshot, so the test command may complete without executing any tests.

## API / Usage

This is a CLI application and does **not** expose an HTTP API.

### Typical usage flow

1. Start the app.
2. Choose a quiz category.
3. Choose how many questions to answer.
4. Answer each multiple-choice question by number.
5. Review your score and missed questions.
6. Optionally play again.

## Database

No database is used.

Quiz content is stored locally in the JSON file:

- `data/questions.json`

There is no ORM, migration layer, or persistence backend.

## Docker

No Docker configuration was found in the repository.

- No `Dockerfile`
- No `docker-compose.yml`
- No containerization setup

## CI/CD

No CI/CD configuration was found in the repository.

- No GitHub Actions workflows
- No Jenkins configuration
- No GitLab CI files
- No deployment pipeline files

## Architecture

The application follows a simple modular CLI architecture:

1. **`index.js`** starts the program.
2. Questions are loaded from `data/questions.json`.
3. The user selects a category and question count.
4. `Quiz` in `src/quiz.js` runs the session:
   - shuffles questions using the Fisher-Yates algorithm
   - asks questions one at a time
   - checks answers
   - tracks progress and score
   - displays explanations and missed-question review
5. Final results are displayed.
6. The user can restart the quiz.

### Design goals

- Keep input handling separate from quiz logic
- Keep content separate from code
- Use only built-in Node.js APIs
- Provide a lightweight, dependency-free CLI experience

## Additional Information

### Package metadata

From `package.json`:

- **Name:** `quiz-cli`
- **Version:** `1.0.0`
- **Description:** Interactive command-line quiz game for learning JavaScript
- **Main entry:** `index.js`
- **License:** MIT

### Scripts

- `npm start` → `node index.js`
- `npm test` → `node --test`

### Implementation notes

- Uses ES modules (`"type": "module"`)
- Uses built-in Node.js APIs only
- Uses ANSI escape codes for terminal styling
- Tracks user answers and presents a results review at the end
- Displays explanations after questions when available

### Known repository state

- No test directory is present in the current snapshot
- No database, Docker, or CI/CD files are present
- The app lives in a nested folder: `test-app/test-app/`
