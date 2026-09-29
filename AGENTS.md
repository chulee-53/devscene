# DevScene - Codex Project Instructions

## Project Overview

DevScene is a Windows-first desktop application for developers.

Its purpose is to let developers launch an entire project-specific development environment with one click or one global keyboard shortcut.

The core product concept is:

> Do not launch individual apps. Launch the project.

Developers often work on multiple projects, and each project requires a different combination of:

- IDE
- project directory
- terminal
- terminal commands
- GitHub repository
- browser
- localhost URL
- Notion page
- Figma page
- other applications or URLs

DevScene stores these as a Workspace and launches them together.

Example:

Workspace: ODI

- Open `C:\Projects\ODI\FE` in VSCode
- Open a terminal in `C:\Projects\ODI\FE`
- Run `npm run dev`
- Open the project's GitHub repository
- Open `http://localhost:3000`
- Optionally open project-specific Notion/Figma URLs

The user can then launch this environment through:

- a Launch button
- an optional global shortcut

---

## Product Scope

The MVP is intended for developers in general.

Initial automatic project detection may be optimized for common web development projects, but the architecture must remain generic enough to support:

- frontend projects
- backend projects
- Python projects
- Unity projects
- other development environments

Do not design the core domain model around only Node.js or VSCode.

---

## MVP Features

The MVP must support:

1. Creating a Workspace
2. Editing a Workspace
3. Deleting a Workspace
4. Selecting a project root folder
5. Opening an IDE with a project directory
6. Opening arbitrary desktop applications
7. Opening URLs
8. Opening a terminal in the project directory
9. Running configured terminal commands
10. Launching all configured workspace items
11. Assigning an optional global keyboard shortcut
12. Saving all workspace settings locally
13. Automatically analyzing a project folder and recommending configuration

No account system is required.

No backend server is required.

No cloud database is required.

The MVP is free and local-first.

---

## Automatic Project Analysis

Automatic recommendations should initially be rule-based.

Do NOT add AI/LLM-based project analysis unless explicitly requested.

Examples:

### Git

If `.git` exists:

- recognize the folder as a Git repository
- inspect the Git remote
- if the remote points to GitHub, recommend opening the GitHub repository

### Node.js

If `package.json` exists:

- recognize a Node.js-based project
- inspect `scripts`
- recommend useful scripts such as:
  - `npm run dev`
  - `npm start`
- detect the package manager when possible

### Common project files

Possible signals include:

- `.git`
- `package.json`
- `package-lock.json`
- `pnpm-lock.yaml`
- `yarn.lock`
- `requirements.txt`
- `pyproject.toml`
- `.vscode`
- `README.md`

Recommendations should always be editable by the user.

Project-specific services such as Notion, Figma, Jira, or internal documentation usually cannot be inferred from the local repository and should initially be added manually.

---

## Product Flow

The primary flow is:

1. User creates a Workspace
2. User chooses a project directory
3. DevScene analyzes the project
4. DevScene proposes detected tools/actions
5. User accepts, removes, or adds items
6. User saves the Workspace
7. Workspace appears on the Home screen
8. User clicks Launch or uses the configured global shortcut
9. DevScene launches the entire project environment

The first vertical slice should be:

> Launch button → open a specified project directory in VSCode

After that works, extend the same architecture to URLs, terminals, commands, and multiple launch items.

---

## Planned Later Features

Do NOT implement these unless explicitly requested:

- window position/layout restoration
- multi-monitor workspace restoration
- cloud sync
- accounts
- team workspaces
- cross-device sync
- macOS support
- Linux support
- AI recommendations

Window layout restoration is planned for a later version and should not be forgotten.

---

## Technology Stack

Current stack:

- Electron
- React
- TypeScript
- Vite
- Node.js

Planned UI/tooling:

- Tailwind CSS
- shadcn/ui
- Zustand
- Zod
- electron-store
- Vitest

Windows is the first supported OS.

---

## TypeScript Configuration

This project uses TypeScript 5.9.

Do not downgrade TypeScript to the original Electron Forge template version.

Important settings:

```json
{
  "compilerOptions": {
    "target": "ESNext",
    "module": "ESNext",
    "moduleResolution": "bundler",
    "jsx": "react-jsx",
    "allowJs": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "noImplicitAny": true,
    "sourceMap": true,
    "outDir": "dist",
    "resolveJsonModule": true
  }
}