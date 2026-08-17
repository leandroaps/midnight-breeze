# Changelog

## Version

### 1.0.0

- Release versions
- released initial package

### 1.0.2

- add themed icon colored

### 1.0.1

- add themed icon colored

### 2.0.0

- add new colors to the theme

### 3.0.0

- add new colors to the theme
- updates some package versions

### 3.0.1

- adjusts the file

### 4.0.0

- adds new icon
- adds missing entries
- adjust package size

### 4.2.0

- updates vsce
- adds new entries
- updates .gitignore

### 4.3.0

- adds GitHub Actions workflow

### 4.4.0

- adds new icon

### 4.4.1

- updates icon

### 4.4.2

- version bump

### 4.4.3

- updates vsce for marketplace compliance

### 4.5.0

- updates the icon

### 4.5.1

- adds missing entries and adjusts some colors

### 4.5.2

- fixes wrong colors

### 4.7.0

- updates dependencies
- enhances theme colors and styles
- fixes build issues

### 5.0.0

#### Semantic highlighting

- enables `semanticHighlighting` and adds a `semanticTokenColors` block (37 entries), which the theme was missing entirely — language servers now drive precise coloring in TypeScript, Python, Rust, C# and others
- covers namespace, class, enum, enumMember, interface, struct, type, typeParameter, parameter, variable, property, decorator, event, function, method, macro, label, comment, string, keyword, number, regexp and operator
- adds modifier support: `readonly` and `defaultLibrary` variants, `selfKeyword`, `newOperator`, literal tokens, plus `*.abstract` and `*.async` in italic and `*.deprecated` struck through

#### Workbench colors (186 new entries)

- editor: `foldBackground`, `linkedEditingBackground`, `symbolHighlightBackground`, word/selection highlight borders, cursor background, primary and secondary multi-cursor, dimmed line numbers, indent guides 2–6 (normal and active)
- debug: adds the full `debugIcon.*` set (breakpoints, start, pause, stop, disconnect, restart, step over/into/out/back) and `debugExceptionWidget.*`, none of which were defined before
- merge editor: adds the complete 3-way `mergeEditor.*` group (changes, base changes, handled and unhandled conflicts in focused and unfocused states, minimap overview), previously absent
- tabs and editor groups: selected tab colors, top borders, hover borders, unfocused inactive background, unfocused modified borders, `editorGroupHeader.noTabsBackground`, `editorPane.background`, `sideBySideEditor.*`, drop-into prompt
- sticky scroll: sidebar, panel and terminal variants plus `editorStickyScroll.border`
- horizontal activity bar (`activityBarTop.*`) and activity error/warning badges
- test coverage: `testing.covered*`, `testing.uncovered*` and `testing.coverCountBadge*`
- terminal: find match, hover highlight, overview ruler and command guide
- also adds `listFilterWidget.*`, `tree.table*`, notification icons, `keybindingTable.*`, settings row states, `radio.*`, `minimapGutter.*`, `chat.*`, comments widget, `ports.iconRunningProcessForeground`, `button.border` and `button.separator`

#### Syntax tokens (22 new rules)

- `invalid.deprecated`, enum members, boolean/null/undefined literals, character constants
- JSDoc support: doc comments, block tags, doc types and variables
- regexp internals: quantifiers, character classes, anchors and groups
- markdown: link underlines, heading and list punctuation, setext headings
- diff headers and ranges
- YAML keys, which previously inherited the red from `entity.name.tag`
- `meta.brace` and `meta.embedded`
