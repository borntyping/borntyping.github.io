---
title: Merging a subdirectory of a git repository, revisited
category: Development
layout: post
---

My previous post on the topic used git's builtin `filter-branch` subcommand, which has been superseded by the [git-filter-repo](https://github.com/newren/git-filter-repo) project.

In the repository being merged, we create a branch named `filtered` that only contains the contents of the `src/` directory, moved to `src/other/` - the branch no longer contains files that were outside the `src/` directory.

```bash
git switch -c filtered
git-filter-repo --path src/ --path-rename src/:src/other/
```

In the repository the subdirectory is being merged into:

```bash
git remote add other ../other-repository/
git fetch other
git merge -s ours --no-commit --allow-unrelated-histories other/filtered
git read-tree -mu other/filtered
git commit
```
