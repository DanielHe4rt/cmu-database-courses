* Slides: [https://15445.courses.cs.cmu.edu/fall...](https://15445.courses.cs.cmu.edu/fall2022/slides/02-modernsql.pdf) 
* Notes [https://15445.courses.cs.cmu.edu/fall...](https://15445.courses.cs.cmu.edu/fall2022/notes/02-modernsql.pdf)
* YouTube Video:  [https://www.youtube.com/watch?v=II5qNuxfSoo...](https://www.youtube.com/watch?v=II5qNuxfSoo&list=PLSE8ODhjZXjaKScG3l0nuOiDTTqpfnWFf&index=2&t=1s)
* Class Agenda:
	* Aggregations + Group By
	* String / Date / Time Operations
	* Output Control + Redirection
	* Nested Queries
	* Common Table Expressions
	* Window Functions


* Pronunciation of a specific year in English: break into two numbers
	* 1971: nineteen seventy one - 71'
	* 1972: nineteen seventy two - 72'
	* Yay learned something new

* Vocabulary
	* Enrolled - matricula
	* Ad-hoc - ??


* Historical Review: SQL
	* IBM created in the 71' the first relational query language, called **"SQUARE"** - [Square Paper 1975](https://dl.acm.org/doi/epdf/10.1145/361219.361221)
	* IBM then created **"SEQUEL"** in 1971 as a Prototype 
	* IBM released the first commercial SQL-BASED DBMS's
	* Standards organizations joined the SQL party:
		* ANSI joined at: 1986
		* ISO joined at: 1987
		* SQL born at: 1992
			* Turning the "Sequel" into Structured Query Language, aka SQL.
	* Implemented Standards so far:
		* SQL:1999 - Regex, Triggers and OO
		* SQL: 2003 - XML, WIndows, Sequences, Auto-Gen ID's
		* SQL: 2008 - Truncation, Fancy Sorting
		* SQL: 2011 - Temporal DB's, Pipelined DML
		* SQL: 2016 - JSON Polymorphic tables
		* Minimum language syntax a system need to say that it supports SQL is [SQL-92](https://db.cs.cmu.edu/files/sql/sql1992.txt)
	* Use this article ["The Rise of SQL"](https://spectrum.ieee.org/the-rise-of-sql) for the presentation
* Relational Languages
	* Data Manipulation Language (DML)
		* Commands to manipulate a certain information (INSERT, UPDATE, DELETE)
	* Data Definition Language (DDL)
		* Commands to create/model/shape a schema (Create, alter, drop) 
	* Data Control Language (DCL)
		* Commands to set permissions for each user (grant, revoke)
	* -----
	* Aggregators
		* Functions that return a single value from ma bag of tuples
		* AVG, MIN, MAX, SUM, COUNT
		* Aggregate function can **(almost)** only be used in the **SELECT** output list.
			* You can also run **GROUP BY** together with these aggregators
			* `SELECT department, SUM(salary) FROM employees GROUP BY department`
			* `SELECT AVG(gpa), COUNT(sid) FROM student WHERE login LIKE '%@cs'
		* Non Aggregated values in SELECT must be presented in the **GROUP BY**.
		* **HAVING** clause acts as same of **WHERE** clause, but for the **GROUP BY**
	* Distinct Aggregators
		* Function that returns a single and distinct value on the tuple
		* Supported aggregators:  COUNT, SUM, AVG
		* Get the number of unique students that have an “@cs” login (3).
		* `SELECT COUNT(DISTINCT login) FROM student WHERE login LIKE '%@cs'`
	* -----
	* String Operations
		* Each database specifies if is Case Insensitive/Sensitive and if you're gonna need double or single quotes.
		* Available String functions on [SQL-92 standard](https://www.postgresql.jp/document/pg702doc/user/x2732.htm)
		* By Database Structure
			* SQL-92 - Case Sentitive - Single Only
			* Postgres - Case Sensitive - Single Only
			* ScyllaDB - Case Sensitive - Single Only
			* MySQL - Case Insensitive - Single/Double
		* **LIKE** Operation
			* Used for string matching
			* Operators
				* '%' - Matches any substring (including substrings)
					* `SELECT * FROM enrolled AS e WHERE e.cid LIKE '15-%'`
				* '\_' - Match any one character
					* `SELECT * FROM student AS s WHERE s.login LIKE '%@c_'`
				* '||' - Concatenate two strings
					* `SELECT name FROM student WHERE login = LOWER(name) || '@cs'`
	* -----
	* Output Redirection
		* THIS IS GOLD and I feel dummy for not knowing this before :o
		* Concept: Storing query results inside a new table in a easier way
			* Inner SELECT must generate the same columns as the target table
				* `INSERT INTO CourseIds (SELECT DISTINCT cid FROM enrolled)`
				* `CREATE TABLE CourseIds (SELECT DISTINCT cid FROM enrolled);`
			* When use that:
				* Persist data for the Future Use
				* Performance Optimization
				* Data Sharing (outsiders)
			* Worries:
				* Storage Overhead
				* Data Mainentance
				* Data Freshness
			* Go with Cache to avoid these stuff plz
	* -----
	* Output Control 
		* OrderBY [ASC/DESC]
		* LIMIT 
	* -----
	* Nested Queries 
		* Query containing another query
		* Difficult to optimize
		* Inner queries can appear anywhere in a query
		* ![[Pasted image 20230911175534.png]]
	* -----
	* Window Function
		* Data related to that specific query result
		* Functions: ROW_NUMBER, OVER (keyword) and RANK()
		* OVER is a keyword to enable your Window Functions to be using aggregators like GROUP BY
		* `SELECT *, ROW_NUMBER() OVER (ORDER BY cid) FROM enrolled ORDER BY cid`
	* -----
	* CTE - we can do recursions with SQL? lol
* Conclusion
	* Really cool stuff and SQL got more interesting.
