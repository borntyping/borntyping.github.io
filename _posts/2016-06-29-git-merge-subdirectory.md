---
layout: post
title: Merging a subdirectory of a separate Git repository
---

In the repository being merged:

```bash
git checkout -b temp
git filter-branch --prune-empty --subdirectory-filter <subdirectory>/ temp
```

In the repository the subdirectory is being merged into:

```bash
git remote add other ../<other-repository>
git fetch other
git merge -s ours --no-commit --allow-unrelated-histories other/temp
git read-tree --prefix=<path> -u other/temp
git commit
```

Done!

The output of the merge should look something like this:

```
$ cd other-repository
$ git checkout -b temp
Switched to a new branch 'temp'
$ git filter-branch --prune-empty --subdirectory-filter other/ temp
Rewrite 82e8de6f33e9e4e797e0331aac1fc602f68f6bfa (13/13) (0 seconds passed, remaining 0 predicted)    
Ref 'refs/heads/temp' was rewritten
$ cd ../repository
$ git merge -s ours --no-commit --allow-unrelated-histories other/temp
Automatic merge went well; stopped before committing as requested
$ git read-tree --prefix=other -u other/temp
$ git commit
[feature/merge bc00b33] Merge remote-tracking branch 'other/temp' into feature/FTD-768-build
```
