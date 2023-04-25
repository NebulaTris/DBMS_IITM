# WEEK 7 OPPE Practice Question 4
## Problem Statement:
![download](https://user-images.githubusercontent.com/94922914/234214512-d731f81b-4e03-4ff1-b6e6-a718017f4d62.png)</br>
Write a Python program to print the roll number of the student. Student's first name is given in a file named 'name.txt' resides in the same folder as python program file.
The output of the python program is only roll number.  
For example, if the first name of the student is 'Vikas'. Then output must be CS01 only. Note: No spaces.
  
 ## Solution:
 ```python 
import sys
import os
import psycopg2

file = open("name.txt", "r")
name = file.read()
try:
    connection = psycopg2.connect(database = sys.argv[1],
    user = os.environ.get('PGUSER'), 
    password = os.environ.get('PGPASSWORD'), 
    host = os.environ.get('PGHOST'),
    port = os.environ.get('PGPORT'))
    
    cursor = connection.cursor()
    query="select roll_no from students where student_fname='{}'".format(name)
    cursor.execute(query)
    result= cursor.fetchall()
    
    for res in result:
        print(res[0])
except(Exception,psycopg2.DatabaseError) as error:
    print(error)
finally:
    connection.close
```
