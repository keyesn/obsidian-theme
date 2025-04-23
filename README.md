# Obsidian Theme Development Guide

A personal project to learn CSS/styling by building a custom Obsidian theme.
**Focus**: Experimentation with Sass, Grunt automation, and Obsidian theming concepts.

---

## Table of Contents

One of the VSCode extensions is screwing with this and I can't stand the warnings.

---

## Setup Guide

### Prerequisites

- **Node.js** (v18+ recommended): [Download](https://nodejs.org/)

### 1. Initialize Project

```bash
# Clone your theme template (replace with your repo)
git clone https://github.com/your-username/obsidian-theme.git
cd obsidian-theme

# Install dependencies
npm install

# Install Grunt CLI globally (if not already installed)
npm install -g grunt-cli
```

### 2. Configure Paths

Create `.env` file in project root:

```env
OBSIDIAN_VAULT_PATH="/path/to/your/vault/.obsidian/themes"
```

---

## Development Workflow

### Grunt Automation Tasks

```bash
# Start development mode (watches files & auto-rebuilds)
grunt watch

# Manual production build
grunt build
```

**What happens during `grunt watch`:**

1. Compiles SCSS --> CSS
2. Combines CSS files
3. Minifies output
4. Copies theme to Obsidian vault
5. Watches for file changes

---

## Key Tools Explained

### NPM Packages

#### Core Packages

| Package  | Purpose                                      |
| -------- | -------------------------------------------- |
| `dotenv` | Loads environment variables from `.env` file |
| `sass`   | Compiles Sass/SCSS to CSS                    |

#### Development Packages

| Package                | Purpose                                             |
| ---------------------- | --------------------------------------------------- |
| `grunt`                | JavaScript task runner (orchestrates build process) |
| `grunt-contrib-sass`   | Compiles Sass files to CSS                          |
| `grunt-contrib-watch`  | Monitors files for changes and triggers rebuilds    |
| `grunt-concat-css`     | Combines multiple CSS files                         |
| `grunt-contrib-cssmin` | Minifies CSS for production                         |
| `grunt-contrib-copy`   | Copies files between directories                    |
| `grunt-env`            | Manages environment variables for Grunt tasks       |

### VS Code Extensions (Optional)

- **Essential:**
  - [Sass](https://marketplace.visualstudio.com/items?itemName=Syler.sass-indented)
  - [Stylelint](https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint)
- **Quality of Life:**
  - [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
  - [Grunt Tasks](https://marketplace.visualstudio.com/items?itemName=anthonydiamonds.grunt-tasks)

---

## Learning Resources

### Obsidian Theming

- [Official Theme Docs](https://docs.obsidian.md/Themes/App+themes/Build+a+theme)
- [CSS Variables Reference](https://docs.obsidian.md/Themes/App+themes/CSS+variables)

### Reference Themes

- [Primary Theme](https://github.com/primary-theme/obsidian)
- [Minimal Theme](https://github.com/kepano/obsidian-minimal)

---

## Future Plans

- Explore migration to Gulp for build tasks instead of Grunt.
  - Another task runner that uses streams (in-memory file processing) for faster builds.
  - Generally considered more modern and performant, but requires writing more code vs JSON-like configuration.
