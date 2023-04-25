## Question 1
Write an SQL statement to find the names of teams that have played more than 3
matches.</br>
Database: FLIS

### Solution:
```
select name from teams where team_id in
  (select team_id
  from ((select host_team_id as team_id, count(*) as c
  from matches
  group by host_team_id)
  union all
  (select guest_team_id as team_id, count(*) as c
  from matches
  group by guest_team_id)) as t1
  group by team_id having sum(c) > 3
  )
```

## Question 2
Write an SQL statement to find the first name, last name of the faculty of the department
having department code as ”ME” and who have issued at least one book, such that there
are no duplicate firstname-lastname pairs.</br>
Database: LIS

### Solution:
```
select distinct faculty_fname, faculty_lname
from faculty natural join members natural join book_issue
where faculty.department_code = ’ME’
```
## Question 3
Write an SQL statement to find the number of book-titles issued on 11th August 2021.</br>
Database: LIS

### Solution:
```
select count(title) from book_catalogue where isbn_no in
  (select isbn_no
  from book_issue a, book_copies b
  where a.accession_no=b.accession_no and
  a.doi=’2021-08-11’
  )
```
## Question 4
Write an SQL statement to find the names of faculty (faculty fname, faculty lname) who
did not issue any book.</br>
Database: LIS

### Solution:
```
select faculty_fname,faculty_lname
from faculty
where faculty.id not in
(select members.id from members natural join book_issue
where members.id is not null)
```
## Question 5
Write an SQL statement to find the unique book titles which are issued to “PG” students
but not to “UG” students.</br>
Database: LIS

### Solution:
```
select distinct(title) from
  book_catalogue natural join book_copies natural join
  book_issue natural join members
  where member_type = ’PG’
except
select distinct(title) from
  book_catalogue natural join book_copies natural join
  book_issue natural join members
  where member_type = ’UG’
```
