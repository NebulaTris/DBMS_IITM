# WEEK 7 OPPE Practice Question 3
## Problem Statement:
![download](https://user-images.githubusercontent.com/94922914/234213788-27952b86-9674-4c37-b886-942dd1c464d5.png)</br>
Write a Python program to output the jersey number of the player. Player's name is given in a file named 'player.txt' resides in the same folder as python program file. 
The output of the python program is only jersey number.  
For example, if the jersey number of the player is 99. Then output must be 99 only. Note: No spaces.
  
 ## Solution:
 ```python 
import sys
import os
import psycopg2

file  = open("player.txt" , "r")
name = file.read()

try:
    connection = psycopg2.connect(database = sys.argv[1],
    user = os.environ.get('PGUSER') ,
    password = os.environ.get('PGPASSWORD') ,
    host = os.environ.get('PGHOST'),
    port = os.environ.get('PGPORT'))
    
    cursor = connection.cursor()
    query = "select jersey_no from players where name = '{}'".format(name)
    cursor.execute(query)
    result = cursor.fetchall()
    for res in result:
        print(res[0])
    cursor.close()
except(Exception, psycopg2.DatabaseError) as error:
    print(error)
finally:
    connection.close
```
