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
	PK int staff_no,
	int responsibility_start,
	int responsibility_end,
)

Tutor(
	PK int staff_no,
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

Course(
	PK varchar(4) id,
	varchar(20) title,
)
```