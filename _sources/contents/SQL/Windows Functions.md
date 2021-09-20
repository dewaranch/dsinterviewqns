## Windows Functions

**Reference:** [📖Explanation](https://www.red-gate.com/simple-talk/sql/t-sql-programming/introduction-to-t-sql-window-functions/), [🔫Playground](https://dbfiddle.uk/?rdbms=sqlserver_2017&fiddle=6379904805d1f465cc0f6ea33fc3c0d6)

Window (also, windowing or windowed) functions perform a calculation over a set of rows. I like to think of “looking through the window” at the rows that are being returned and having one last chance to perform a calculation. The window is defined by the OVER clause which determines if the rows are partitioned into smaller sets and if they are ordered.
They allow you to add your favourite aggregate function to a non-aggregate query. Similar to Transform is pandas group by clause.

Some common windows functions are as follows:

- **Ranking functions**
	- ROW_NUMBER: *is used to add unique row numbers to a partition or to the entire result set. It has the ability to turn non-unique rows into unique rows.*
	- RANK: *it will give numbers same as row_number just that same data will get same rank*
	- DENSE_RANK: *doesnot skip and rank number*
	- NTILE: *It assigns bucket numbers to the rows instead of row numbers or ranks*

```{figure} ../SQL/images/image2.PNG
---
name: image2
---
Ranking functions, check playground to work with this
```

- **Offset functions**
	- LAG
	- LEAD
	- FIRST_VALUE
	- LAST_VALUE

- **Statistical functions**
 	– PERCENT_RANK
 	- CUME_DIST
 	- PERCENTILE_DISC
 	- PERCENTILE_CONT

One problem is you cannot add window functions to the WHERE clause.





```{admonition} Problem: Rank Scores
:class: tip, dropdown

**Reference - [Leetcode](https://leetcode.com/problems/rank-scores/)**

Write a SQL query to rank scores. If there is a tie between two scores, both should have the same ranking. Note that after a tie, the next ranking number should be the next consecutive integer value. In other words, there should be no "holes" between ranks.

| Id | Score |
|----|-------|
| 1  | 3.40  |
| 2  | 3.65  |
| 3  | 4.00  |
| 4  | 3.50  |
| 5  | 4.00  |
| 6  | 3.65  |

For example, given the above Scores table, your query should generate the following report (order by highest score):

| score | Rank    |
|-------|---------|
| 4.00  | 1       |
| 4.00  | 1       |
| 3.95  | 2       |
| 3.65  | 3       |
| 3.65  | 3       |
| 3.40  | 4       |

```

```{admonition} Solution:
:class: dropdown

The tie resolving method which is being asked in the question is called Dense Rank, if we use Rank it will have "holes"

`
select 
Score, dense_rank() over(order by score desc) as Rank
from Scores
`

```

```{admonition} Problem: Consecutive Numbers
:class: tip, dropdown

**Reference - [Leetcode](https://leetcode.com/problems/consecutive-numbers/)**


Write an SQL query to find all numbers that appear at least three times consecutively.

Return the result table in any order.

Input: 

Logs table:

| Id | Num |
|----|-----|
| 1  | 1   |
| 2  | 1   |
| 3  | 1   |
| 4  | 2   |
| 5  | 1   |
| 6  | 2   |
| 7  | 2   |


Result table:

| ConsecutiveNums |
|-----------------|
| 1               |

1 is the only number that appears consecutively for at least three times.

```

```{admonition} Solution:
:class: dropdown

Multiple solutions are possible, one of them is given below

`

with a(Num,NextNum,SecondNextNum ) as(

SELECT   Num
         , LEAD(Num, 1) OVER (ORDER BY Id) AS NextNum
         , LEAD(Num, 2) OVER (ORDER BY Id) AS SecondNextNum
      FROM Logs
      
)

select distinct(Num) as ConsecutiveNums from a
where
Num = NextNum
and Num = SecondNextNum

`

```