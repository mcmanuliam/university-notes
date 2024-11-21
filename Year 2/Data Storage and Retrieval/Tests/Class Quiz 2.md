[[Class-Quiz.pdf]]

---

**Question 1**: Following best practices for clarity of expression, provide the relational algebra for the query "What are the name and years of releases longer than 2 hours released by studio 'Universal'?

***In assuming Movies.Studio is a Foreign Key of Studio.Name***

$$LengthGreaterThan120:=\sigma_{(LengthMins > 120)}[Release]$$
$$Universal:=\sigma_{(Studio = Universal)}[Movies]$$$$Joined:=(LengthGreaterThan120 \bowtie_{(LengthGreaterThan120.MovieTitle=Universal.Title)} Universal)$$
$$Projected := \pi _{MovieTitle, Year} ( Joined )$$
---

**Question 2**: Provide the SQL statement for the query "List the studios that have released movies after 2011 that are longer than 3 hours.

```sql
SELECT Movies.Studio
FROM Release, Movies
WHERE Release.Year > 2011 AND Release.LengthMins > 180 AND Release.MovieTitle = Movies.Title
GROUP BY Movies.Studio
```

---

**Question 3**: In what order should you create the following tables? 

![[Pasted image 20241119151812.png]]

- Campus, since it's not dependent on anything else.
- Course, since it's only dependent on Campus
- Class since it's dependent on Course
- and finally Student since it's dependent on Class and Campus.

---

**Question 4**: When does the cardinality of a relation change during the development and lifetime of a relational database?

The cardinality is the number of rows in a relation, this will be an ever changing value as tuples are added and removed from the relation.

---

**Question 5**: Provide the schema to represent the following ER diagram and state any foreign key constraints

**Obsidian doesn't have any underline function so used PK to indicate Primary Key and FK to indicate Foreign Key.**

```
Customer (
	varchar(50) PK Email
	FK Order.number as order_number 
)

Order (
	int PK number
)
```