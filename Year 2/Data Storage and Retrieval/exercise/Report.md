### 1. Your Database Design - (12 marks)
Provide the EER diagram (or similar) of your constructed database. (you can take a screenshot of the diagram in MySQL Workbench).

![[Pasted image 20241114193739.png]]

***Had to download SQL Workbench for this one, had a real rough time.***

---
### 2. Queries & Results - (9 marks)

Provide the SQL and results for queries 1-9. You can copy in the text of the query, and the CSV or take a screenshot of the relevant part of MySQL Workbench. For each query, state what SQL design pattern you used for the query.

For queries 1-4 ONLY, also provide the relational algebra (don't worry about the ordering for query 3 for the relational algebra):
##### Questions:
**Question 1**: Find the job title (i.e., lecturer, professor, etc.) of staff member Stephen Brewster.
- ***Basic***

```sql
SELECT `job_title`
FROM Staff
WHERE name_firstname="Stephen" AND name_surname="Brewster"
```

$$Filtered := \sigma((namefirstname=Stephen \cap namesurname=Brewster)[Staff])$$
$$Project:=\pi _{jobtitle} (Filtered)$$

![[Pasted image 20241114150603.png]]

---

**Question 2**: Find the exam results for all students apprentices taking CS-1Q. 
- ***Equi-Join***

```sql
SELECT `exam_mark`
FROM Enrollment, Course
WHERE Enrollment.course_id=Course.id AND Course.title="CS-1Q"
```

$$Filtered := \sigma _{(title=CS-1Q)}[Course]$$
$$Joined := (Filtered \bowtie _{(courseid=id)}Enrollment)$$
$$Project:=\pi _{exammark} (Joined)$$

![[Pasted image 20241114150637.png]]

---

**Question 3**: Show the results of query 2 with the students' apprentices' names, and order the results in ascending order alphabetically by surname.
- ***Equi-Join***

```sql
SELECT `name_firstname`, `name_surname`, `exam_mark`
FROM Enrollment, Course, Student

WHERE Enrollment.course_id=Course.id 
	AND Enrollment.student_id=Student.id 
	AND Course.title="CS-1Q"

ORDER BY Student.name_firstname, Student.name_surname ASC
```

$$Filtered := \sigma _{(title=CS-1Q)}[Course]$$
$$SemiJoined := (Filtered \bowtie _{(courseid=id)}Enrollment)$$
$$Joined := (SemiJoined \bowtie _{(studentid=id)}Student)$$
$$Project:=\pi _{exammark, namefirstname, namesurname} (Joined)$$

![[Pasted image 20241114150716.png]]

---

**Question 4**: Find the names of all staff lecturing on 'CS-1Q' who are also professors.
- ***Equi-Join***

```sql
SELECT `name_firstname`, `name_surname`
FROM Teaches, Course, Staff

WHERE Teaches.course_id=Course.id 
	AND Teaches.staff_no=Staff.staff_no
	AND Course.title="CS-1Q"
	AND Staff.job_title="professor"
```

$$FilteredCourse:= \sigma _{(title=CS-1Q)}[Course]$$
$$FilteredStaff:= \sigma _{(jobtitle=professor)}[Staff]$$
$$SemiJoined := (FilteredCourse\bowtie _{(courseid=id)}Teaches)$$
$$Joined := (SemiJoined\bowtie _{(staffno=staffno)}FilteredStaff)$$
$$Project := \pi _{namefirstname, namesurname}(Joined)$$

![[Pasted image 20241114150748.png]]

---

**Question 5**: Find the number of staff members of each job title (Hint: consider the Grouping design pattern).
- ***Group-by***

```sql
SELECT `job_title`, COUNT(*) as `count`
FROM Staff
GROUP BY `job_title`
```

![[Pasted image 20241114150828.png]]

---

**Question 6**: Find the names of tutors who are not lecturers and whose tutorial group meets in room 11. 
- ***Equi-Join***

***Hint:*** 
	***(1) Create a query to select the tutors whose group meets in room 11 and then*** 
	***(2) extend the first query using the join pattern with the Staff table.)***

```sql
SELECT `name_firstname`, `name_surname`
FROM `Tutorial Group`, Staff

WHERE Staff.staff_no=`Tutorial Group`.tutor
	AND `Tutorial Group`.room_numbers_tutorial_room = 11
	AND NOT Staff.job_title = 'lecturer'
```

![[Pasted image 20241114150858.png]]

---

**Question 7**: For each assessed student, display their student ID and their average exam and practical marks.
- ***Group-by***

```sql
SELECT Student.id, 
	AVG(Enrollment.exam_mark) as `avg_exam_mark`, 
	AVG(Enrollment.practical_mark) as `avg_practical_mark`
 
FROM Student, Enrollment

WHERE Enrollment.student_id = Student.id
GROUP BY Student.id
```

![[Pasted image 20241114151959.png]]

---

**Question 8**: Show the results of query 7 with the students' names, but only for those with the surname 'Smith' or 'Saunders'.
- ***Group-by***

```sql
SELECT Student.id,
	Student.name_firstname, 
	Student.name_surname,
	AVG(Enrollment.exam_mark) as `avg_exam_mark`, 
  AVG(Enrollment.practical_mark) as `avg_practical_mark`
 
FROM Student, Enrollment

WHERE Enrollment.student_id = Student.id
	AND (Student.name_surname = "Smith"
  OR Student.name_surname = "Saunders")

GROUP BY Student.id
```

![[Pasted image 20241114152023.png]]

---

**Question 9**: Find the names of staff who manage themselves.
- ***Basic***

```sql
SELECT Staff.name_firstname, Staff.name_surname
FROM Staff
WHERE Staff.staff_no = Staff.manager_no
```

![[Pasted image 20241114152123.png]]

---

### 3. Challenges & Reflections - (3 marks)

(i) Summaries the main design and building process for constructing a database. Discuss why are ER diagram necessary in designing the database? And, why is the transition from conceptual to logical design important? - 

(ii) Discuss the challenges you faced when constructing your database. What major problems did you have in carrying out the building and querying of the database, and how did you overcome them? Also, include a reflection on your choice of DBMS - 

(iii) Include with a brief reflection on your personal achievements in doing this work (in other words, what you now know that you didn't know before or what you can now do that you couldn't do before). Consider your achievements in terms of their importance and the level of effort you had to expend. If you still have particular difficulties (i.e. things you believe you should have achieved, but haven't (yet!)), identify them. This will be useful to you when revising -

---

The main process for designing and building a database involves:
- Requirements Gathering
- Creating a design
- Creating a schema based off a design
- Building the physical database.

ER diagrams are essential as they help map out entities, attributes and relationships giving you a clear idea of the blueprint before jumping to implementation.

Transitioning from conceptual to logical design is an important stage as it refines the structure, specifying data types, primary and foreign keys, and relationships in a format ready for the DBMS. This step ensures that the design is practical and can be implemented accurately in the database system.

 When constructing the database, I didn't struggle too much, there were some initial challenges in familiarizing myself with the software. I chose to use Beekeeper as my DBMS and found it really user-friendly overall. Setting up tables initially posed a few issues, mainly with understanding how the software's interface worked for defining schema and relationships. However, Beekeeper made it incredibly easy to run SQL scripts, so whenever I ran into limitations with the UI, I could quickly get around it by executing `ALTER TABLE` queries directly.

Reflecting on my choice of Beekeeper as a DBMS, I think it was beneficial in terms of usability and speed for a project of this scale. I imagine other DBMS options like SQL Workbench might have offered more advanced features for schema management, but due to this being quite a simple project Beekeeper provided a solid balance for learning and practical application.

I'm realising now I've gained a much more structured approach to **SQL** through this exercise. I've only worked with SQL in small, personal projects using SQLite, which often became a horrible mess to maintain. Now, I've developed a much better understanding of setting up SQL in a more professional, scalable way, including:

- Hosting a database on Docker
- Designing effective Entity Relationships
- Creating a schema and handling relationships properly
- Implementing the schema with industry-standard tools
- Inserting pre-existing data from a file
- Performing basic SQL queries

While I found the SQL syntax itself straightforward, I can see now that understanding the theory behind relational databases—especially relational algebra—could be a massively helpful going forward thinking deeper about databases. 
