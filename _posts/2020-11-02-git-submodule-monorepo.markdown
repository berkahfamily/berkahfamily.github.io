---
layout: post
title: "Git Submodule & Monorepo"
date: 2020-11-01 12:49:00 +0700
categories: notes
---

# Detach package to other repository as submodule

> Ref: [stackoverflow](https://stackoverflow.com/a/17864475/1586914)

1. Split into subtree

   ```bash
   git subtree split -P packages/libs -b libs
   ```

   this will checkout new branch named `libs` that only has commits from `packages/libs` folder.

2. Create new local repository and pull from this local changes.

   ```bash
   mkdir libs
   git init
   git pull ../big-project libs
   ```

3. Push this new local repo eg to `git@gitlab.com:berkahfamily/ka-libs.git`

4. In the `big-project` remove `libs` track

   ```bash
   git rm -rf packages/libs
   ## then commit and completly remove the folder
   rm -rf packages/libs
   ```

5. Add `libs` as `big-project` submodule
   ```bash
   git submodule add -- git@gitlab.com:berkahfamily/ka-libs.git packages/libs
   ```
