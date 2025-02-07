---
title: "Thread by @__tinygrad__"
source: "https://x.com/__tinygrad__/status/1885591500471624102"
author:
  - "[[@__tinygrad__]]"
published: 2025-02-01
created: 2025-02-01
description: "In what sort of a crazy world does it make sense to maintain both CUDA *and* ROCm? Imagine maintaining a different compiler and standard lib"
tags:
  - "clippings"
---
**the tiny corp** @\_\_tinygrad\_\_ [2025-02-01](https://x.com/__tinygrad__/status/1885588961177067621)

In what sort of a crazy world does it make sense to maintain both CUDA \*and\* ROCm? Imagine maintaining a different compiler and standard library for each CPU architecture. It makes no sense.

---

**the tiny corp** @\_\_tinygrad\_\_ [2025-02-01](https://x.com/__tinygrad__/status/1885591500471624102)

It's worse than just that. SNPE for Qualcomm, RKNN for Rockchip, BUDA for tenstorrent, and yes, even MLX for Apple are entire \*frameworks\* that are hardware specific.

There's no reason for this. There's only so many ways ALUs, cores, RAMs, and caches fit together. tinygrad will support them all. Potentially with a few new rewrite rules for whatever your hardware is and tricks it has.

tinygrad's rewrite engine is similar to MLIRs, but it's 10x simpler. tinygrad is the frontend of PyTorch, the middleware of Triton/Pallas (both built on MLIR), and compute specific drivers that are 100x simpler than the default ones.

This year, we will prove it can be just as fast. With the same speed and way more simplicity, how do we lose?