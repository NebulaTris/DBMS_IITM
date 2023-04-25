## Question 1
Write an SQL statement to find the name of the manager of the team: “All Stars”.</br>
Database: FLIS

### Solution:
```
select m.name
from managers m, teams t
where m.team_id = t.team_id and t.name = ’All Stars’
```

## Question 2
Write an SQL statement to find the names of all teams.</br>
Database: FLIS

### Solution:
```
select name from teams
```
## Question 3
Write an SQL statement to find the titles of books authored by an author having first
name as ”Joh Paul” and last name as ”Mueller”.</br>
Database: LIS

### Solution:
```
select c.title
from book_catalogue c, book_authors a
where c.isbn_no = a.isbn_no
and author_fname = ’Joh Paul’ and author_lname = ’Mueller’
```
## Question 4
Write an SQL statement to find the titles of books published by ”McGraw Hill Educa-
tion”.</br>
Database: LIS

### Solution:
```
select title
from book_catalogue
where publisher = ’McGraw Hill Education’
```
## Question 5
Write an SQL statement to display the first name and the last name of students (stu-
dent fname, student lname) pursuing ‘PG’ courses.</br>
Database: LIS

### Solution:
```
select student_fname, student_lname from students s, members m
where s.roll_no = m.roll_no and member_type = ’PG’
```
