---
title: "Help to resolve the conflict \"Not a file: .obsidian/workspace.json\" - Help - Obsidian Forum"
source: "https://forum.obsidian.md/t/help-to-resolve-the-conflict-not-a-file-obsidian-workspace-json/76087"
author:
  - "[[anton_eng]]"
published: 2024-02-01
created: 2025-01-31
description: "I don’t understand why I have the following error in Obsidian when using the Obsidian Git plugin: ConflictsPlease resolve them and commit them using the commands Obsidian Git: Commit all changes followed by Obsidian G&hellip;"
tags:
  - "clippings"
---
`git rm --cached .obsidian/workspace.json`

also you have to create a .gitignore file and include .obsidian/workspace.json
- What is a .gitignore file? Where am I supposed to store it?
	- https://stackoverflow.com/questions/5698148/where-does-the-gitignore-file-belong

read more on [obsidiangit tips and tricks 150](https://publish.obsidian.md/git-doc/Tips-and-Tricks#Tips+and+Tricks)  
you can read more about it in [stackoverflow: How do I make Git forget about a file that was tracked, but is now in .gitignore? 73](https://stackoverflow.com/questions/1274057/how-do-i-make-git-forget-about-a-file-that-was-tracked-but-is-now-in-gitignore)