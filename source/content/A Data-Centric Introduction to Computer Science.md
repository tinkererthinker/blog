[5.1 From Tables to Lists](https://dcic-world.org/2025-02-09/tables-to-lists.html#%28part._.Extracting_a_.Column_from_a_.Table%29) 

![[Pasted image 20250527134432.png|100]]

> This focuses our attention on the numeric ticket sales, but we’re still stuck with a column in a table, and none of the other tables functions let us do the kinds of computations we might want over these numbers. Ideally, we want the collection of numbers on their own, without being wrapped up in the extra layer of table cells.

> In principle, we could have a collection of operations on a single column. In some languages that focus solely on tables, such as [SQL](https://en.wikipedia.org/wiki/SQL), this is what you’ll find. However, in Pyret we have many more kinds of data than just columns (as we’ll soon see [Introduction to Structured Data](https://dcic-world.org/2025-02-09/intro-struct-data.html)], we can even create our own!), so it makes sense to leave the gentle cocoon of tables sooner or later. An extracted column is a more basic kind of datum called a list, which can be used to represent a sequence of data outside of a table.

Another example would be the document distance problem where we represent two documents as two lists of words. Then, we map two lists of strings to two lists of vectors which allows us to work with the dot product.

## 4.2 Processing Tables

- Which discount code has been used most often?
- Is there a relationship between the number of tickets purchased in one order and the time of purchase?
- How many orders have been made for each delivery option?

In data analysis, we often work with large [[Datasette|datasets]], some of which were collected by someone else. Datasets don’t necessarily come in a form that we can work with. We might need the raw data pulled apart or condensed to coarser granularity. Some data might be missing or entered incorrectly. On top of that, we have to plan for long-term maintenance of our datasets or analysis programs. Finally, we typically want to use visualizations to either communicate our data or to check for issues with our data.

##### 5.2.2 Some Example Exercises[](https://dcic-world.org/2025-02-09/processing-lists.html#\(part._my-len\) "Link to here")

To illustrate our thinking, let’s work through a few concrete examples of list-processing functions. All of these will consume lists; some will even produce them. Some will transform their inputs (like `map`), some will select from their inputs (like `filter`), and some will aggregate their inputs. Since some of these functions already exist in Pyret, we’ll name them with the prefix `my-` to avoid errors.

#### 8.1 Functions as Data

It’s interesting to consider how expressive the little programming we’ve learned so far can be. To illustrate this, we’ll work through a few exercises of interesting concepts we can express using just functions as values. We’ll write two quite different things, then show how they converge nicely.