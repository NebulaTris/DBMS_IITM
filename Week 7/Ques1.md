# WEEK 7 OPPE Practice Question 1 - Prime Jersey
## Problem Statement:
In this question, you have to write a Python program to print the names of the players and the team of each player of all those players whose jersey number is a prime number.
  1. The list should be ordered in reverse alphabetical order of player names. If two or more players have the same name, then further sorting should be done on the team name, again in reverse alphabetical order.
  2. The format of output is as given below:
  Name of the player, followed by a comma (,), then a space and then the team name.
  For example, if Arjun has jersey number 5 and is playing for All Stars and Pranav, with jersey number 7, is playing for team Amigos, then the output will be:
  Pranav, Amigos</br>
  Arjun, All Stars
  
 ## Solution:
 ```
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
    query = "select players.name, teams.name, players.jersey_no from teams, players where players.team_id = teams.team_id"
    
    cursor.execute(query)
    
    result = cursor.fetchall()
    
    def prime(n):
        if n<=1:
            return False
        for i in range(2,n):
            if n%i==0:
                return False
        return True
    final_res = []
    for res in result:
        if prime(res[2]):
            final_res.append(res[0]+", "+res[1])
            
    final_res.sort(reverse=True)
    
    for final in final_res:
        print(final)
    
    cursor.close()
except(Exception, psycopg2.DatabaseError) as error:
    print(error)
finally:
    connection.close
```
 
