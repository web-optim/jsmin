<h1 align="center">
  <img src="./images/jsmin_logo.png" alt="jsmin logo" align="center" />
  <br />
  <b align="center">Jsmin</b>
</h1>
<p align="center">
  <b align="center"><a href="README.md">Readme</a></b> |
  <b><a href="https://github.com/web-optim/jsmin">GitHub</a></b> | <br /><br />
  <a href="#">
    <img
      alt="GitHub code size in bytes"
      src="https://img.shields.io/github/languages/code-size/web-optim/jsmin?style=flat-square"
    />
  </a>
  <a href=""
    ><img
      alt="Maintenance"
      src="https://img.shields.io/maintenance/yes/2026?style=flat-square"
    />
  </a>
  <a href="https://www.codefactor.io/repository/github/web-optim/jsmin">
    <img
      alt="CodeFactor"
      src="https://www.codefactor.io/repository/github/web-optim/jsmin/badge"
    />
  </a>
  <a href="https://gitpod.io/#https://github.com/web-optim/jsmin">
    <img
      alt="Gitpod"
      src="https://img.shields.io/badge/Gitpod-Ready--to--Code-blue?logo=gitpod"
    />
  </a>
  <br />
  <br />
  <i>
    An extremely fast JavaScript minifier (pronounced as jasmine or jazz-min
    /jăz′mĭn/.) written in Rust.
  </i>
</p>
<details>
  <summary><b>Table of Contents</b></summary>
  <p>

- **Getting Started**
  - [🚀 Features](#features-)
  - [🛠️ Usage](#usage-)
- **Overview**
  - [🎨 Goals](#goals-)
  - [📊 Performance](#performance-)
  - [🧪 In Progress](#in-progress-)
- **Community**
  - [📣 More Contributors Wanted](#more-contributors-wanted-)
  - [💖 Supporting Jsmin](#supporting-jsmin-)
  - [🛣️ Roadmap](#roadmap-%EF%B8%8F)
  - [🙋 Contributing](#contributing-)
  - [📜 License](#license-)
  - [🤝 Credits](#credits-)

  </p>
</details>

# Goals 🧢

- Fully written in Rust for maximum compatibility with Rust programs and derivatives (FFI, WASM, embedded, etc.).
- Maximises performance on a single CPU core for simple efficient scaling and easy compatible integration.
- Minification of individual inputs/files only; no bundling or transforming.
- Prefer minimal complexity and faster performance over maximum configurability and minimal extra compression.

**[⬆️ Back to Top](#--)**

# Performance 📊

Comparison with esbuild, run on [common libraries](./bench).

> Work in progress! 🙂.

**[⬆️ Back to Top](#--)**

# Features 🚀

- 🚀 Fast parsing powered by SIMD instructions and lookup tables.
- 🚂 Data is backed by a fast reusable bump allocation arena.
-  Supports JSX.
- 🎚️ Analyses scopes and variable visibilities.
- 🔍 Minifies identifiers.
- ⏭️ Omits semicolons, spaces, parentheses, and braces where possible.
- ⚗️ Transforms functions to arrow functions when `new`, `this`, `arguments`, and `prototype` aren't used.
- 🧮 Transforms `if` statements to expressions.

**[⬆️ Back to Top](#--)**

# Usage 🛠️

## Rust

Add the dependency:

```toml
[dependencies]
jsmin = "0.6"
```

Call the method:

```rust
use jsmin::{Session, TopLevelMode, minify};

let mut code: &[u8] = b"const main = () => { let my_first_variable = 1; };";
let session = Session::new();
let mut out = Vec::new();
minify(&session, TopLevelMode::Global, code, &mut out).unwrap();
assert_eq!(out.as_slice(), b"const main=()=>{let a=1}");
```

## Node.js

Install the dependency:

```bash
npm i @jsmin/node
```

Call the method:

```typescript
import {minify} from "@jsmin/node";

const src = Buffer.from("let x = 1;", "utf-8");
const min = minify(src);
```
**[⬆️ Back to Top](#--)**

# In Progress 🧪

- Combine and reorder declarations.
- Evaluation and folding of constant expressions.
- Parse and erase TypeScript syntax.
- Removal of unreachable, unused, and redundant code.
- Inlining single-use declarations.
- Replacing if statements with conditional and logical expressions.
- Returning an explicit error on illegal code e.g. multiple declarations/exports with identical names.
- Much more inline, high level, and usage documentation.
- Support import and export string names e.g. `import { "a-b" as "c-d" } from "x"`.
- Simplify pattern parsing and minification.
- Micro-optimisations:
  - Unwrap string literal computed members, then identifier or number string members.
  - Replace `x === null || x === undefined` with `x == null`, where `x` is side-effect free.
  - Replace `typeof x === "undefined"` with `x === undefined`.
  - Using shorthand properties.
  - Replace `void x` with `x, undefined`.
  - Replace `return undefined` with `return`.
  - Replace `const` with `let`.
  - Hoist `let` and `const`.
  - Unwrapping blocks.
  - Unwrapping paretheses, altering expressions as necessary.
  - `if (...) return a; else if (...) return b; else return c` => `return (...) ? a : (...) ? b : c`.

**[⬆️ Back to Top](#--)**

# More Contributors Wanted 📣

We are looking for more willing contributors to help grow this project. For more information on how you can contribute, check out the [project board](https://github.com/neon-mmd/web-optim/jsmin?query=is%3Aopen) and the [CONTRIBUTING.md](CONTRIBUTING.md) file for guidelines and rules for making contributions.

**[⬆️ Back to Top](#--)**

# Supporting Jsmin 💖

> For full details and other ways you can help out, see: [**Contributing**](CONTRIBUTING.md)

If you use Jsmin and would like to contribute to its development, we're glad to have you on board! Contributions of any size or type are always welcome, and we will always acknowledge your efforts.

Several areas that we need a bit of help with at the moment are:

- **Completing the In-Progress listings:** Help by completing some of the things from the [in-progress](#in-progress-) listing. 
- Submit a PR to add a new feature, fix a bug, update the docs, add a theme, widget, or anything else.
- Star Jsmin on GitHub.

**[⬆️ Back to Top](#--)**

# Roadmap 🛣️

> Coming soon! 🙂.

**[⬆️ Back to Top](#--)**

# Contributing 🙋

Contributions are welcome from anyone. It doesn't matter who you are; you can still contribute to the project in your own way.

## Not a developer but still want to contribute?

Check out this [video](https://youtu.be/FccdqCucVSI) by Mr. Nick on how to contribute.

## Developer

If you are a developer, have a look at the [CONTRIBUTING.md](CONTRIBUTING.md) document for more information.

**[⬆️ Back to Top](#--)**

# License 📜

Jsmin is licensed under the [APACHEv2](LICENSE) license.

**[⬆️ Back to Top](#--)**

# Credits 🤝

We would like to thank the following people for their contributions and support:

**Contributors**

<p>
  <br />
  <a href="https://github.com/web-optim/jsmin/graphs/contributors">
    <img src="https://contrib.rocks/image?repo=web-optim/jsmin" />
  </a>
  <br />
</p>

**Stargazers**

<p>
  <a href="https://github.com/web-optim/jsmin/stargazers">
    <img src="http://reporoster.com/stars/dark/web-optim/jsmin"/>
  </a>
</p>

**[⬆️ Back to Top](#--)**

---

<p align="center">
  <a href="https://github.com/web-optim/jsmin">
    <img src="https://github.githubassets.com/images/icons/emoji/octocat.png" />
  </a>
  <br /><br />
  <i>Thank you for Visiting</i>
</p>
