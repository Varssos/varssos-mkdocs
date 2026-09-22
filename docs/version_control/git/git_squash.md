# Git squash

## Squash child commits to one above the `parent_commit_id`

All the commits above the `<parent_commit_id>` can be coupled into one

```bash
git rebase -i <parent_commit_id>
```

## Squash N commits from top

```bash
git rebase -i HEAD~N
```

## Squash commits from branch `squash-merge-branch` to `master`

```bash
git checkout master
git merge --squash <branch_to_squash>
```
