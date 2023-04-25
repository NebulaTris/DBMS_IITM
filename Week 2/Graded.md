## Question 1
Write an SQL statement to find the match numbers of those matches in which the host team scored more (goals) than the guest team.</br>
Database: FLIS

### Solution:
```
select match_num
from matches
where host_team_score > guest_team_score;
```

## Question 2
Write an SQL statement to find the colors of the home-jersey and the away-jersey (jersey home color, jersey away color) used by the team: “All Stars”.</br>
Database: FLIS

### Solution:
```
select jersey_home_color, jersey_away_color
from teams
where name = ’All Stars’;
```
## Question 3
Write an SQL statement to find the names of players of the team: “All Stars”.</br>
Database: FLIS

### Solution:
```
select p.name
from players p, teams t
where p.team_id = t.team_id and t.name = ’All Stars’;
```
## Question 4
Write an SQL statement to find the first names and the last names (student fname,
student lname) of students who belong to the department with department code as
”MCA” and who were born after ’2002-06-15’.</br>
Database: LIS

### Solution:
```
select student_fname, student_lname
from students
where department_code = ’MCA’ and dob> ’2002-06-15’;
```
## Question 5
Write an SQL statement to find the first names and the last names of faculty (faculty fname, faculty lname) who belong to the department: ”Computer Science”.</br>
Database: LIS

### Solution:
```
select f.faculty_fname, f.faculty_lname
from faculty f, departments d
where f.department_code = d.department_code
and department_name = ‘Computer Science’;
```
