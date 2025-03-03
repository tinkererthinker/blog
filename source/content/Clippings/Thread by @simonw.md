---
title: "Thread by @simonw"
source: "https://x.com/smsm1/status/1572408841014509569"
author:
  - "[[@simonw]]"
published: 2022-09-20
created: 2025-02-22
description: "If someone gives you a CSV file with 100,000 rows in it, what tools do you use to start exploring and understanding that data?"
tags:
  - "clippings"
---
**Simon Willison** @simonw [2022-09-20](https://x.com/simonw/status/1572285367382061057)

If someone gives you a CSV file with 100,000 rows in it, what tools do you use to start exploring and understanding that data?

---

**Simon Willison** @simonw [2022-09-20](https://x.com/simonw/status/1572285685280960514)

(I'm mainly interested in answers from people who do this kind of thing relatively often and DON'T use SQLite / Datasette to do it, but if you do use those I'm interested in hearing from you too!)

---

**Simon Willison** @simonw [2022-09-20](https://x.com/simonw/status/1572285785189285893)

Follow up: same question for 1 million rows, 10 million rows, 1 billion rows

---

**Simon Willison** @simonw [2022-09-20](https://x.com/simonw/status/1572294557131476995)

Wow the answers to this are absolutely fantastic, and VERY varied

---

**Simon Willison** @simonw [2022-09-20](https://x.com/simonw/status/1572295332767371265)

My own answer: I either open the CSV directly in the Datasette Desktop Mac application (https://datasette.io/desktop) or I do this:

sqlite-utils insert /tmp/data.db rows big.csv --csv

datasette /tmp/data.db

That gives me a table called "rows" in a fresh SQLite database

---

**Kyle Falconer** @pereclies [2022-09-20](https://x.com/pereclies/status/1572354157176311809)

Datasette looks interesting. Do you know of something like that but for Windows or Linux?

---

**Shaun McDonald** @smsm1 [2022-09-21](https://x.com/smsm1/status/1572408841014509569)

Datasette works on Linux and Windows too from the command line, not sure about the GUI being available. I've got a team using it regularly for exploring GTFS files.

---

**Shaun McDonald** @smsm1 [2022-09-21](https://x.com/smsm1/status/1572409291167916034)

(where other more specific tools don't succeed or trying to find very specific info that the other tools don't make available easily).