# Ember CSS

**Ember CSS** is a lightweight, warm-toned CSS framework built with Sass. It gives plain HTML elements (headings, text, lists, buttons, forms, inputs and tables) a consistent custom theme, and adds utility classes for color, font size, font weight, margin, padding and borders. Everything is driven by variables, so the whole look can be changed in one place.

Open `index.html` to see every element and utility in action.

---

## Features

- **Themed HTML elements** — no classes needed for `h1`–`h6`, `p`, `a`, `ul`, `ol`, `dl`, `blockquote`, `code`, `pre`, `kbd`, `mark`, `hr`, `button`, `input`, `select`, `textarea`, `fieldset`, `legend` and `table`.
- **Utility classes** — color, background, border color, font size, font weight, text alignment, margin, padding, borders, rounded corners and shadow.
- **Customizable** — Sass variables (with `!default`) at build time, and CSS custom properties (`--em-*`) at runtime.
- **Built with Sass partials** — organized into `abstracts`, `base`, `components` and `utilities`.

## Folder structure

```
Custom-CSS-Framework/
├── dist/
│   ├── ember.css          ← compiled framework (use this)
│   └── ember.min.css      ← minified version
├── scss/
│   ├── ember.scss         ← main file, loads all partials
│   ├── abstracts/
│   │   ├── _variables.scss  ← all customizable Sass variables & maps
│   │   ├── _functions.scss  ← to-rem(), shade(), fade()
│   │   ├── _mixins.scss     ← focus-ring, button-variant, eyebrow
│   │   └── _root.scss       ← turns Sass variables into CSS variables
│   ├── base/
│   │   ├── _reset.scss
│   │   └── _typography.scss ← headings, text, links, lists, quotes, code
│   ├── components/
│   │   ├── _buttons.scss
│   │   ├── _forms.scss
│   │   └── _tables.scss
│   └── utilities/
│       ├── _borders.scss
│       ├── _colors.scss
│       ├── _spacing.scss
│       └── _typography.scss
├── index.html             ← demo page
└── README.md
```

## Sass features used

| Feature | Where |
|---|---|
| Partials & modules (`@use`, `@forward`) | `ember.scss` loads 13 partials from 4 folders |
| Variables with `!default` | `abstracts/_variables.scss` |
| Maps + `@each` loops | color, font size, font weight, spacing and heading utilities |
| `@if` / `@else` control flow | `utilities/_spacing.scss` (skips `p-auto`, handles single vs. double sides) |
| Functions (`@function`) | `to-rem()`, `shade()`, `fade()` in `abstracts/_functions.scss` |
| Mixins (`@mixin` / `@include`) | `focus-ring`, `button-variant`, `eyebrow` in `abstracts/_mixins.scss` |
| Nesting & parent selector `&` | buttons, forms, tables, links, `h1::after` |
| Interpolation `#{}` | generated class names and selectors |
| Built-in modules | `sass:math`, `sass:map`, `sass:string` |

---

## Installation

### Option 1 — Use the compiled CSS (easiest)

1. Download or clone this repository:
   ```bash
   git clone https://github.com/gao00147/Custom-CSS-Framework.git
   ```
2. Copy `dist/ember.css` (or `dist/ember.min.css`) into your project.
3. Link it in the `<head>` of your HTML:
   ```html
   <link rel="stylesheet" href="css/ember.css">
   ```

### Option 2 — Use the Sass source

1. Copy the `scss/` folder into your project.
2. Install Sass (requires Node.js):
   ```bash
   npm install -g sass
   ```
3. Compile:
   ```bash
   sass scss/ember.scss dist/ember.css
   # or watch for changes while you work:
   sass --watch scss/ember.scss:dist/ember.css
   ```
   No Node.js? The **Live Sass Compiler** extension for VS Code works too: open `scss/ember.scss` and click **Watch Sass** in the status bar.

---

## Usage

### Themed elements

Just write normal HTML — it is styled automatically.

```html
<h1>Page title</h1>
<p>Text with a <a href="#">link</a> and <mark>highlight</mark>.</p>

<form>
  <fieldset>
    <legend>Sign up</legend>
    <label for="email">Email</label>
    <input id="email" type="email" placeholder="you@example.com">
    <label class="check"><input type="checkbox"> Remember me</label>
    <button>Submit</button>
  </fieldset>
</form>

<table>
  <thead><tr><th>Name</th><th>Role</th></tr></thead>
  <tbody><tr><td>Alex</td><td>Designer</td></tr></tbody>
</table>
```

### Buttons

`<button>`, `<input type="submit">`, `<input type="reset">` and `<input type="button">` are themed automatically. Use `.btn` to make a link look like a button.

| Class | Result |
|---|---|
| `.btn-secondary` `.btn-accent` `.btn-success` `.btn-warning` `.btn-danger` `.btn-dark` | Color variants |
| `.btn-outline` | Outline style (combine with a color: `.btn-danger .btn-outline`) |
| `.btn-sm` / `.btn-lg` | Small / large size |

```html
<button class="btn-secondary btn-outline btn-lg">Learn more</button>
<a href="#" class="btn btn-success">Link button</a>
```

### Forms

| Class | Result |
|---|---|
| `label.check` | Inline label for a checkbox or radio |
| `.is-valid` / `.is-invalid` | Green / red border on an input |
| `.table-sm` | Compact table (on `<table>`) |

### Utility classes

**Colors** — available names: `primary`, `secondary`, `accent`, `success`, `warning`, `danger`, `light`, `dark`, `white`, `muted`

| Pattern | Example | Property |
|---|---|---|
| `.text-{color}` | `.text-primary` | text color |
| `.bg-{color}` | `.bg-secondary` | background color |
| `.border-{color}` | `.border-danger` | border color |

**Typography**

| Pattern | Values |
|---|---|
| `.fs-{size}` | `xs` 0.75rem · `sm` 0.875rem · `md` 1rem · `lg` 1.25rem · `xl` 1.5rem · `2xl` 2rem · `3xl` 2.75rem |
| `.fw-{weight}` | `light` 300 · `normal` 400 · `medium` 500 · `semibold` 600 · `bold` 700 |
| `.text-{align}` | `left` · `center` · `right` |
| Others | `.text-uppercase` · `.text-italic` · `.font-heading` · `.font-mono` |

**Spacing** — `{property}{side}-{size}`

- Property: `m` = margin, `p` = padding
- Side: *(none)* all sides · `t` top · `b` bottom · `s` left · `e` right · `x` left & right · `y` top & bottom
- Size: `0` 0 · `1` 0.25rem · `2` 0.5rem · `3` 1rem · `4` 1.5rem · `5` 3rem · `auto` (margin only)

```html
<div class="mt-4 px-3">...</div>   <!-- margin-top 1.5rem, padding left/right 1rem -->
<div class="mx-auto p-5">...</div> <!-- centered, padding 3rem -->
```

**Borders**

| Class | Result |
|---|---|
| `.border` | 1px border on all sides |
| `.border-top` `.border-bottom` `.border-left` `.border-right` | Border on one side |
| `.border-0` `.border-2` `.border-4` | Remove border / 2px / 4px width |
| `.rounded-0` `.rounded` `.rounded-lg` `.rounded-pill` | Corner radius |
| `.shadow` | Soft drop shadow |

```html
<div class="border border-2 border-primary rounded-lg p-3 shadow">Card</div>
```

---

## Customization

### 1. With CSS variables (no compiling needed)

Every theme value is exposed as a CSS custom property. Override them in your own stylesheet, loaded **after** Ember CSS:

```css
:root {
  --em-primary: #0b7285;      /* teal instead of orange */
  --em-secondary: #2b2d42;
  --em-radius: 0;             /* square corners everywhere */
  --em-font-heading: "Poppins", sans-serif;
}
```

Hover colors, focus rings and table stripes are calculated from these variables, so they update automatically.

| Variable | Default | Controls |
|---|---|---|
| `--em-primary` … `--em-muted` | see `_variables.scss` | Theme colors |
| `--em-border-color` | `#e7e1db` | Borders of inputs, tables, `.border` |
| `--em-font-base` | system font stack | Body text |
| `--em-font-heading` | Georgia, serif | Headings, legends, blockquotes |
| `--em-font-mono` | monospace stack | `code`, `pre`, `kbd` |
| `--em-font-size` / `--em-line-height` | `1rem` / `1.6` | Body text size and spacing |
| `--em-spacer` | `1rem` | Base spacing between elements |
| `--em-radius` | `0.5rem` | Corner radius |
| `--em-transition` | `0.2s ease` | Hover/focus animation speed |

### 2. With Sass variables (recompile)

Edit the values in `scss/abstracts/_variables.scss` and recompile, **or** configure them from your own Sass file without touching the framework:

```scss
@use "path/to/scss/ember" with (
  $color-primary: #0b7285,
  $border-radius: 0,
  $spacer: 1.25rem
);
```

Sass maps generate the utility classes, so adding a color to `$theme-colors` automatically creates `.text-{name}`, `.bg-{name}` and `.border-{name}`:

```scss
@use "path/to/scss/ember" with (
  $theme-colors: ("primary": #0b7285, "brand": #ff006e, "dark": #111111)
);
```

> Note: when you replace `$theme-colors`, list every color you still want classes for.

---

## Browser support

Works in all current versions of Chrome, Edge, Firefox and Safari. Hover shades use `color-mix()` (supported since 2023).

## License

MIT — free to use and modify.
