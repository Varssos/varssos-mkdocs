# Git stash

## Add current changes to stash

```bash
git stash
```

## Show stash list

```bash
git stash list
```

!!! important
    Stash with index 0 is the newest one!

## Show which files were modified in stash@{0}

```bash
git stash show stash@{0}
```

## Show what was modified in stash@{0}

```bash
git stash show stash@{0} -p
```

## Stash with description

```bash
git stash save "Modified x, and added y"
```

## Apply the newest stash from stash list

```bash
git stash apply
```

!!! important
    Keep in mind that it will be still in stash list

## Apply the newest stash from stash list and erase from list

```bash
git stash pop
```

## Pop stash with index 2

```bash
git stash pop stash@{2}
```

## Stash untracked files

```bash
git stash -u
```

## Remove element from stash list

```bash
git stash drop stash@{0}
```

## Remove all elements from stash list

```bash
git stash clear
```
