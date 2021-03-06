[![Latest version](https://img.shields.io/github/v/release/Nixinova/Linguist?label=latest%20version&style=flat-square)](https://github.com/Nixinova/Linguist/releases)
[![Last updated](https://img.shields.io/github/release-date/Nixinova/Linguist?label=updated&style=flat-square)](https://github.com/Nixinova/Linguist/releases)
[![npm downloads](https://img.shields.io/npm/dt/linguist-js?logo=npm)](https://www.npmjs.com/package/linguist-js)

# Linguist

Analyses all files located in a given folder and collates the results.
Powered by [github-linguist](https://github.com/github/linguist), although it doesn't need to be installed.

## Install

Linguist is available [on npm](https://npmjs.com/package/linguist-js) as `linguist-js`.

Install locally using `npm install linguist-js` and import it into your code like so:

```js
const linguist = require('linguist-js');
```

Or install globally using `npm install -g linguist-js` and run using the CLI command `linguist`.

```
linguist --help
```

## Usage

Linguist contains one function which analyses a given folder.

As an example, take the following file structure:

```
.
| src
| | cli.js 1kB
| | index.ts 2kB
| readme.md 3kB
```

Running Linguist on this folder will return the following JSON:

```json
{
	"count": 3,
	"results": {
		"src/index.ts": "TypeScript",
		"src/cli.js": "JavaScript",
		"readme.md": "Markdown"
	},
	"languages": {
		"programming": { "JavaScript": 1000, "TypeScript": 2000 },
		"markup": {},
		"data": {},
		"prose": { "Markdown": 3000 }
	}
}
```

## API

### Node

```js
const linguist = require('linguist-js');
let folder = './src';
let options = { keepVendored: false, quick: false };
let { count, results, languages } = linguist(folder, options);
```

- `linguist(folder?, opts?)` (default export):
  Analyse the language of all files found in a folder.
  - `folder` (optional; string):
    The folder(s) to analyse (defaults to `./`).
    Analyse multiple folders using the syntax `"{folder1,folder2,...}"`.
  - `opts` (optional; object):
    An object containing analyser options.
    - `keepVendored` (boolean):
      Whether to keep vendored files (dependencies, etc) (defaults to `false`).
    - `quick` (boolean):
      Whether to skip the checking of gitattributes files for manual language classifications (defaults to `false`).

### Command-line

```
linguist --analyze [<folder>] [--files] [--vendored] [--quick]
linguist --help
```

- `--analyze`:
  Analyse the language of all files found in a folder.
  - `<folder>` (optional):
    The folder to analyse (defaults to `./`).
    Analyse multiple folders using the syntax `"{folder1,folder2,...}"`.
  - `--files` (optional):
    Whether to print a full list of all files analysed.
  - `--vendored` (optional):
    Whether to include vendored files (dependencies, etc).
  - `--quick` (optional):
    Whether to skip the checking of gitattributes files for manual language classifications.
- `--help`:
  Display a help message.
- `--version`:
  Display the current version of linguist-js.
