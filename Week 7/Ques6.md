# WEEK 7 OPPE Practice Question 6
## Problem Statement:
<img src="https://user-images.githubusercontent.com/94922914/234222018-540c48db-3a93-4ae0-955c-8f8e8f04a7a6.png" width="500"/></br>
Write a Python program to print the student's first name, the corresponding department name and the respective year of date of birth, if the year is even then print "Even" or else "Odd".
Student's first name is given in a file named 'name.txt' resides in the same folder as python program file.
The output of the python program is only student's first name, the corresponding department name and year of date of birth, if the year is even then "Even" or else "Odd".
- For example, 'Suman' and 'Computer Science' is the name and department name of the student. '2002' is the year he was born in. '2002' is even. Then, the final output will be Suman,Computer Science,Even only. Note: No spaces.
- For example, 'Vinod' and 'Electrical Engineering' is the name and department name of the student. '2003' is the year he was born in. '2003' is not even. Then, the final output will be Vinod,Electrical Engineering,Odd only. Note: No spaces.
  
 ## Solution:
 ```python 
import sys
import os
import psycopg2

file = open("name.txt","r")
name = file.read()

try:
    connection = psycopg2.connect(
        database = sys.argv[1],
        user = os.environ.get('PGUSER'),
        password = os.environ.get('PGPASSWORD'),
        host = os.environ.get('PGHOST'),
        port = os.environ.get('PGPORT'))
        
    cursor = connection.cursor()
    query ="select students.student_fname, departments.department_name, students.dob from students,departments where students.student_fname = '{}' and departments.department_code = students.department_code".format(name)
    cursor.execute(query)
    
    result = cursor.fetchall()
    
    for res in result:
        if res[2].year%2==0:
            print(res[0]+","+res[1]+","+"Even")
        else:
            print(res[0]+","+res[1]+","+"Odd")
    
    cursor.close()
except(Execption, psycopg2.DatabaseError) as error:
    print(error)
finally:
    connection.close
```
