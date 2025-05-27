[5.1 From Tables to Lists](https://dcic-world.org/2025-02-09/tables-to-lists.html#%28part._.Extracting_a_.Column_from_a_.Table%29) 

![[Pasted image 20250527134432.png|100]]

> This focuses our attention on the numeric ticket sales, but we’re still stuck with a column in a table, and none of the other tables functions let us do the kinds of computations we might want over these numbers. Ideally, we want the collection of numbers on their own, without being wrapped up in the extra layer of table cells.

> In principle, we could have a collection of operations on a single column. In some languages that focus solely on tables, such as [SQL](https://en.wikipedia.org/wiki/SQL), this is what you’ll find. However, in Pyret we have many more kinds of data than just columns (as we’ll soon see [Introduction to Structured Data](https://dcic-world.org/2025-02-09/intro-struct-data.html)], we can even create our own!), so it makes sense to leave the gentle cocoon of tables sooner or later. An extracted column is a more basic kind of datum called a list, which can be used to represent a sequence of data outside of a table.


