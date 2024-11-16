In this coursework, you will create a database based on a model answer ER diagram for a scenario of the same structure as coursework 1, and then perform some queries on your database. There are four tasks to complete, listed below, including writing a report that should be submitted via Moodle.

#### Task 1
Starting from the coursework 2 model ER diagram provided on Moodle, create a relational database. To do this you should first convert the ER Diagram to a corresponding relational schema. For this task, you need only define the set of tables you need for the base relations and start relating them. Do not worry about populating or querying the database until this task is done.

```
Staff(
	PK int staff_no,
	varchar(30) name_firstname,
	varchar(40) name_surname,
	varchar(60) job_title,
	FK int Staff.staff_no as manager_no,
)

Lecturer(
	PK int Staff.staff_no as staff_no,
	int responsibility_start,
	int responsibility_end,
)

Tutor(
	PK int Staff.staff_no as staff_no,
	bool parttime,
)

Enrollment(
	PK FK int Student.ids as tudent_no,
	PK FK varchar(4) Course.id as course_id,
	int exam_mark,
	int practical_mark,
)

Student(
	PK int id,
	varchar(30) name_firstname,
	varchar(40) name_surname,
	varchar(60) email,
)

TutorialGroup(
	PK varchar(4) tutorial_number,
	varchar(5) room_numbers_tutorial_room,
	varchar(5) room_numbers_lab_room,
	PK FK varchar(4) Course.id as course_id,
)

Teaches(
	PK FK varchar(4) Course.id as course_id,
	PK int Staff.staff_no as staff_no,
)

TutorialMembership(
	PK FK varchar(4) Course.id as course_id,
	PK int Student.id as student_id,
	
)

Course(
	PK varchar(4) id,
	varchar(20) title,
)
```


#### Task 2
Populate your database with the supplied data. The data is available as individual .csv files (and pdf file) in the Coursework 2: Database Queries Report section of the Moodle page. 

You can enter the data into your database in one of two ways: 

(1) Import the data as text files into the table using the import facility (see 'Importing Data From Files). (2) Enter the data manually row by row in the Results grid view (see 'Importing Manually') 

**NB** – before you do either of these – you must check the following:

1. Your tables have the same number and type of attributes/fields as the tables in the text files/on the sheet 
2. The attribute/field names are in the same order 
3. The data types of the actual data and those that are in your tables match.

If any of the above does not match, then you can change your database OR the order of data in the text files. However, note that if you change the data then your queries might not produce the expected results, so **it is best to avoid changing the data if at all possible.** 

The order that you populate the tables is important: you should populate the entities BEFORE populating the weak entities or relationships, to ensure that foreign key constraints can be met – remember, the value inserted in a foreign key column MUST already exist in the referenced primary key. Plan ahead the order that you are going to import data into the tables.


#### Task 3

**Question 1**
```sql
SELECT `job_title`
FROM Staff
WHERE name_firstname="Stephen" AND name_surname="Brewster"
```

**Question 2**
```sql
SELECT `job_title`
FROM Staff
WHERE name_firstname="Stephen" AND name_surname="Brewster"
```

**Question 3**
```sql
SELECT `job_title`
FROM Staff
WHERE name_firstname="Stephen" AND name_surname="Brewster"
```

**Question 4**
```sql
SELECT `job_title`
FROM Staff
WHERE name_firstname="Stephen" AND name_surname="Brewster"
```

5
```sql
SELECT `job_title`
FROM Staff
WHERE name_firstname="Stephen" AND name_surname="Brewster"
```


#### Task 4
Produce a report (to be submitted in PDF format) detailing your database design, your queries and some reflections about how you built the database (including a critical reflection on your choice of DBMS, e.g. pros/cons, ease of use, documentation/tutorials etc).

Your report should include:

1. Y**our database design– (12 marks)**
	Provide the EER diagram (or similar) of your constructed database. (you can take a screenshot of the diagram in MySQL Workbench).


2. **Queries & Results - (9 marks)** 
	Provide the SQL and results for queries 1-9. You can copy in the text of the query, and the CSV or take a screenshot of the relevant part of MySQL Workbench. For each query, state what SQL design pattern you used for the query. 
	
	For queries 1-4 ONLY, also provide the relational algebra [don't worry about the ordering for query 3 for the relational algebra].


3. **Challenges & Reflections** - no more than 400 words (3 marks)

	(i) Summarise the main design and building process for constructing a database. Discuss why are ER diagram necessary in designing the database? And, why is the transition from conceptual to logical design important?
	
	(ii) Discuss the challenges you faced when constructing your database. What major problems did you have in carrying out the building and querying of the database, and how did you overcome them? Also, include a reflection on your choice of DBMS.
	
	(ii) Include with a brief reflection on your personal achievements in doing this work (in other words, what you now know that you didn't know before or what you can now do that you couldn't do before). Consider your achievements in terms of their importance and the level of effort you had to expend. If you still have particular difficulties (i.e. things you believe you should have achieved, but haven't (yet!)), identify them. This will be useful to you when revising.
