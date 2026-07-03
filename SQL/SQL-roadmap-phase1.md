# Learning Roadmap: SQL & Relational Databases — Phase 1 (PostgreSQL)

**Goal:** Become genuinely comfortable with SQL and the relational model in PostgreSQL — design a small normalized schema, query across related tables (joins + aggregation), write and modify data safely inside transactions, and both **seed** and **verify** database state for tests — and understand *why* the relational model behaves the way it does, not just recite syntax.
**Context:** Three drivers weighted evenly — (1) **app backend** (Supabase/Postgres for the Visual Life Archive app), (2) **QAOps** (test-data setup/teardown and DB state verification in automated tests), and (3) **general fluency** (querying data and thinking relationally). The core of SQL is identical across all three, so the roadmap teaches the machine first and points it at each use case in the final stage.
**Time budget:** ~50–68 hrs of focused study + practice. No fixed schedule — estimates are in hours so you can pace yourself. SQL rewards reps: run every example against a real database.
**Starting point:** Total beginner — never written SQL. No database background assumed. JavaScript/Node is **not** a prerequisite (SQL stands on its own); it only reappears as light context in Stage 7 when connecting a database to app code.

---

## 🗺️ Overview

You start by building the *right mental model* — what a relational database actually is (tables of rows and columns linked by shared keys) and why SQL is a **declarative** language where you describe *what* data you want, not *how* to fetch it. From there it's relentlessly practical: querying one table fluently, then designing tables properly (data types, constraints, and just enough normalization to avoid the classic beginner mistakes), then the concept that makes it "relational" — **foreign keys and JOINs**. The back half turns toward your goals: aggregating and summarizing data, then writing/modifying data safely inside **transactions** (the heart of reliable test-data setup), and finally pointing everything at your real stack — **Supabase**, indexes, and seeding/verifying database state for automated tests. By the end you won't just make queries return rows; you'll know *why* the query planner did what it did and *why* your schema is shaped the way it is.

---

## ⚠️ A Note On Your Starting Point (read this)

You picked "all three goals evenly," which is the right call — the core of SQL (SELECT, JOINs, constraints, transactions) is the same whether you're seeding a test database, powering the Visual Life Archive app, or answering a question about your data. But it means **you can't skip the fundamentals to rush to "Supabase stuff."** The reason a Supabase table has a foreign key, the reason a test needs a transaction to roll back cleanly, the reason a JOIN returns the rows it does — all of it is just the relational model + SQL applied. Learn the machine first (Stages 1–6), then point it at your tools (Stage 7). The must-knows are flagged 🔴; don't skip those.

One more thing: **type every example yourself.** SQL is a motor skill as much as a concept. Reading a JOIN and writing a JOIN are different abilities, and only the second one shows up when you need it.

---

## Prerequisites (Complete Before Stage 1)

- [ ] **Basic command line** 🟡 — open a terminal, run a command, navigate directories. You have this from your Git track. Needed to run `psql` (though you can also use a GUI/web editor). — est. **0–1 hr**
- [ ] **A place to run PostgreSQL** 🔴 — pick one: (a) install PostgreSQL locally + use `psql`/pgAdmin, (b) spin up a free **Supabase** project and use its SQL Editor, or (c) a browser sandbox for the early stages. You'll want a real Postgres (a or b) by Stage 3. — est. **1 hr**
> ✅ That's it. No programming background required. If you already have a terminal and a Postgres to connect to, skip straight to Stage 1.

---

## Stage 1: The Relational Model & Setup — Foundation
**Goal of this stage:** Understand what a relational database *is* and what SQL *is*, and get a working Postgres you can run queries against.
**Estimated time:** 4–6 hrs
**Milestone:** You can explain, in your own words, what a table/row/column is, why data is split across related tables, and what "declarative" means — and you have a PostgreSQL instance where you can load a sample database and run your first `SELECT`.

### Must-Know Topics 🔴
- [ ] **What a relational database is** — data organized into **tables** (relations) of **rows** (records) and **columns** (fields); why this model has dominated for 50 years; the intuition that a table models *one kind of thing*
- [ ] **Why relational vs. a spreadsheet or NoSQL** — the problem relationships and integrity solve; where a single giant table falls apart (redundancy, inconsistency)
- [ ] **SQL is declarative** — you describe *what* you want; the database's query planner decides *how* to get it. This is the root mental shift for anyone coming from imperative programming
- [ ] **PostgreSQL specifically** — what Postgres is, why it's the default serious open-source choice (and why Supabase is "just Postgres"); SQL standard vs. Postgres dialect
- [ ] **Connecting & running SQL** — `psql` basics (or the Supabase SQL Editor / pgAdmin), loading a sample database, running a statement, reading the result grid

### Should-Know Topics 🟡
- [ ] Client tools landscape — `psql` (CLI) vs. pgAdmin/DBeaver (GUI) vs. Supabase's web editor; when each is convenient
- [ ] What a "schema" and a "database" are at a glance (you'll go deeper later) — the `public` schema you'll live in by default

### Deep-Learning-Teacher Sessions for This Stage
> Use `deep-learning-teacher` on each in order:
> 1. "Teach me the relational model — what tables, rows, and columns are, and *why* we split data across related tables instead of one big spreadsheet. Quiz me until I can explain it without notes."
> 2. "Teach me what SQL is and why it's declarative, and walk me through connecting to PostgreSQL and running my first query. Verify I understand what the database is doing when I run a SELECT."

---

## Stage 2: Querying a Single Table — SELECT, Filtering & Sorting
**Goal of this stage:** Retrieve exactly the rows and columns you want from one table, filtered and sorted, fluently and without looking up syntax.
**Estimated time:** 8–10 hrs
**Milestone:** Given any single table, you can select specific columns, filter with a compound `WHERE`, sort and page the results, handle `NULL`s correctly, and de-duplicate with `DISTINCT` — and explain the logical order the clauses execute in.

### Must-Know Topics 🔴
- [ ] `SELECT` & column selection — choosing columns, `*`, column **aliases** (`AS`), computed columns
- [ ] `WHERE` filtering — comparison operators, `AND`/`OR`/`NOT`, and precedence; `IN`, `BETWEEN`, `LIKE`/`ILIKE` (pattern matching)
- [ ] **`NULL` handling** — why `NULL` is "unknown," why `= NULL` doesn't work, and `IS NULL` / `IS NOT NULL` (this trips up *everyone* early)
- [ ] `ORDER BY` — sorting ascending/descending, sorting by multiple columns
- [ ] `LIMIT` / `OFFSET` — capping and paging results
- [ ] `DISTINCT` — eliminating duplicate rows
### Should-Know Topics 🟡
- [ ] The **logical order of execution** — that `FROM → WHERE → SELECT → ORDER BY → LIMIT` run in a different order than they're written; explains why a `SELECT` alias can't be used in `WHERE`
- [ ] Basic string/number/date functions and operators — concatenation, arithmetic, `LOWER`/`UPPER`, casting with `::`
### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me the SELECT statement — choosing columns, aliases, and filtering with WHERE including IN, BETWEEN, and LIKE. Quiz me by giving me a table and a question and making me write the query."
> 2. "Teach me ORDER BY, LIMIT, DISTINCT, and especially NULL handling with IS NULL. Then teach me the logical order SQL clauses actually execute in, and quiz me on why a SELECT alias can't be referenced in WHERE."

---

## Stage 3: Designing Tables — Data Types, Constraints & Schema Design
**Goal of this stage:** Create your own tables *properly* — right data types, the constraints that protect your data, and enough normalization to avoid the classic beginner schema mistakes.
**Estimated time:** 8–11 hrs
**Milestone:** You can write `CREATE TABLE` with appropriate types and constraints, choose a primary key deliberately, alter and drop tables, and take a messy "one big table" and normalize it into clean related tables — explaining *why* each split reduces redundancy.

### Must-Know Topics 🔴
- [ ] **`CREATE TABLE`** & core PostgreSQL **data types** — `text`/`varchar`, `integer`/`bigint`, `numeric`, `boolean`, `date`/`timestamptz`, `uuid`, and `json`/`jsonb` (relevant to your app); choosing the right type and *why it matters*
- [ ] **Constraints** — `PRIMARY KEY`, `NOT NULL`, `UNIQUE`, `DEFAULT`, `CHECK`; how constraints make the database enforce correctness instead of your app code
- [ ] **Primary keys** — what makes a good one; `GENERATED ... AS IDENTITY` (auto-increment) vs. `uuid`; why every table should have one
- [ ] `ALTER TABLE` / `DROP TABLE` — evolving a schema: adding/removing columns and constraints
- [ ] **Normalization basics (1NF → 2NF → 3NF)** — the intuition, not the academic formalism: no repeating groups, every column depends on the key, split out anything that describes a *different* thing; the update/insert/delete anomalies normalization prevents

### Should-Know Topics 🟡
- [ ] Composite keys and when a single column isn't enough to identify a row
- [ ] When to **deliberately denormalize** — that 3NF is a default, not a religion; read-heavy or prototype cases where you relax it on purpose
- [ ] `SERIAL` vs. identity columns — the older `SERIAL` you'll see in tutorials vs. the modern standard-SQL identity syntax

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me CREATE TABLE, PostgreSQL data types, and constraints (PRIMARY KEY, NOT NULL, UNIQUE, DEFAULT, CHECK). Quiz me by giving me a real-world thing to model and making me write the table definition with the right types and constraints."
> 2. "Teach me database normalization — 1NF, 2NF, 3NF — using the intuition of anomalies rather than the formal definitions. Give me a messy single table and make me normalize it into related tables, then have me justify each split."

---

## Stage 4: Relationships & JOINs — Where It Becomes "Relational" 🧠
**Goal of this stage:** This is the concept that makes a relational database relational. Link tables with foreign keys and combine them with JOINs — confidently, without accidental Cartesian products.
**Estimated time:** 8–11 hrs (slow down here — JOINs are *the* skill everything else leans on)
**Milestone:** You can define foreign keys with the right `ON DELETE` behavior, model one-to-many and many-to-many relationships, and write `INNER`/`LEFT` (and `FULL`) joins across multiple tables — and predict which rows a given join will return before you run it.

### Must-Know Topics 🔴
- [ ] **Foreign keys & referential integrity** — a column that references another table's primary key; how the database *prevents* orphaned rows; `ON DELETE CASCADE` / `SET NULL` / `RESTRICT` and choosing deliberately
- [ ] **Relationship shapes** — **one-to-many** (the everyday case: one user → many photos), **many-to-many** via a **join/junction table**, and one-to-one; recognizing which you have
- [ ] **`INNER JOIN`** — matching rows across tables on a join condition; table aliases; joining three or more tables
- [ ] **`LEFT JOIN`** (and `RIGHT`/`FULL OUTER`) — keeping unmatched rows; using `WHERE ... IS NULL` to find "rows in A with no match in B" (the anti-join pattern)
- [ ] **The Cartesian product trap** — what happens when you forget the `ON` condition, and why it's dangerous on real tables

### Should-Know Topics 🟡
- [ ] Self-joins — joining a table to itself (e.g., an org chart), light touch
- [ ] `USING` vs. `ON`, and why explicit aliases prevent ambiguous-column bugs
- [ ] How `NULL` in a join key silently drops rows from an `INNER JOIN`

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me foreign keys and referential integrity — how they link tables and prevent orphaned rows, and the ON DELETE options. Then teach me one-to-many and many-to-many relationships with a join table. Quiz me on modeling relationships for a real app."
> 2. "Teach me JOINs — INNER, LEFT, and FULL OUTER — using the mental model of matching rows on a condition. Give me two tables and make me predict exactly which rows each join returns, including the Cartesian-product trap and the LEFT JOIN ... IS NULL anti-join pattern."

---

## Stage 5: Aggregation, Grouping & Subqueries — Answering Questions
**Goal of this stage:** Move from "fetch rows" to "answer questions about the data" — counts, sums, averages, grouped summaries, and queries nested inside queries.
**Estimated time:** 8–10 hrs
**Milestone:** You can compute aggregates, group rows and filter groups with `HAVING`, combine grouping with joins, and use a subquery (and a CTE) to answer a question that a single flat query can't — and explain the difference between `WHERE` and `HAVING`.

### Must-Know Topics 🔴
- [ ] **Aggregate functions** — `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`; aggregating over all rows vs. per group
- [ ] **`GROUP BY`** — collapsing rows into groups; the rule that every non-aggregated `SELECT` column must be grouped; grouping across a JOIN (e.g., photos-per-user)
- [ ] **`HAVING` vs. `WHERE`** — filtering *groups* after aggregation vs. filtering *rows* before it; *why* they're separate and where each belongs
- [ ] **Subqueries** — a query inside a query: in `WHERE` (`IN`, `EXISTS`), and as a value; correlated vs. uncorrelated at a glance
- [ ] **CTEs (`WITH`)** — naming a subquery to make complex queries readable; the modern default for anything non-trivial

### Should-Know Topics 🟡
- [ ] `EXISTS` vs. `IN` — subtle correctness/performance differences, especially with `NULL`s
- [ ] Set operations — `UNION` / `UNION ALL`, `INTERSECT`, `EXCEPT` (light)
- [ ] A first look at **window functions** — that `OVER (...)` exists for "aggregate without collapsing rows" (awareness only; deep-dive is Phase 2)

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me aggregate functions and GROUP BY, including grouping across a JOIN, and drill me hard on HAVING vs. WHERE — where each filter belongs and why. Give me questions about data and make me write the grouped query."
> 2. "Teach me subqueries and CTEs (WITH) — using a query inside a query to answer something a flat query can't. Give me a multi-step question and make me solve it both with a subquery and with a CTE, then compare readability."

---

## Stage 6: Writing Data & Transactions — Integrity in Motion 🧠
**Goal of this stage:** Change data safely. This is the QAOps-critical stage: `INSERT`/`UPDATE`/`DELETE`, upserts, and **transactions** — the mechanism that makes test-data setup and teardown reliable and reversible.
**Estimated time:** 6–9 hrs
**Milestone:** You can insert, update, delete, and upsert rows (returning what changed), wrap multiple statements in a transaction, and explain — with a concrete testing example — why a transaction that `ROLLBACK`s gives you clean, isolated test state every run.

### Must-Know Topics 🔴
- [ ] **`INSERT`** — single and multi-row inserts; `INSERT ... RETURNING` to get back generated IDs (huge for test setup)
- [ ] **`UPDATE`** & **`DELETE`** — with `WHERE`; the classic footgun of forgetting the `WHERE` clause and changing every row
- [ ] **Upsert** — `INSERT ... ON CONFLICT DO UPDATE/NOTHING`; idempotent seeding
- [ ] **Transactions** — `BEGIN` / `COMMIT` / `ROLLBACK`; all-or-nothing units of work
- [ ] **ACID** — Atomicity, Consistency, Isolation, Durability at an intuitive level; *why* transactions matter for correctness — and specifically for **test data**: set up state, run the test, roll back to a pristine database

### Should-Know Topics 🟡
- [ ] Isolation levels at a glance — that concurrent transactions can interfere, and Postgres's default (`READ COMMITTED`); awareness, not depth
- [ ] `TRUNCATE` vs. `DELETE` — fast full-table clears for teardown, and the differences
- [ ] Constraint violations as transaction failures — how a failed `INSERT` aborts the transaction

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me INSERT, UPDATE, DELETE, and upsert (ON CONFLICT), including RETURNING and the forgotten-WHERE footgun. Quiz me on writing safe data-modification statements."
> 2. "Teach me transactions (BEGIN/COMMIT/ROLLBACK) and ACID at an intuitive level, and connect it directly to test automation: how a transaction I roll back gives me clean, isolated database state for every test run. Make me design a setup/teardown flow for a test."

---

## Stage 7: PostgreSQL In Your Real Stack — Supabase, Indexes & Test Data
**Goal of this stage:** Point everything you've learned at your actual goals — the Supabase-backed app, seeding/verifying data for automated tests, and a first real look at performance.
**Estimated time:** 8–11 hrs
**Milestone:** You can design and create the Visual Life Archive schema in Supabase (using both the Table Editor and the SQL Editor), seed and verify database state as part of a test, add an index and explain what it buys you, and articulate where SQL/Postgres stops and the next layer (RLS, ORMs, migrations) begins.

### Must-Know Topics 🔴
- [ ] **Supabase = Postgres** — the Table Editor vs. the SQL Editor; that everything you learned is the real database underneath; schemas and the `public` schema; a first awareness of **Row Level Security** (that Supabase enables it and *why* — depth is Phase 2)
- [ ] **Seeding & verifying test data** — writing SQL to set up known state before a test and to **assert** on state after (query the DB to confirm the app wrote what it should); tying this back to Stage 6 transactions for teardown
- [ ] **Indexes — intro** — what an index is (a lookup structure), why queries get faster, that **primary keys are indexed automatically but foreign keys are not**; the cost (writes/space) so you don't index everything
- [ ] **Reading a query's plan — first look** — `EXPLAIN` exists and shows whether an index is used (awareness; tuning is Phase 2)
- [ ] **Where SQL meets app code** — conceptually how an app (Node/`supabase-js`, or Cypress/Playwright in a test) sends SQL/queries to Postgres; parameterized queries and *why string-concatenating user input is dangerous* (SQL injection, at an awareness level)

### Should-Know Topics 🟡
- [ ] **Views** — saving a complex query as a reusable virtual table (Supabase docs lean on this); light touch
- [ ] **Migrations** — that schema changes belong in version-controlled migration files, not clicked into a dashboard (connects to your Git track); awareness
- [ ] The **ORM / query-builder** layer above SQL — `supabase-js`, Prisma, Drizzle — and why you still learned raw SQL first (you can read what they generate and drop to SQL when they can't)

### Deep-Learning-Teacher Sessions for This Stage
> 1. "Teach me how Supabase is really just Postgres — the Table Editor vs. SQL Editor, schemas, and a first awareness of Row Level Security. Walk me through designing and creating a small schema (like a per-day photo/caption app) both ways, and verify I understand what's happening in the database underneath."
> 2. "Teach me using SQL for test automation — seeding known state before a test and querying the database to verify state after, with transactions for teardown. Then teach me the intro to indexes: what they are, why FK columns often need one, and the trade-off. Quiz me on when an index helps and connect it to EXPLAIN."

---

## 🏁 Final Milestone
You can take an app idea from nothing to a working relational database: design a normalized schema in PostgreSQL with the right types, keys, and constraints; query it fluently across related tables with joins and aggregation; insert/update/delete data safely inside transactions; and — the QAOps payoff — seed and verify database state for automated tests with clean, isolated setup and teardown. You can do all of this in Supabase against the Visual Life Archive app, add an index where it matters, and explain to another engineer *why* your schema is shaped the way it is, *why* a given JOIN returns the rows it does, and *why* a rolled-back transaction gives you a pristine test database every run — not just recite the syntax.

---

## ⏭️ What's Out of Scope (For Now)

- **Row Level Security (RLS) in depth** — Supabase's auth-based row policies are essential *for the app*, but they're a security layer on top of the SQL you're learning here. Awareness now; a dedicated Phase 2 (pairs naturally with a Supabase/auth roadmap).
- **Query performance tuning** — `EXPLAIN ANALYZE`, index types (B-tree/GIN/GiST), the query planner internals. You get an intro to indexes in Stage 7; real tuning is Phase 2.
- **Window functions & advanced analytics** — `OVER (PARTITION BY ...)`, `ROW_NUMBER`, `RANK`, running totals, recursive CTEs. Powerful and mainstream, but a Phase 2 topic once the core clicks.
- **Stored procedures, functions & triggers (PL/pgSQL)** — logic *inside* the database. Situational; learn it the day a project needs it.
- **Database migrations tooling** — Supabase migrations, Prisma Migrate, Flyway. Flagged as should-know awareness in Stage 7; the tooling deep-dive is its own topic.
- **ORMs / query builders** (`supabase-js`, Prisma, Drizzle) — you deliberately learned raw SQL first so these make sense; adopting one is a separate track.
- **Database administration** — backups, replication, connection pooling, roles/permissions at scale, scaling Postgres. Relevant when you run infrastructure, not when you're learning the language.
- **NoSQL comparison depth** — you'll understand *why* relational fits your app; a real NoSQL (document/key-value) study is separate.

---

## 🔗 Cross-References To Your Other Roadmaps

- **JavaScript Phase 1 (Stage 8) & TypeScript Phase 1 (Stage 7) capstones** both list "advanced backend (databases)" as *out of scope* and keep their Express APIs deliberately minimal. **This roadmap fills that gap** — it's the database layer those capstones stop short of. Once this is done, their APIs can talk to a real, well-designed Postgres instead of an in-memory stub.
- **React Native + Expo Phase 1** targets the Visual Life Archive app with **Supabase** as the backend. Stage 7 here designs the schema that roadmap's app will read from and write to.
- **GitHub Phase 1 (Stage 5, Actions II)** runs test suites in CI. The seed/verify pattern from Stage 6–7 here is what those CI test jobs will use to set up and tear down database state.

---

## 📌 Suggested Order of `deep-learning-teacher` Sessions
> Copy-paste these as prompts, in order.
1. Stage 1 — Relational model: "Teach me the relational model — what tables, rows, and columns are, and why we split data across related tables instead of one big spreadsheet. Quiz me until I can explain it without notes."
2. Stage 1 — SQL & setup: "Teach me what SQL is and why it's declarative, and walk me through connecting to PostgreSQL and running my first query. Verify I understand what the database is doing when I run a SELECT."
3. Stage 2 — SELECT/WHERE: "Teach me the SELECT statement — choosing columns, aliases, and filtering with WHERE including IN, BETWEEN, and LIKE. Quiz me by giving me a table and a question and making me write the query."
4. Stage 2 — Sorting/NULL/order: "Teach me ORDER BY, LIMIT, DISTINCT, and especially NULL handling with IS NULL. Then teach me the logical order SQL clauses actually execute in, and quiz me on why a SELECT alias can't be referenced in WHERE."
5. Stage 3 — Tables/constraints: "Teach me CREATE TABLE, PostgreSQL data types, and constraints (PRIMARY KEY, NOT NULL, UNIQUE, DEFAULT, CHECK). Quiz me by giving me a real-world thing to model and making me write the table definition with the right types and constraints."
6. Stage 3 — Normalization: "Teach me database normalization — 1NF, 2NF, 3NF — using the intuition of anomalies rather than the formal definitions. Give me a messy single table and make me normalize it into related tables, then have me justify each split."
7. Stage 4 — Foreign keys/relationships: "Teach me foreign keys and referential integrity — how they link tables and prevent orphaned rows, and the ON DELETE options. Then teach me one-to-many and many-to-many relationships with a join table. Quiz me on modeling relationships for a real app."
8. Stage 4 — JOINs: "Teach me JOINs — INNER, LEFT, and FULL OUTER — using the mental model of matching rows on a condition. Give me two tables and make me predict exactly which rows each join returns, including the Cartesian-product trap and the LEFT JOIN ... IS NULL anti-join pattern."
9. Stage 5 — Aggregation/GROUP BY: "Teach me aggregate functions and GROUP BY, including grouping across a JOIN, and drill me hard on HAVING vs. WHERE — where each filter belongs and why. Give me questions about data and make me write the grouped query."
10. Stage 5 — Subqueries/CTEs: "Teach me subqueries and CTEs (WITH) — using a query inside a query to answer something a flat query can't. Give me a multi-step question and make me solve it both with a subquery and with a CTE, then compare readability."
11. Stage 6 — Writing data: "Teach me INSERT, UPDATE, DELETE, and upsert (ON CONFLICT), including RETURNING and the forgotten-WHERE footgun. Quiz me on writing safe data-modification statements."
12. Stage 6 — Transactions/ACID: "Teach me transactions (BEGIN/COMMIT/ROLLBACK) and ACID at an intuitive level, and connect it directly to test automation: how a transaction I roll back gives me clean, isolated database state for every test run. Make me design a setup/teardown flow for a test."
13. Stage 7 — Supabase/schema: "Teach me how Supabase is really just Postgres — the Table Editor vs. SQL Editor, schemas, and a first awareness of Row Level Security. Walk me through designing and creating a small schema (like a per-day photo/caption app) both ways, and verify I understand what's happening in the database underneath."
14. Stage 7 — Test data & indexes: "Teach me using SQL for test automation — seeding known state before a test and querying the database to verify state after, with transactions for teardown. Then teach me the intro to indexes: what they are, why FK columns often need one, and the trade-off. Quiz me on when an index helps and connect it to EXPLAIN."
