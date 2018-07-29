---
layout: post
title: "Gotcha: SQL 'between' predicate"
date: 2018-07-26
tags: ["note", "code", "gotcha", "tip", "sql", "sap hana", ]
---

Just a quick note of gotcha that I have fallen into a couple of times. (We are in the SAP HANA dialect of SQL here.) This gotcha is caused by two interacting issues.

**Firstly**: In the SAP HANA SQL dialect, the between operator is syntactic sugar: `COL between LOW and HIGH` is equivalent to `(COL >= LOW) and (COL <= HIGH)` (note the non-strict inequality on the upper bound of the range). In other dialects this upper bound is strict, which can be helpful (discussed below), but on the other hand the ISO-compliant behaviour is a non-strict upper bound (`<=`). So, you need to be careful about what the dialect you have at hand is doing.

**Secondly**: Lexicographic ordering of strings dictates that: <br/> `'2018-09-03 23:34:12' > '2018-09-03' > '2018-09' > '2018'`

Consider the following query:

``` sql
-- A test of the 'between' predicate
select * from
    -- A table of dates in two formats
    (
    (select '2018-07-01' as dte, 'full date' as info from dummy)
    union all (select '2018-08-02' as dte, 'full date' as info from dummy)
    union all (select '2018-09-03' as dte, 'full date' as info from dummy) -- where you at?!?
    union all (select '2018-10-04' as dte, 'full date' as info from dummy)
    union all (select '2018-07' as dte, 'month only' as info from dummy)
    union all (select '2018-08' as dte, 'month only' as info from dummy)
    union all (select '2018-09' as dte, 'month only' as info from dummy)
    union all (select '2018-10' as dte, 'month only' as info from dummy)
    )
-- The 'between' predicate is inclusive, so we are hoping to see both months in the results
where dte between '2018-08' and '2018-09'
;
```

Output:

| DTE |	INFO |
| --- | --- |
| 2018-08-02 | full date |
| 2018-08 | month only |
| 2018-09 | month only |

Note that `2018-09-03` was excluded, which may not have been the expected behaviour. These versions will have the exected behaviour (I prefer the 2.):

1. Truncate the column (may be computationally expensive?): <br/> `where left(dte, 7) between '2018-08' and '2018-09'`

2. Be explicit. Note that the upper bound is not the last-in-range, but the first out-of-range: <br/> `where dte >= '2018-08' and dte < '2018-10'`

The other advantage of 2. is that it works in all SQL dialects, and at arbitrary levels of detail, e.g.

* `'2017-10-03' < '2018'` (dates from 2017 or before) and,
* `'2017-10-03 09:23:16' < '2017-10-04'` (datetimes on or before 2017-10-03).
