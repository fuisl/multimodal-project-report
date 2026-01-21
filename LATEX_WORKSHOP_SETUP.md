# LaTeX Workshop Live Rendering Setup Guide

## Overview
This project is now optimized for live PDF rendering using VS Code's LaTeX Workshop extension with continuous compilation.

## Prerequisites
- VS Code with [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) extension installed
- TeX Live 2024+ installed (includes lualatex)
- latexmk installed

## Optimization Features

### 1. **Primary Build Recipe**
- **Recipe**: `latexmk (lualatex) 🔃 [RECOMMENDED]`
- **Benefits**:
  - Single-command compilation (latexmk handles all steps automatically)
  - Intelligent recompilation (only reruns when needed)
  - Much faster than manual step-by-step recipes
  - Ideal for live rendering with fast feedback loops

### 2. **Enhanced .latexmkrc Configuration**
The `.latexmkrc` file has been optimized with:

- **LuaLaTeX Engine**: Uses `lualatex` with `--shell-escape` for advanced features (minted, tikz, etc.)
- **SyncTeX Support**: Enabled (`--synctex=1`) for accurate PDF↔editor synchronization
- **Fast Rebuilds**: Configured to minimize recompilation time during edits
- **Continuous Mode Ready**: Fully supports LaTeX Workshop's continuous compilation

### 3. **VS Code Settings Optimizations**
Updated `vscode.settings.json` with:

- **Auto-build on Save**: `autoBuild.run: "onSave"` - compiles automatically when you save
- **Build Interval**: `autoBuild.interval: 1000` - waits 1 second after last edit before building (prevents excessive recompiles)
- **PDF Viewer**: Opens PDF in a tab within VS Code for seamless editing
- **Tools Updated**: 
  - `latexmk` now includes proper flags: `-lualatex`, `-synctex=1`, `-interaction=nonstopmode`
  - `lualatex` tool adds `-shell-escape` for minted support

## Usage

### Live Rendering (Default)
1. Open `paper.tex` in VS Code
2. The project automatically builds on save
3. View the PDF in the PDF viewer tab
4. Edit and save to see changes instantly

### Manual Builds
- Click the green play button in the LaTeX Workshop sidebar to run the default recipe
- Use command palette (`Ctrl+Shift+P`): `LaTeX Workshop: Build LaTeX`

### Alternative Recipes
If needed, you can switch recipes:
- `LaTeX Workshop: Change Default Builder` - select from 3 available recipes
- Or manually select from the VS Code status bar

## Performance Tips

1. **Disable Auto-build During Research**: If you're doing heavy reading/research, temporarily disable auto-build to reduce CPU usage
2. **Use SyncTeX**: Ctrl+Click on PDF to jump to source code (or vice versa with Cmd+Click on Mac)
3. **Watch File Size**: Monitor `paper.pdf` size in the PDF viewer tab; if it gets large, consider splitting into multiple files

## Advanced Configuration

### Enable Minted Syntax Highlighting
Minted is already supported via `--shell-escape`. Just use:
```latex
\usepackage{minted}
\begin{minted}{python}
# Your code here
\end{minted}
```

### Using Glossaries
Glossary support is pre-configured in `.latexmkrc`. Define glossaries as usual:
```latex
\usepackage{glossaries}
\makeglossaries
```

## Troubleshooting

### "latexmk: Could not find file `.latexmkrc`"
- Ensure the `.latexmkrc` file exists in the project root
- Some systems require `_latexmkrc` to be renamed to `.latexmkrc`

### PDF Not Updating
1. Check the LaTeX Workshop output panel for compilation errors
2. Verify the recipe is set to "latexmk (lualatex) 🔃 [RECOMMENDED]"
3. Try manually building with the play button

### Slow Compilation
1. Check if you have many large images
2. Consider moving complex tikz figures to separate files
3. Temporarily disable auto-build: Set `autoBuild.run: "never"` and build manually

## Files Modified

- `vscode.settings.json` - Updated VS Code LaTeX Workshop configuration
- `.latexmkrc` - New optimized latexmk configuration (replaces `_latexmkrc`)
- `paper.tex` - No changes (magic comments already in place)

## Related Documentation

- [LaTeX Workshop Documentation](https://github.com/James-Yu/LaTeX-Workshop)
- [latexmk Documentation](http://www.ctan.org/pkg/latexmk)
- [LuaLaTeX Documentation](http://www.luatex.org/)
