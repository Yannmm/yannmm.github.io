---
layout: post
title: Git - the Stupid Content Tracker
tags: git
---

```
GIT(1)
        git - the stupid content tracker
```

## Ideas

- First Git is able to generate a hash for any piece of data. Like the coordinate of a point on a map. (Content tracking)
- Git repository hold the hash from above.
- A `commit` is just a piece of string that trakcs parent commit(s), author some files or trees.
- A `tree` is just directory which may contian files and other directories(trees).
- A new tree is created each time there is file in the tree gets updated. The new tree will link to old tree.
- Git is a mini file system using above object model to store data.
- Second a `branch` only records hash of certain commit, so it's just a pointer. (Versioning)
- `HEAD` is a special pointer keeping track of your current branch.
- When `HEAD` moves, git regenerate all contents in working area by traversing trees starting from current commit.
- Third since hash is universally unique, data of that hash can be passed around network. (Distribution)

## Git Worktree

It seems Git just copying current working directory somewhere else so you can have any number of working directories at the same time.

## References

- ![How git works?](https://www.youtube.com/watch?v=nHkLxts9Mu4)
- ![ZSH git plugin](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/git)
