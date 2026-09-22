# Git blame

[Git blame doc](https://git-scm.com/docs/git-blame)

[Git blame bitbucket tutorial](https://www.atlassian.com/git/tutorials/inspecting-a-repository/git-blame)

## Show revision and author last modified each line of a file

```bash
git blame README.md
```

## Git blame show from line 1 to line 5

```bash
git blame -L 1,5 README.md
```

## Show email instead of username

```bash
git blame -e README.md
```

## Ignore whitespace changes

```bash
git blame -w README.md
```

## Detects moved or copied lines within the same file

```bash
git blame -M README.md
```

## Detects lines that were moved or copied from other files

```bash
git blame -C README.md
```
