---
layout: lesson
root: .
title: Basic queries
minutes: 30
---

## Writing my first query

Let's start by using the **articles** table. Here we have data on every
article that has been published, including the title of the article, the
authors, date of publication, etc.

Let’s write an SQL query that selects only the title column from the
articles table.

    SELECT title
    FROM articles;

We have capitalized the words SELECT and FROM because they are SQL keywords.
SQL is case insensitive, but it helps for readability, and is good style.

If we want more information, we can just add a new column to the list of fields,
right after SELECT:

    SELECT title, authors, issns, date
    FROM articles;

Or we can select all of the columns in a table using the wildcard *

    SELECT *
    FROM articles;

### Unique values

If we want only the unique values so that we can quickly see the ISSNs of
journals included in the collection, we use `DISTINCT`

    SELECT DISTINCT issns
    FROM articles;

If we select more than one column, then the distinct pairs of values are
returned

    SELECT DISTINCT issns, date
    FROM surveys;

## Filtering

Databases can also filter data – selecting only the data meeting certain
criteria.  For example, let’s say we only want data for a specific ISSN
for the *Theory and Applications of Mathematics & Computer Science* journal,
which has a ISSN code 2067-2764|2247-6202.  We need to add a
`WHERE` clause to our query:

    SELECT *
    FROM articles
    WHERE issns='2067-2764|2247-6202';

We can use more sophisticated conditions by combining tests with `AND`
and `OR`.  For example, suppose we want the data on *Theory and Applications of Mathematics & Computer Science*
published in November 2015 :

    SELECT *
    FROM articles
    WHERE (issns='2067-2764|2247-6202') AND (date = '01/11/2015');

Note that the parentheses are not needed, but again, they help with
readability.  They also ensure that the computer combines `AND` and `OR`
in the way that we intend.

If we wanted to get data for the *Humanities* and *Religions* journals, which have
ISSNs codes `2076-0787` and `2077-1444`, we could combine the tests using OR:

    SELECT *
    FROM articles
    WHERE (issns = '2076-0787') OR (issns = '2077-1444');

> ### Challenge
>
> What would be a good challenge to set at this point?

Although SQL queries often read like plain English, it is *always* useful to add
comments; this is especially true of more complex queries.

## Sorting

We can also sort the results of our queries by using `ORDER BY`.
For simplicity, let’s go back to the articles table and alphabetize it by issns.

    SELECT *
    FROM articles
    ORDER BY issns ASC;

The keyword `ASC` tells us to order it in Ascending order.
We could alternately use `DESC` to get descending order.

    SELECT *
    FROM articles
    ORDER BY authors DESC;

`ASC` is the default.

We can also sort on several fields at once.
To truly be alphabetical, we might want to order by genus then species.

    SELECT *
    FROM articles
    ORDER BY issns DESC, authors ASC;

> ### Challenge
>
> Think of nice challenges


## Order of execution

Another note for ordering. We don’t actually have to display a column to sort by
it.  For example, let’s say we want to order the articles by their ISSN, but
we only want to see Authors and Titles.

    SELECT authors, title
    FROM articles
    WHERE issns = '2067-2764|2247-6202'
    ORDER BY date ASC, authors ASC;

We can do this because sorting occurs earlier in the computational pipeline than
field selection.

The computer is basically doing this:

1. Filtering rows according to WHERE
2. Sorting results according to ORDER BY
3. Displaying requested columns or expressions.

Clauses are written in a fixed order: `SELECT`, `FROM`, `WHERE`, then `ORDER
BY`. It is possible to write a query as a single line, but for readability,
we recommend to put each clause on its own line.

> ### Challenge
>
> Let's try to combine what we've learned so far in a single
> query.  Write a nice challenge!

Previous: [SQL Introduction](00-sql-introduction.html) Next: [SQL Aggregation.](02-sql-aggregation.html)
