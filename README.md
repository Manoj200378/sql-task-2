use studentmanagement;
# Creating Students Table
   CREATE TABLE Students02 (
    student_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(151) UNIQUE NOT NULL
	);

# Assigning Values into students Table
INSERT INTO Students02 VALUES (1, 'sasi', 'sasi@gmail.com'); 
INSERT INTO Students02 VALUES (2, 'Kiran', 'Kiran@gmail.com');
INSERT INTO Students02 VALUES (3, 'Manoj', 'Manoj@gmail.com');
INSERT INTO Students02 VALUES (4, 'Rahul', 'Rahul@gmail.com');
INSERT INTO Students02 VALUES (5, 'Dawn', 'Dawn@gmail.com');
INSERT INTO Students02 VALUES (6, 'Nikhil', 'Nikhil@gmail.com');
INSERT INTO Students02 VALUES (7, 'Nitish', 'Nitish@gmail.com');
INSERT INTO Students02 VALUES (8, 'Rana', 'Rana@gmail.com');
INSERT INTO Students02 VALUES (9, 'Nitya', 'Nitya@gmail.com');
INSERT INTO Students02 VALUES (10, 'Mounika', 'jasmine@gmail.com');

#Creating Courses Table
CREATE TABLE Courses (
   Course_id INT PRIMARY KEY,
   Course_name VARCHAr (25) NOT NULL,
   Course_description TEXT
   );

# Assigning values into courses table
INSERT INTO Courses VALUES (100, 'Mathematics', 'NA');
INSERT INTO Courses VALUES (93, 'Biology', 'NA');
INSERT INTO Courses VALUES (83, 'English', 'NA');
INSERT INTO Courses VALUES (79, 'Hindi
', 'NA');

#Creating Enrolments table
CREATE TABLE Enrolments (
   Enrolment_id INT PRIMARY KEY,
   Student_id INT,
   Course_id INT,
   Enrolment_date DATE,
   FOREIGN KEY (student_id) REFERENCES Students(student_id),
   FOREIGN KEY (course_id) REFERENCES Courses(course_id)
   );

#Assigning values into Enrolments Table
INSERT INTO Enrolments VALUES (07, 1, 100, '2024-05-23');
INSERT INTO Enrolments VALUES (11, 1, 93, '2024-05-23');
INSERT INTO Enrolments VALUES (12, 2, 100, '2024-05-25');
INSERT INTO Enrolments VALUES (14, 3, 93, '2024-06-18');
INSERT INTO Enrolments VALUES (15, 4, 83, '2024-06-21');
INSERT INTO Enrolments VALUES (16, 5, 83, '2024-06-31');
INSERT INTO Enrolments VALUES (20, 6, 83, '2024-05-31');
INSERT INTO Enrolments VALUES (19, 6, 100, '2024-05-31');
INSERT INTO Enrolments VALUES (13, 7, 93, '2024-04-31');
INSERT INTO Enrolments VALUES (18, 8, 100, '2024-04-25');
INSERT INTO Enrolments VALUES (29, 9, 83, '2024-05-17');
INSERT INTO Enrolments VALUES (21, 10, 79, '2024-06-16');
INSERT INTO Enrolments VALUES (22, 10, 79, '2024-06-16');

# 1) List all students and the courses they are enrolled in
SELECT 
    Students.name AS student_name, 
    Courses.course_name AS course_name
FROM Enrolments
INNER JOIN Students ON Enrolments.student_id = Students.student_id
INNER JOIN Courses ON Enrolments.course_id = Courses.course_id;

# 2) Find the number of students enrolled in each course
SELECT 
    Courses.course_id, 
    Courses.course_name, 
    COUNT(Enrolments.student_id) AS num_enrolled_students
FROM Courses
LEFT JOIN Enrolments ON Courses.course_id = Enrolments.course_id
GROUP BY Courses.course_id, Courses.course_name;

# 3)  List students who have enrolled in more than one course.
SELECT 
    student_id, 
    COUNT(course_id) AS num_courses_enrolled
FROM Enrolments
GROUP BY student_id
HAVING COUNT(course_id) > 1;

# 4) Find courses with no enrolled students
SELECT 
    Courses.course_id, 
    Courses.course_name
FROM Courses
LEFT JOIN Enrolments ON Courses.course_id = Enrolments.course_id
WHERE Enrolments.enrolment_id IS NULL;
