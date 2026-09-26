# rg

`rg` (ripgrep) is a line-oriented search tool that recursively searches the current directory for a regex pattern — like `grep`, but faster and with saner defaults.

## Why use ripgrep?

- Ignores files listed in `.gitignore`/`.ignore` by default, so it won't waste time searching `node_modules`, build output, etc.
- Can limit a search to specific file types, e.g. `rg -tpy foo` searches only Python files.
- Generally faster than `grep`/`ack`/`ag`, with Unicode support out of the box.

## Installation

[rg installation guide](https://github.com/burntsushi/ripgrep#installation)

```bash
sudo apt-get update
sudo apt-get install ripgrep
```

## Basic usage

[ripgrep GUIDE](https://github.com/BurntSushi/ripgrep/blob/master/GUIDE.md)

```bash
rg fast README.md
rg 'fast\w+' README.md
rg 'fn write\('
```

## Common flags

| Flag | Meaning |
|---|---|
| `-i` | case-insensitive search |
| `-w` | match whole words only |
| `-v` | invert match (show non-matching lines) |
| `-F` | treat the pattern as a literal string, not a regex |
| `-n` / `-N` | show/hide line numbers (shown by default when output is a terminal) |
| `-c` | only print the count of matching lines per file |
| `-l` | only print file names that contain a match |
| `-A N` / `-B N` / `-C N` | show N lines of context after/before/around each match |

## Ignoring files

All of ripgrep's default filtering can be toggled with flags:

- `--no-ignore` — disable all `.gitignore`/`.ignore`-based filtering.
- `--hidden` (`-.` for short) — also search hidden files and directories.
- `--text` (`-a` for short) — also search binary files. Be careful: binary files may emit control characters to your terminal and cause strange behavior.
- `--follow` (`-L` for short) — follow symlinks.

## Manual filtering

Filter by extension:
```bash
rg 'fn run' -g '*.rs'
```

Or use a predefined file type instead of a glob (`-t` takes the type name as its argument; it can also be written attached, e.g. `-trust`):
```bash
rg 'fn run' -t rust
```

Exclude a file type with `--type-not` (or its short form `-T`, also `-Trust`):
```bash
rg TODO --type-not rust
```

## Replacements

`-r`/`--replace` only changes what's shown in the search **output** — it does not modify the files on disk:
```bash
rg fast README.md -r FAST
```

To actually edit files in place, pipe matching file names into `sed`:
```bash
rg fast -l | xargs sed -i 's/fast/FAST/g'
```

## Combining with fzf

For an interactive "live grep" with a preview pane, see the [fzf notes](fzf.md#useful-one-liners).
