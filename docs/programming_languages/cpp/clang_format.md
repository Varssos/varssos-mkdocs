# Clang format

## Setup clang format in VS code

[Windows](https://www.youtube.com/watch?v=xxuaOG0WjIE)

**On Linux:**

[Tutorial how to set it on Linux](https://eellaup.medium.com/how-to-set-up-clang-format-in-visual-studio-code-in-a-vagrant-environment-georgiatech-gios-1935ed73efd1)

1. Check available clang-format versions

```bash
sudo apt-cache search clang-format
```

2. Install last version e.g

```bash
sudo apt-get install clang-format-12
```

3. Check location of installed clang-format bin

```bash
whereis clang-format-12
# Output: /user/bin/clang-format-9
# You should put it in clang-format VS code extension config
```

4. Install the clang-format VS code extension
5. Edit extension setting in JSON format and add this on the bottom

```json
"editor.codeActionsOnSave": {
    "source.fixAll": true
},
"editor.formatOnSave": true,
"clang-format.executable": "/usr/bin/clang-format-12",
"clang-format.style": "file",
"clang-format.language.c.enable": true,
"[c]": {
    "editor.defaultFormatter": "xaver.clang-format",
    "editor.wordBasedSuggestions": false,
    "editor.suggest.insertMode": "replace",
    "editor.semanticHighlighting.enabled": true
},
"clang-format.language.cpp.enable": true,
"[cpp]": {
    "editor.defaultFormatter": "xaver.clang-format",
    "editor.wordBasedSuggestions": false,
    "editor.suggest.insertMode": "replace",
    "editor.semanticHighlighting.enabled": true
}
```

6. Download [.clang-format](./clang-format-example) and put it in the project path (rename the downloaded file to `.clang-format`)
