---
created: 2025-02-09
---
I want to make sense of [[tinygrad]]'s codebase. Let's dive in!

Why is tensor.py almost 4000 lines long?!?!

![[Pasted image 20250209204447.png]]
![[Pasted image 20250209204408.png]]

Nobody has time to read 4000 lines of code, so I asked ChatGPT to analyze the `tensor.py` file and identify its essential functions, as well as the parts that can be ignored initially.

### Key Observations:

- The main class is **`Tensor`**, defined at line 119. This is likely the core data structure.
- There are a few other classes (`train`, `test`), which seem to be context managers.
- The first ~100 lines contain many helper functions (`_apply_map_to_tensors`, `_frompy`, `_fromnp`, etc.), which likely handle conversions, metadata, and shape manipulations.

### Getting Started:

To understand the essentials, focus on:

1. **The `Tensor` class** (starting at line 119) – This is the core data structure.
2. **Key tensor operations** inside the `Tensor` class (methods like `__init__`, `__add__`, `matmul`, etc.).
3. **Basic helper functions** like `_frompy`, `_fromnp`, and `get_shape`, which handle conversions.

### What You Can Ignore (Initially):

- Any functions starting with `_` (e.g., `_metaop`, `_apply_winograd_matrix`) – These are internal helpers.
- Winograd-related functions (`_get_winograd_matcols`, `_apply_winograd_matrix`) – Likely for advanced optimizations.
- Context manager classes (`train`, `test`) – Not critical unless you're working on training mode behavior.

```shell
(3929, [(22, 'def _apply_map_to_tensors(applied_map:dict[UOp, UOp]) -> None:'), (48, 'def _metaop(op, shape:tuple[sint,...], dtype:DType, device:Union[str, tuple[str, ...]], arg=None):'), (52, "def _from_np_dtype(npdtype:'np.dtype') -> DType: # type: ignore [name-defined] # noqa: F821"), (55, 'def _to_np_dtype(dtype:DType) -> Optional[type]:'), (59, "def _fromnp(x: 'np.ndarray') -> UOp: # type: ignore [name-defined] # noqa: F821"), (65, 'def get_shape(x) -> tuple[int, ...]:'), (71, 'def _frompy(x:Union[list, tuple, bytes], dtype:DType) -> UOp:'), (82, 'def _get_winograd_matcols(mat, dims:int, shp:tuple[sint, ...], device:Union[str, tuple[str, ...]], dtype:DType) -> list[list[Tensor]]:'), (87, 'def _apply_winograd_matrix(mat, t:Tensor, dims:int) -> Tensor:'), (98, 'def _align_left(*shapes:tuple[sint, ...]) -> tuple[tuple[sint, ...], ...]:')], [(119, 'class Tensor(SimpleMathTrait):'), (198, 'class train(ContextDecorator):'), (203, 'class test(ContextDecorator):')])
```

We can also skim through tinygrad's [quickstart guide](https://docs.tinygrad.org/quickstart/).

