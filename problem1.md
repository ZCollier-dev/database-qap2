Table Creation:

Create Students Table:

CREATE TABLE students (
id SERIAL PRIMARY KEY,
first_name TEXT,
last_name TEXT,
email TEXT,
school_enrollment_date DATE
)

Create Professors Table:

CREATE TABLE professors (
id SERIAL PRIMARY KEY,
first_name TEXT,
last_name TEXT,
department TEXT
)

Create Courses Table:

CREATE TABLE courses (
id SERIAL PRIMARY KEY,
course_name TEXT,
course_description TEXT,
professor_id INT REFERENCES professors(id)
)

Create Enrollments Table:

CREATE TABLE enrollments (
student_id INT REFERENCES students(id),
course_id INT REFERENCES courses(id),
enrollment_date DATE,
PRIMARY KEY (student_id, course_id)
)

Entry Insertion:

Insert data into Students table:

INSERT INTO students (first_name, last_name, email, school_enrollment_date)
VALUES
('Zachary', 'Collier', 'zacharycollier36@protonmail.com', '2024-04-15'),
('Cave', 'Johnson', 'cavejohnson@gmail.com', '2025-01-02'),
('John', 'Doe', 'johndoe@hotmail.com', '2023-05-07'),
('Beth', 'Walsh', 'bethwalsh@yahoo.ca', '2022-08-23'),
('Lauren', 'McDonald', 'laurenmcd@gmail.com', '2023-01-03')

SELECT \* FROM students;//to confirm proper insertion

Insert data into Professors table:

INSERT INTO professors (first_name, last_name, department)
VALUES
('Sanat', 'Mandal', 'Chemistry'),
('Matthew', 'Newman', 'Computer Science'),
('Jeremy', 'Willcott', 'Physics'),
('Joseph', 'Drew', 'Engineering')

Insert data into Courses table:

INSERT INTO courses (course_name, course_description, professor_id)
VALUES
('Chemistry 101', 'Introduction to Chemistry', 1),
('Physics 101', 'Introduction to Physics', 3),
('CompSci 101', 'Introduction to Computer Science', 2)

Insert data into Enrollments table:

INSERT INTO enrollments (student_id, course_id, enrollment_date)
VALUES
(1, 1, '2024-04-15'),
(1, 2, '2024-04-15'),
(3, 1, '2023-05-07'),
(4, 3, '2022-08-23'),
(5, 2, '2023-01-03')

Querying:

Select students enrolled in Physics 101:

SELECT students.first_name || ' ' || students.last_name AS student_full_name, courses.course_name
FROM students
JOIN enrollments ON students.id = enrollments.student_id
JOIN courses ON enrollments.course_id = courses.id
WHERE enrollments.course_id = 2

Find which courses have which professors:

SELECT courses.course_name, professors.first_name || ' ' || professors.last_name AS prof_full_name
FROM courses
JOIN professors ON professors.id = courses.professor_id

Find which courses have students enrolled in them:

SELECT DISTINCT courses.course_name
FROM courses
JOIN enrollments ON courses.id = enrollments.course_id

Update student email:

UPDATE students
SET email = 'lmcdonald@protonmail.com'
WHERE first_name = 'Lauren' AND last_name = 'McDonald'

Delete student:

DELETE FROM students
WHERE first_name = 'Cave' AND last_name = 'Johnson'
