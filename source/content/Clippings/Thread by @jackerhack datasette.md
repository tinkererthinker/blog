---
title: "Thread by @jackerhack"
source: "https://x.com/pranesh/status/1897686174547988506"
author:
  - "[[@jackerhack]]"
published: 2025-02-25
created: 2025-06-01
description:
tags:
  - "clippings"
---
**Kiran Jonnalagadda @jackerhack.ing** @jackerhack [2025-02-25](https://x.com/jackerhack/status/1894334324193071136)

My brain now thinks in Obsidian, but I need something better for tabular data. Google Sheets is so archaic – the data is not even on my disk. Excel needs a paid license for personal use, LibreOffice is so retro, Markdown tables are limited. HTML tables? That… seems good now?

---

**mas.to /** @kingslyj [2025-02-25](https://x.com/kingslyj/status/1894336108517101776)

Google Sheets SQL queries spoilt me.

There doesn't seem to be any open source or self-hosted alternative for that.

---

**Pranesh Prakash (bsky.pranesh.in)** @pranesh [2025-03-06](https://x.com/pranesh/status/1897664006200119523)

Both sqlite and duckdb allow you to directly run sql queries on CSV files. Wouldn't that be similar?

For the inverse, Visidata allows you to use python queries on any SQL db, and with vdsql to do so without loading it into memory first.

---

**mas.to /** @kingslyj [2025-03-06](https://x.com/kingslyj/status/1897675964139634853)

Nope. It's the seamless "back and forth" that makes it unbeatable.

Say, you have a 10 column sheet with the typical spreadsheet-y features automagic formulas, headers / colored cells / borders etc....

---

**mas.to /** @kingslyj [2025-03-06](https://x.com/kingslyj/status/1897676078669607119)

You want to focus on just rows from 5 columns based on conditions applied to 2 of them(or 2 of the remaining 5 columns)

Just one SQL query in a cell to generate that in a different area or a new sheet.

And now you can use spreadsheet-y features against this new range of cells.

---

**mas.to /** @kingslyj [2025-03-06](https://x.com/kingslyj/status/1897676327266000911)

Even generate graphs etc.

And making changes in the original data, updates everything derived from it automagically.

---

**Pranesh Prakash (bsky.pranesh.in)** @pranesh [2025-03-06](https://x.com/pranesh/status/1897678317341544714)

Wouldn't all this work with Visidata? I know you can create columns on the fly and work on those new columns and save the results of that? And if one of the new columns is a function on an existing column (say .lower()) then changes to the orig column will update the new column.

---

**mas.to /** @kingslyj [2025-03-06](https://x.com/kingslyj/status/1897681280697086274)

Now try doing that collaboratively with some non-tech person zealously guarding their turf from the likes of us :-)

---

**Pranesh Prakash (bsky.pranesh.in)** @pranesh [2025-03-06](https://x.com/pranesh/status/1897686174547988506)

Also check out http://datasette.io It makes tables and sql much easier for the average person, and allows for seamless sharing as well. E.g., I saw journalists sharing Datasette links to the US NSF grants being defunded, with the data being hosted on Github. Cool stuff.

---

**mas.to /** @kingslyj [2025-03-06](https://x.com/kingslyj/status/1897691379113115761)

There are also others like NocoDB and Baserow that aim to be Airtable alternatives.

But they these tools do a lot more than just making spreadsheets queryable.

I wish Libreoffice or Gnumeric would add the QUERY function like in Google Sheets.