# WEEK 7 OPPE Practice Question 5
## Problem Statement:
![download](https://user-images.githubusercontent.com/94922914/234215830-b06e741a-157f-4f45-8087-283e671023bd.png)</br>
Write a Python program to print the playground of the given team id. team_id is given in a file named 'team.txt' resides in the same folder as python program file.
- The output of the python program is only playground name.
- For example, if the team_id is 'T0002' . Then output must be Villa Park only
  
 ## Solution:
 ```python 
import sys
import os
import psycopg2

file = open("team.txt","r")
name=file.read()

try:
    connection = psycopg2.connect(database = sys.argv[1],
    user = os.environ.get('PGUSER') ,
    password = os.environ.get('PGPASSWORD') ,
    host = os.environ.get('PGHOST'),
    port = os.environ.get('PGPORT'))
    
    cursor=connection.cursor()
    query="select playground from teams where team_id='{}'".format(name)
    cursor.execute(query)
    result=cursor.fetchall()
    for res in result:
        print(res[0])
    cursor.close()
except(Exception,psycopg2.DatabaseError) as error:
    print(error)
finally:
    connection.close
```
