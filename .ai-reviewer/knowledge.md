# stenoai-main reviewer notes

## Architecture
The `stenoai-main` codebase implements a macOS application designed for recording, transcribing, and summarizing meetings using AI. It consists of an Electron frontend located in the `app/` directory and a Python backend for processing audio, contained within the `src/` directory. The project promotes modular design, with distinct concerns divided across frontend and backend layers.

## Conventions
- **Directory Structure**: The root directory contains a clear separation between the Electron app (`app/`), the Python backend (`src/`), and the CLI interface represented by `simple_recorder.py`. Each module is logically contained, aiding discoverability.
- **Python Style**: Python code adheres to PEP 8 guidelines with type hints and docstrings, as highlighted in `src/audio_recorder.py` and others. The linter used is `ruff`, and version control practices emphasize clarity in commit messages.
- **JavaScript Style**: JavaScript files in the frontend use semicolons and `const`/`let` for variable declarations instead of `var`, as ensured in the `app/renderer/src/` files. Code quality is maintained with `eslint`.
- **Versioning**: Semantic versioning is applied manually for the project, as noted in `CONTRIBUTING.md`. Contributors focus on code quality, with maintainers handling version increments.
- **React + Vite**: The frontend employs React with Vite as the build tool, promoting modern React practices. TypeScript is used for type safety, as indicated in the `app/renderer/tsconfig.json`.

## Intentional non-standard choices
- None identified during the review of the specified files.

## Watch out for
- **Mixing Backend and Frontend Logic**: Ensure that the code in `app/main.js` selectively uses Electron internals without exposing unnecessary details to the frontend, maintaining a proper separation of concerns.
- **Hardcoding Values**: Avoid hardcoding sensitive or frequently changing configuration values directly into the codebase without abstraction or environment variables (as noted in `main.js` concerning `.env` values).
- **Queue Management**: In `main.js`, managing shortcut actions via a queue can create complexities if not handled correctly. Review any edge cases that might lead to missed or duplicated actions.
- **Component Design**: In React components, ensure props are well-defined and utilized, as any misuse can lead to unclear data flows, especially in parent-child component relationships as seen in `App.tsx`.