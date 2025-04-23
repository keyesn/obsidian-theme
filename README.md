# Obsidian Theme Development Guide

A personal project to learn CSS/styling by building a custom Obsidian theme.
**Focus**: Experimentation with Sass, Grunt automation, and Obsidian theming concepts.

---

## Table of Contents

One of the VSCode extensions is screwing with this and I can't stand the warnings.

---

## Usage Instructions

### Workflow for Auto Updates

1. **Start the Watcher**:

  ```bash
  npx grunt
  ```

> [!note]
> Starts the default task that watches for changes.

### Debugging Tips

- If changes aren't appearing, check your `.env` file path.
- Directly examin `theme.css` in your project root to confirm changes are processed.
- If something breaks, check the unminified CSS at `src/css/main.css` for debugging.

---

## Project Structure

```plaintext
src/
├── css/                  # CSS files
│   ├── main.css          # Main CSS file (unminified)
│   └── theme.css         # Minified CSS file (for Obsidian)
├── scss/                 # Sass files
│   ├── _variables.scss   # Sass variables
│   ├── _mixins.scss      # Sass mixins
│   ├── _base.scss        # Base styles
│   ├── _components.scss  # Component styles

```

### SCSS Folder (`src/scss/`)

- Contains source files you edit.
- The main `index.scss` imports other SCSS partials.

### CSS Folder (`src/css/`)

- Serves as an output and storage location
- Contains CSS files that aren't compiled from SCSS:
  - `style-settings.css` : Contains Theme settings plugin configurations.
  - Font files in `fonts/` folder - Custom font definitions

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

> [!note]
> Path should be relative to your home directory (which is added automatically by the Gruntfile).

---

## Development Workflow

### High-Level Steps

1. Sass files are compiled to CSS using the `grunt-contrib-sass` plugin.
2. CSS files might be concatenated into one file using `grunt-concat-css`.
3. The resulting CSS is minified with `grunt-contrib-cssmin` for production.
4. Files are copied to their final destinations with `grunt-contrib-copy`.
5. During development, the `grunt-contrib-watch` plugin monitors file changes and triggers rebuilds.
6. Environment variables are managed through `dotenv` and `grunt-env`.

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

## Review

### Grunt Alternatives

- **Gulp**: A streaming build system that uses code over configuration.
  - More control and flexibility, but requires more setup.
  - Uses streams for faster builds (in-memory file processing).
- **Webpack**: A module bundler that can handle complex build processes.
  - More complex and powerful, but overkill for simple tasks.
  - Can be used for both development and production builds.
- **Rollup**: A module bundler for JavaScript libraries.
  - Focuses on ES modules and tree-shaking for smaller bundles.
  - More suited for library development than theming.
- **Vite**: A modern build tool that uses native ES modules.
  - Fast development server and optimized builds.
  - Great for modern JavaScript projects, but may require more setup for CSS.
- **esbuild**: A fast JavaScript bundler and minifier.
  - Focuses on speed and simplicity.
  - Can be used for CSS, but primarily designed for JavaScript.

---

## Future Plans

- Explore migration to Gulp for build tasks instead of Grunt.
  - Another task runner that uses streams (in-memory file processing) for faster builds.
  - Generally considered more modern and performant, but requires writing more code vs JSON-like configuration.
