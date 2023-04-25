# WEEK 7 OPPE Practice Question 2 - Encoding Teams
## Problem Statement:
In this problem, you have to write a Python program to print an encoding of the ids of the teams whose jersey colour at home is different from the jersey colour when they play away from home.

- The encoding must be using a shift cipher, which is detailed below.
  - An alphabet is mapped to another alphabet as follows. For a given alphabet α, let pos be the position at which α occurs in the alphabet listing (A at 1, B at 2, …. Z at 26). Then the encoding of α is the alphabet at the position (pos + 7) mod 26.</br>
    For example, if M is the alphabet, then the position at which M occurs in the alphabet listing is 13. Then, the encoding of M is the alphabet at the position (13 + 7) mod 26 = 20, which is T. 
  - For each digit β, the encoding of β is (β+7) mod 10.</br>
    For example, if 3 is the digit, then the encoding of 3 is the number (3 + 7) mod 10 = 0.
- The ids should be listed in the ascending order before performing the encoding.
- Each line in the output of the program must correspond to one row retrieved from the table.
  
 ## Solution:
 ```python 
import sys
import os
import psycopg2

try:
    connection = psycopg2.connect(
        database = sys.argv[1],
        user = os.environ.get('PGUSER'),
        password = os.environ.get('PGPASSWORD'),
        host = os.environ.get('PGHOST'),
        port = os.environ.get('PGPORT'))
        
    cursor = connection.cursor()
    query = "select team_id from teams where jersey_home_color <> jersey_away_color"
    
    cursor.execute(query)
    
    result = cursor.fetchall()
    
    for res in result:
        new_res = chr(((ord(res[0][0])-65+7)%26)+65)
        for i in res[0][1:]:
            new_res += str((int(i)+7)%10)
        print(new_res)
        
    cursor.close()
except(Exception, psycopg2.DatabaseError) as error:
    print(error)
finally:
    connection.close
```
