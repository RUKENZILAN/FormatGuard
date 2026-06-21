# FormatGuard
<img width="1165" height="880" alt="FormatGuard2" src="https://github.com/user-attachments/assets/704d1da1-e597-4149-b71a-cebdfc894710" />
<img width="1217" height="790" alt="FormatGuard1" src="https://github.com/user-attachments/assets/f8743102-0d9d-43f7-a954-4357df215ff0" />

A lightweight, single-file JSON ⇄ YAML converter with a built-in security validation layer. No build step, no server, no dependencies beyond one CDN script — open the HTML file in a browser and it works.
Features
**Conversion**

JSON → YAML and YAML → JSON, switchable via toggle pills or a one-click swap button
Auto-convert as you type — output updates automatically (debounced), no "convert" button required
Copy to clipboard and download the converted result as a `.json` or `.yaml` file
Load sample button to quickly see the tool in action
Live character counters for both input and output

**Security layer**
Every conversion is passed through a visible, real-time scan log before output is rendered:

Check	What it catches
Size cap	Blocks input over 1,000,000 characters before parsing
JSON-only YAML schema	Parses YAML with `JSON_SCHEMA`, rejecting custom/executable tags (e.g. `!!js/function`) — the class of bug behind classic YAML deserialization exploits
Structural depth limit	Blocks excessively nested objects/arrays (max 50 levels)
Node count limit	Blocks oversized structures (max 20,000 nodes)
Prototype-pollution guard	Detects and strips dangerous keys (`__proto__`, `constructor`, `prototype`) rather than passing them through
Expansion-ratio check	Compares output size to input size to catch YAML "billion laughs" anchor/alias bombs
Each check shows a pass (green), warning (amber), or block (red) status with details, and an overall status pill (`secure` / `sanitized` / `blocked`) summarizes the result.
Privacy & safety by design
Runs entirely client-side — nothing is sent to a server
Output is written using `textContent`, never `innerHTML`, so converted content can never execute as markup (XSS-safe rendering)

**Theming**

Toggle between a dark theme and a white-background / black-text theme via the button in the header
All colors (backgrounds, borders, text, accents) switch together for consistent contrast in both modes

**Usage**

Open `formatguard.html` in any modern browser
Choose a direction: `JSON → YAML` or `YAML → JSON`
Paste or type your data into the input panel
Watch the output and security scan log update automatically
Copy or download the result
Limits (configurable in code)
```js
MAX_CHARS: 1,000,000        // max input size
MAX_DEPTH: 50                // max nesting depth
MAX_NODES: 20,000            // max total object/array nodes
MAX_EXPANSION_RATIO: 50      // max output_len / input_len
```

These are defined near the top of the `<script>` block in `formatguard.html` and can be adjusted as needed.

**Tech**

Vanilla HTML/CSS/JS — no framework, no build tools
js-yaml (loaded via CDN) for YAML parsing/serialization
Single file, ~ self-contained, easy to host anywhere (or just open locally)
