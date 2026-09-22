# Git reset/revert, undo changes/files

## Create commit which reverts our changes in commit `<commit_id>`

```bash
git revert <commit_id>
```

## Reset commit, stay with unstaged modifications

Reset to state in `<commit_id>`, commits ahead of that commit will be erased from history and modification will not be staged

```bash
git reset <commit_id>
```

## Reset commits, stay with staged modifications

Reset to state in `<commit_id>`, commits ahead of that commit will be erased from history and modification will be staged

```bash
git reset --soft <commit_id>
```

## Erase commits before and on that `<commit_id>`

```bash
git reset --hard <commit_id>
```

## Unstage file

```bash
git reset -- <file>
```

## Erase local file modification

```bash
git checkout -- <file>
# Or
git checkout origin/master -- <file>
```

## Unstage file and erase local modification

```bash
git reset -- <file>
git checkout -- <file>
```
