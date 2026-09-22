# Git log

## Show complete repo commit history

```bash
git log
```

## Show last N commits history

```bash
git log -N
git log -3
```

## Show author commits

```bash
git log --author=<author_name>
```

## Show commits before date

```bash
git log --before "2023-05-12"
```

## Show commits after date

```bash
git log --after "2023-05-13"
```

## Show commit modifications history

```bash
git log -p
```

## Show commit short stat modifications

```bash
git log --stat
```

## Show commits each in one line

```bash
git log --oneline
```

## Present commit history in ASCII graph mode

```bash
git log --graph
```

## Search phrase in commit messages

```bash
git log --grep="YOUR_PHRASE"
```

## Search commits connected with file

```bash
git log -- PATH_TO_YOUR_FILE
```
