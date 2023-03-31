---
title: Cleaning up merged git branches
short: Cleaning up git branches
category: Development
layout: post
date: "2023-03-31"
---

Over the last few years (and jobs) I've collected a number of scripts and processes for working with git and centralised forges like GitHub and GitLab. [switchbox] is my latest attempt to collect the bits of that automation I'm currently using, and mostly does some fiddly work to discover branches that have been merged, rebased, or squashed into the main branch of a git repository.

The most useful bit from my previous tools was the ability to clean up branches and references I wasn't using anymore. Teams at previous jobs had all enforced a standard way to apply merge requests — for instance, my team Datto enforced linear merge commits. My previous attempt at automating this cleanup, [git-river], handled standard merge commits but no other cases.

However, my current job doesn't yet enforce any standard repository configuration and repositories use a mix of rebasing, squashing, and merge commits. I wanted switchbox to handle any type of merge I could think of, so that I wouldn't need to implement this next time I encountered a project that used a different approach to merging changes.

GitHub supports "commit merging", "commit squashing", and "commit rebasing", which I used to name the three strategies I used to find merged branches in switchbox. It does cover a couple other cases beyond those though.

- Merge commits are easy: `git branch --list --merged $upstream` will list every branch merged into `$upstream`. Calling git and parsing it's output here is simple.

- Rebased branches are a little more difficult: `git cherry $upstream $branch` will tell us if each commit in `$branch` has an equivalent commit in `$upstream`. This works for rebases and cherry-picked commits, which both take the contents of a commit and reapply it onto a different parent commit — the commit hash will change, but the contents should be the same. 

- Squashed commits are painful. We can't compare branches or commits, so we're left comparing diffs between commits.

  1. The first thing to do is find a "merge base" - the common ancestor between our upstream branch and the branch that might have been squashed into it. We can do this with `git merge-base $upstream $branch`.

  2. Then we build a diff between the merge base and our potentially-squashed branch with `git diff $branch $merge_base`.

  3. Then we iterate through each commit in our upstream branch since the merge base. For each of these commits, we check if the the diff between that commit and it's parent matches the diff we built in the previous step, with `git diff $commit ^$commit`. If it does, that means the commit is the result of squashing our branch.

Once we've found our merged branches from these three strategies, switchbox then deletes them. It runs `git remote update` before doing any of this, to update all branches from their remote equivalents.

[deployment]: https://github.com/borntyping/deployment
[git-tag-version]: https://github.com/borntyping/deployment/blob/master/roles/stage2-user/files/.local/share/src/git-tag-version
[git-tidy]: https://github.com/borntyping/deployment/blob/master/roles/stage2-user/files/.local/share/src/git-tidy
[git-river]: https://github.com/datto/git-river
[git-workspace]: https://github.com/orf/git-workspace
[switchbox]: https://github.com/borntyping/switchbox
