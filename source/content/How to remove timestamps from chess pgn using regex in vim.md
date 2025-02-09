---
created: 2025-02-09
tags:
  - tech
---


vim command to delete {...}

```shell
%s/{\_.\{-\}}//g
```
### **Breakdown of this command:**

- `:%s` → Substitute (`s`) across the whole file (`%`).
- `{` → Matches the literal `{`.
- `\_.` → Matches **any character including newlines**.
- `\{-}` → Matches **as little as possible** (non-greedy).
- `}` → Matches the literal `}`.
- `//g` → Replaces matches with nothing (deleting them).

It is stranger that regex in vim are different from 'normal' regex. This is the expression you would normally use: 

```shell
/\{[\s\S]*?\}/gm
```
