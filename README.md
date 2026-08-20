# test-app

## Project Description

`test-app` is an interactive command-line quiz application built with Node.js. It helps users practice:

- JavaScript basics
- Node.js fundamentals
- general programming concepts

The app lets users choose a quiz category, select how many questions to answer, track their score, review explanations, and revisit incorrect answers at the end of the session.

## Features

- Category-based quiz sessions
- Adjustable number of questions per run
- Randomized question order
- Multiple-choice answer selection
- Immediate correct/incorrect feedback
- Question explanations when available
- Final score and performance summary
- Review of incorrect answers after the quiz
- Colored terminal output
- Replay prompt to start another session

## Technology Stack

- **Language:** JavaScript
- **Runtime:** Node.js `>=18.0.0`
- **Module system:** ES Modules (`"type": "module"`)
- **APIs used:** Built-in Node.js modules only
  - `node:fs/promises`
  - `node:readline`
  - `node:path`
  - `node:url`
- **Package manager:** npm
- **Testing:** Node test runner (`node --test`)
- **Dependencies:** No third-party runtime dependencies

## Project Structure

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

### Key files

- **`index.js`**  
  Application entry point. Loads quiz data, handles category and question-count selection, runs the quiz loop, displays results, and prompts to play again.

- **`src/input.js`**  
  Terminal input helpers built on `readline`. Provides prompting, selection, confirmation, and “press Enter” interactions.

- **`src/quiz.js`**  
  Main quiz engine and state management. Handles shuffling, scoring, progress tracking, result rendering, and review of missed questions.

- **`src/colors.js`**  
  ANSI color formatting helpers for terminal output.

- **`data/questions.json`**  
  Local quiz data source containing categories and multiple-choice questions.

## Prerequisites

- Node.js **18.0.0 or later**
- npm

## Setup Instructions

1. Clone the repository.
2. Change into the project directory:

   ```bash
   cd test-app
   ```

3. Install dependencies:

   ```bash
   npm install
   ```

   > This project has no external runtime dependencies, but running `npm install` is the standard setup step and prepares the project for use with npm scripts.

## Configuration

The quiz content is stored locally in `data/questions.json`.

### Expected question data format

The quiz data uses a category-based structure similar to:

- `categories`
  - category ID
    - `name`
    - `questions[]`
      - `question`
      - `options[]`
      - `answer` — zero-based index of the correct option
      - `explanation` — optional

### Package configuration

Important values from `package.json`:

- `type: "module"`
- `main: "index.js"`
- `engines.node: ">=18"`
- `license: "MIT"`

## How to Run

Start the application with:

```bash
npm start
```

This runs:

```bash
node index.js
```

You can also run it directly:

```bash
node index.js
```

When the app starts, it displays a colored banner and guides you through:

1. selecting a category
2. selecting the number of questions
3. answering each question
4. viewing the final score and review
5. deciding whether to play again

## Testing

Run the test command with:

```bash
npm test
```

This executes:

```bash
node --test
```

### Notes

- No test files are present in the repository snapshot.
- As a result, `npm test` may complete without running any actual test cases.

## API / Usage

This is a **CLI-only application**.

- No HTTP API
- No REST endpoints
- No server
- No external service integration

### Typical usage flow

1. Launch the app.
2. Choose a quiz category.
3. Choose how many questions to answer.
4. Enter your answer by selecting a numbered option.
5. Review feedback and explanations.
6. Read your score summary and missed questions.
7. Choose whether to replay.

## Database

No database is used.

All quiz content is stored locally in:

- `data/questions.json`

## Docker

No Docker configuration is included in this repository.

- No `Dockerfile`
- No `docker-compose.yml`

## CI/CD

No CI/CD configuration was found in the repository.

- No GitHub Actions workflow files
- No Jenkins pipeline
- No GitLab CI configuration

## Architecture

The application uses a simple layered CLI architecture:

1. **Entry point** — `index.js`
2. **Data source** — `data/questions.json`
3. **Input layer** — `src/input.js`
4. **Quiz logic layer** — `src/quiz.js`
5. **Presentation layer** — `src/colors.js`

### Execution flow

- Load quiz data from JSON
- Let the user choose a category
- Let the user choose how many questions to answer
- Create a `Quiz` instance
- Shuffle and present questions
- Record answers and track progress
- Display score and performance feedback
- Review incorrect answers
- Prompt the user to play again

### Implementation details

- Questions are shuffled using the Fisher-Yates algorithm
- Progress is displayed with a text-based progress bar
- Incorrect answers are stored for later review
- The app includes top-level error handling and exits with status `1` on fatal errors

## Additional Information

- The app prints a colored terminal banner on startup.
- Terminal colors are handled without external libraries.
- The project is intentionally small and self-contained.
- Existing categories in the quiz data include:
  - `JavaScript Basics`
  - `Node.js Fundamentals`
  - `General Programming`

### Notes for contributors

Because the project uses only built-in Node.js modules, setup and execution are lightweight. Updating or expanding the quiz typically involves editing `data/questions.json` and, if needed, the logic in `src/quiz.js` or the terminal helpers in `src/input.js` and `src/colors.js`.