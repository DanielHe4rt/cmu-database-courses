
Link: [YouTube]( https://www.youtube.com/watch?v=uikbtpVZS2s&list=PLSE8ODhjZXjaKScG3l0nuOiDTTqpfnWFf&index=1)
* Class Agenda:
	* Course Logistics
	* Relational Model
	* Relational Algebra

### Vocabulary && Terms

* Databaseology - Logia de Banco de Dados
* Carnegie - Palavra própria mas lembrar
* Bribe - suborno
* Plagiarism - Plágio
* Linear Scan - escaneamento linear
* Ledger 
	* record of a business financial transaction - caderno de contabilidade
* Blockchain - Distributed ledger with growing list of records via cryptographic hash;
* Tight - Apertado
* Devised - concebeu
* Tenets - Principios
	* Tenets - Core believes != General Rules - Principles
* avoid the overhead - evitar sobrecarga
* Constraints - restrições
### Messy Notes
- Andy Pavlo enjoys to talk about databases
- Also the CMU is sponsored by Snowflake
	- Probably we're gonna learn about in a upcoming lesson
- People try to bribe him 
- Course overview
	- Design/Implementation of a DBMSs
- Projects
	- Start ASAP the [project zero](https://15445.courses.cs.cmu.edu/fall2022/project0/) and 
	- 2 weeks to finish it 
	- C++ 11
	- Build a Key-Value database
- Course Logistics
	- [Discord FTW](https://discord.gg/fD7BCSCg)
	- I can apply stuff being a outsider
- Databases
	- Organized Collection of inter-related data that models some aspect of the real-world;
	- Databases are the core compoments of most computer applications;
	- [Flat File Strawman](https://en.wikipedia.org/wiki/Flat-file_database) (Database)
		- Separated by comma/line (CSV)
		- One file per entity
		- The whole file needs to be loaded each time you want to read/update records
		- Flawless
			- Limited by memory
			- Hardcoded by indexes 
			- +1 step by parsing the data
		- Data Integrity
			- Subject: Artists and Musics
			- How do we ensure that the record 'related' is the same for each entry?
			- What if somebody overwrites the record with a invalid string?
			- What if there's multiple artists on an album?
		- Implementation
			- How to find a particular record?
			- What if we now want to create a new application that uses the same database?
			- What if two threads try to write to the same file at the same time?
				- The file locks every time that you stream it.
		- Durability
			- What if the machine crashes while our program is updating a record?
			- What if we want to replicate the database on multiple machines?
				- that's a problem
	- Database Management System
		- To avoid those many questions, you should USE or BUILD a DBMS.
		- The general purpose of a DBMS is to support creationg, querying, updating and administration of databases in accordance with some *data model*.
		- Data Models
			- Collection of concepts for describing a data in a database;
			- A *schema* is a description of a particular collection given a data model;
			- Available Data Models:
				- Most DBMS's
					- Relational
				- NoSQL
					- Key/Value
					- Graph
					- Document / Object
					- Wide-Column / Column-family
				- Machine Learning
					- Array / Matrix / Vectors
				- Obsolete
					- Hierarchical
					- Network
					- Multi-Value
		- Early DBMS's
			- Early database application were difficult to build and maintain on available DBMSs in the 1960s
			- Examples: IDS IMS CODASYL
			- Computers were expensive, humans were cheap;
			- Tight coupling between logical and physical layers;
			- Programmers had to know exactly what the application queries would execute before deploy the database;
			- Back in 1969, [Edgar Frank Codd](https://en.wikipedia.org/wiki/Edgar_F._Codd), a.k.a Ted Codd, devised the Relational Model.
		- Relational Model
			- Definition (by Pavlo)
				- The Relational model defines a database abstraction based on relations to avoid maintenance overhad.
			- Key tenets
				- Store database in simple data structures (relations)
				- Physical Storage left up to the DBMS implementation;
					- Can be up to the developer decide the model to implement like: tree, hash table, column or row store;
					- Radical idea back in 60's
				- Access data through high-level language, DBMS figures out the best executiton strategy;
					- Insted write prodecural code in Fortran, Cobol and among others to make direct calls to the Database API, use a high legel language to tell the system what you wanted to do for you
			- Three Pillars
				- **Structure**: The definition of thej database relation and their contents
				- **Integrity:** Ensure the Database contents safisfy constraints;
				- **Manipulation:** Programming interface for accessing and modifying a database's contents;
			- Relation Meaning (by **pavlo**):
				- A **relation** is an unordered set that contain the relationship of attributes that represent entities;
				- A **tuple** is a set of attribute values (also known as it **domain**) in the relation
					- Values are (normally) atomic/scalar
					- The special values **NULL** is a member of every domain (if allowed);
				- [N-ary Relation stuff](https://www.cs.odu.edu/~toida/nerzic/content/relation/definition/cp_gen/index.html):
					- ordered **n-tuple**: set of  *n* objects represented by x1 to xn 
					- $$ <_{x + 1},_{x + 2},_{x + n}> $$
					- cartesian product:  
						- A = Data
						- X = Tuple
						- A1 ... An -> Xn
						- X1 ... XN -> set of tuple
						- X belongs to A and for each item inside 
							- 1 < i < N
					- n-ary relation: 
						- subset of cartesian product. and a cartesian product is a subset of ordered n-tuples
						- basically a N-ary relation is a table with N columns
			- Primary Keys:
				- Artificial column: Identifier
				- A relation's primary key uniquely identifies a single tuple
				- Some databases automatically create an internal primary key if a table does not define one;
				- Auto-generation of unique integer primary keys:
					- SEQUENCE (SQL:2003)
					- AUTO_INCREMENT (MySQL)
			- Foreign Keys:
				- Specifies that an attribute from one relation has to map to a tuple in another relation
				- Responsible to know the cardinality between data: 1:1, 1:n, n:n
		- Data Manipulation Languages (DML)
			- Methods to store and retrieve information from Database
			- **Procedural (Relational Algebra):** The query specifies the (high-level) strategy to find the desired result based on sets / bags;
			- **Non-Procedural (Declarative and Relational Calculus):** The query specifies only what data is wanted and not how to find it.
		- **Relational Algebra**
			- Fundamental operations to retrieve and manipulate tuples in a relation. (based on set algebra).
			- Each operator takes one or more relations as its inputs and outputs a new relation.
				- We can "chain" operators together to create more complex operators
				* $$
					\leftarrow (left arrow)
					\sigma (sigma)
					\Pi (projection)
					\bowtie (inner join)
					\times (cross product)
					\cap (intersection)
					- (difference)
				$$
			* **SELECT:**
				* Choose a subset of the tuples from a relation that satisfies a selection predicate
					* Predicate acts as a filter to retain only tuples that fulfill its qualifying requirements;
					* Can combine multiple predicates using conjunctions /disjunctions;
					* Table songs: song_id, artist_id
					* Row: 1, 1
					* Row: 2, 1
					* Row: 3, 1
					* Row: 2, 5
						* $$\sigma_{predicate}(R)$$
						* $$ R(song\_id, artist\_id) $$ 
						* $$\sigma_{artist\_id='1'}(R)$$
						* $$ \sigma _{artist\_id='1' } \wedge _{song\_id='1' }(R) $$
						* ``SELECT * FROM songs WHERE song_id = 1 AND artist_id = 1``
