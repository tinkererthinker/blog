---
title: "Automatically resolve Syncthing conflicts using a three-way merge"
source: "https://www.rafa.ee/articles/resolve-syncthing-conflicts-using-three-way-merge/"
author:
  - "[[Rafael Epplée]]"
published: 2020-09-17
created: 2025-05-23
description: "Software engineer, artist and musician"
tags:
  - "clippings"
---
I’m trying to move away from applications and services that store data using proprietary formats or servers that are not mine. I’m relying more and more on syncthing to do that, and today I would like to show you a simple trick that I think opens up a whole range of possibilities for syncing app data.

For files that don’t change often, syncthing is already quite nice, but for other files like todo lists, notes etc. that get changed on multiple devices before being synced, syncthing doesn’t know how to combine the changes and creates a [conflict file](https://docs.syncthing.net/users/faq.html#what-if-there-is-a-conflict).

As a developer being used to git’s convenient merging, this bugged me a lot. I tend to overlook these files, and resolving them using `vimdiff` or `meld` is time consuming.

## git merge-file

Enter `git merge-file`. It’s bundled with git, but can run completely independent of any git repository. It automatically merges two versions of a file with little to no conflicts. Exquisite!

To work its magic, `merge-file` performs a “three-way merge”, where it looks at three files - the two conflicting edited versions, and their common ancestor. The common ancestor is the version that both conflicting versions are based on. Using this, git can figure out whether lines missing in one of the versions were actually added or removed - with only two files, this would be impossible ([See this stackoverflow post for a more thorough explanation](https://stackoverflow.com/questions/4129049/why-is-a-3-way-merge-advantageous-over-a-2-way-merge)).

“But where do we get the common ancestor from?”, you might ask. This is where syncthing’s awesome versioning feature comes into play. As it turns out, syncthing can automatically keep an older copy of files when they are modified. You can go all in with this and keep multiple older versions depending on different criteria, but I simply use “Trash Can” versioning which just keeps the most recent “backup” of a file. We can then use this backup to perform a three-way merge using `merge-file`!

## How to actually do this

Assuming we have a simple syncthing folder containing a file called `notes.md` with the following content:

```md
- I like markdown
```

On one node, I add a line at the start:

```md
- I like syncthing
- I like markdown
```

On the other node, I add a line at the end:

```md
- I like markdown
- I also like git
```

Once syncthing detects the conflict, it will create a `.sync-conflict` file, resulting in this directory layout:

```
├── notes.md
├── notes.sync-conflict-20200917-224540-5CYLJKE.md
└── .stversions
    └── notes~20200917-173218.md
```

We can now run `git merge-file`, providing version one, the common ancestor and then version two:

```sh
git merge-file notes.md .stversions/notes~<xxxxx>.md notes.sync-conflict-<xxxxx>.md
```

after which `notes.md` contains the following:

```md
- I like syncthing
- I like markdown
- I like also git
```

Alright! Git merged the three files without us doing anything!

## Caveats

Since syncthing only creates backups in `.stversions` when receiving changes from a remote machine and not when the file is modified locally, you might end up in a situation without a common ancestor in `.stversions`. In this case, you can simply use an empty file as the common ancestor:

```sh
touch empty.md
git merge-file notes.md empty.md notes.sync-conflict-<xxxxx>.md
```

This might result in more conflicts than usual, but in general git is pretty good at figuring out common lines between differing versions.

## Closing thoughts

I’ve only been running this by hand since I didn’t have too many conflicts, but you could easily put this in a script that periodically scrubs your folder. This way, most merges run automatically, and if any lines actually conflict, you see them when editing the conflicting file the next time - way easier than manually looking for `.sync-conflict` files all the time.

I think this method has lots of potential to enable more use cases for syncthing. For example, if you keep your playlists as `.m3u` files in a syncthing folder, you might use `git merge-file --union` to tell git to just keep both versions in case of conflicting lines. This way, at the cost of some deleted songs re-appearing, you would never have a single conflict!

This is why I love storing data in plain text files: I now have convenient, robust, offline-capable note synchronization without needing any server (be that from a third party or maintained on my own), all while being free to choose and switch between a wide range of note-taking software. For me, storing more and more of my personal data like this is the logical path forward.