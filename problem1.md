Table Creation:

CREATE TABLE students (
	id SERIAL PRIMARY KEY,
	first_name TEXT,
	last_name TEXT,
	email TEXT,
	school_enrollment_date DATE
)

CREATE TABLE professors (
	id SERIAL PRIMARY KEY,
	first_name TEXT,
	last_name TEXT,
	department TEXT
)

CREATE TABLE courses (
	id SERIAL PRIMARY KEY,
	course_name TEXT,
	course_description TEXT,
	professor_id INT REFERENCES professors(id)
)

CREATE TABLE enrollments (
	student_id INT REFERENCES students(id),
	course_id INT REFERENCES courses(id),
	enrollment_date DATE,
	PRIMARY KEY (student_id, course_id)
)

Entry Insertion:

INSERT INTO students (first_name, last_name, email, school_enrollment_date)
VALUES
	('Zachary', 'Collier', 'zacharycollier36@protonmail.com', '2024-04-15'),
	('Cave', 'Johnson', 'cavejohnson@gmail.com', '2025-01-02'),
	('John', 'Doe', 'johndoe@hotmail.com', '2023-05-07'),
	('Beth', 'Walsh', 'bethwalsh@yahoo.ca', '2022-08-23'),
	('Lauren', 'McDonald', 'laurenmcd@gmail.com', '2023-01-03')

SELECT * FROM students;//to confirm proper insertion

INSERT INTO professors (first_name, last_name, department)
VALUES
	('Sanat', 'Mandal', 'Chemistry'),
	('Matthew', 'Newman', 'Computer Science'),
	('Jeremy', 'Willcott', 'Physics'),
	('Joseph', 'Drew', 'Engineering')

INSERT INTO courses (course_name, course_description, professor_id)
VALUES
	('Chemistry 101', 'Introduction to Chemistry', 1),
	('Physics 101', 'Introduction to Physics', 3),
	('CompSci 101', 'Introduction to Computer Science', 2)

INSERT INTO enrollments (student_id, course_id, enrollment_date)
VALUES
	(1, 1, '2024-04-15'),
	(1, 2, '2024-04-15'),
	(3, 1, '2023-05-07'),
	(4, 3, '2022-08-23'),
	(5, 2, '2023-01-03')

Querying:

SELECT students.first_name || ' ' || students.last_name AS student_full_name, courses.course_name
FROM students
JOIN enrollments ON students.id = enrollments.student_id
JOIN courses ON enrollments.course_id = courses.id
WHERE enrollments.course_id = 2

SELECT courses.course_name, professors.first_name || ' ' || professors.last_name AS prof_full_name
FROM courses
JOIN professors ON professors.id = courses.professor_id

SELECT DISTINCT courses.course_name
FROM courses
JOIN enrollments ON courses.id = enrollments.course_id

Update:

UPDATE students
SET email = 'lmcdonald@protonmail.com'
WHERE first_name = 'Lauren' AND last_name = 'McDonald'

Delete:

DELETE FROM students
WHERE first_name = 'Cave' AND last_name = 'Johnson'
