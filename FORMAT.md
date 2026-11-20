# Icon Themes

Each `*.json` file in this folder is an icon set you can pick in **Settings → Appearance → Icon Set**. A theme that needs its own images can also live in a subfolder as `<folder>/theme.json`. After adding or editing a file, press the reload button next to the picker.

Files that ship with Clairvoyance (this README, `monoline.json`, `colored-paper.json`, `porcelain.json`, and `fluent.json`) are overwritten on every launch. Give your theme its own file name; copying `monoline.json` to a new name is a good place to start.

## Format

```json
{
  "id": "my-icons",
  "name": "My Icons",
  "description": "Optional.",
  "author": "Optional.",
  "icons": {
    "folder":   { "lucide": "folder-code", "color": "#e8a838" },
    "markdown": { "color": "var(--accent)" },
    "code":     { "image": "my-icons/code.png" },
    "pdf":      { "svg": "<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24'>...</svg>" }
  },
  "extensions": {
    ".sln": { "lucide": "layers", "color": "#a855f7" },
    ".cmake": "code"
  },
  "fileNames": {
    "cmakelists.txt": "code"
  }
}
```

- `id`: letters, digits, `.`, `_`, `-` (up to 64). `linework` is reserved for the built-in set.
- Leave out any slot and it falls back to **Linework**, the built-in set. A spec with only `color` recolors the inherited glyph.

### Slots

`folder`, `folderOpen`, `file`, `markdown`, `code`, `data`, `record`, `image`, `audio`, `video`, `pdf`, `office`, `archive`, `canvas`, `base`, `binder`, `hierarchy`, `link`, `url`, `report`, `exhibit`, `todo`, `todoStaff`.

Todo status marks, drawn before each todo in the todo and sprint lists: `statusTodo`, `statusInProgress`, `statusBlocked`, `statusReadyForReview`, `statusReviewed`, `statusDone`, `statusWontFix`, `statusCanceled`, `statusWorkingAsDesigned`. Give each its own shape, and keep the status colors every bundled set uses so a status looks the same in any set: todo, won't fix, and canceled `#8b949e`; in progress `#d29922`; blocked `#f85149`; ready for review `#58a6ff`; reviewed `#2dd4bf`; done `#3fb950`; working as designed `#a371f7`. A status you leave out uses Linework's, not your `todo` icon.

`folderOpen` falls back to your `folder`; `office`, `archive`, and `canvas` to your `file`; `binder` and `hierarchy` to your `base`; `url` to your `link`; `record` (Binder records) to your `data`; `report` and `todo` to your `markdown`; `exhibit` to your `code`; `todoStaff` (Staff-created todos) to your `todo`.

### Glyphs

Use one of these per icon:

- `lucide`: a kebab-case Lucide name from the curated set (`file`, `file-code`, `file-json`, `folder-git`, `layers`, `terminal`, `package`, ...). An unknown name shows the generic file glyph.
- `svg`: inline `<svg>` markup, up to 64 KB.
- `image`: a `.png`, `.jpg`, `.gif`, `.webp`, or `.svg` path relative to the theme file, up to 256 KB, and inside this folder.

Any glyph spec may add a `small` variant, drawn at 20px and below (tree rows, tabs), for art that needs a separate pixel-hinted version: `{ "svg": "<svg ...48px art...>", "small": { "svg": "<svg ...16px art...>" } }`. `colored-paper.json` and `porcelain.json` use this for every icon.

`color` takes any CSS color, including theme variables such as `var(--accent)`. It only applies to `lucide` glyphs; `svg` and `image` icons keep their own colors.

### Overrides

`extensions` keys are lowercase with a leading dot. The longest match wins, so `.vcxproj.filters` beats `.filters`. `fileNames` keys are exact lowercase names and win over extensions. A value is a slot name (`"code"`) or a glyph spec.
