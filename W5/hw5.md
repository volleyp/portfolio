# SQL

First we are going to establish a aconnection to the sql data base **user_action.db**. a connection in our case is a communication link between a Python program and a database server. When we are connecting to a database using the **sqlite3** module we are establishing a connection to the database server. This connection allows you to send SQL queries to the database and retrieve the results. We are opening and closing the connection. The reason for closing the connection after we are done using it is to free up resources.


Note that the code will be written in SQL but for displaying the dataframes we will read the SQL querys using pandas.


```python
import sqlite3 as sql
import pandas as pd
import numpy as np

```


```python
database = 'user_actions.db'

connection = sql.connect(database) #establish connection

query = "SELECT * FROM user_actions;" #creating a query

df = pd.read_sql_query(query, connection) #reading query using pandas
 
connection.close() #closing connection

```


```python

pd.set_option('display.max_rows', None) #analyze the data briefly
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>user_id</th>
      <th>username</th>
      <th>email</th>
      <th>action</th>
      <th>timestamp</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>34</td>
      <td>user34</td>
      <td>user34@email.com</td>
      <td>signup</td>
      <td>2015-02-04 14:38:47</td>
    </tr>
    <tr>
      <th>1</th>
      <td>28</td>
      <td>user28</td>
      <td>user28@email.com</td>
      <td>signup</td>
      <td>2015-03-09 11:55:33</td>
    </tr>
    <tr>
      <th>2</th>
      <td>27</td>
      <td>user27</td>
      <td>user27@email.com</td>
      <td>login</td>
      <td>2015-04-17 14:48:31</td>
    </tr>
    <tr>
      <th>3</th>
      <td>27</td>
      <td>user27</td>
      <td>user27@email.com</td>
      <td>login</td>
      <td>2015-04-21 13:22:14</td>
    </tr>
    <tr>
      <th>4</th>
      <td>27</td>
      <td>user27</td>
      <td>user27@email.com</td>
      <td>reset_password</td>
      <td>2015-04-25 16:30:15</td>
    </tr>
  </tbody>
</table>
</div>



## Task 1

Now we want to retrieve the usernames of all users who have performed the "signup" action.


```python
connection = sql.connect('user_actions.db') #open the connection

query = "SELECT username FROM user_actions WHERE action = 'signup'" # sql query to retrieve usernames for signup 

users_signup = connection.execute(query).fetchall() #interactiong adn retrieveng the data based on the query

connection.close() #close the connection

```


```python
print("usersthat signed up: ", users_signup)
```

    usersthat signed up:  [('user34',), ('user28',), ('user1',), ('user24',), ('user15',), ('user20',), ('user18',), ('user25',), ('user3',), ('user9',), ('user27',), ('user16',), ('user17',), ('user4',), ('user8',), ('user13',), ('user19',), ('user31',), ('user10',), ('user23',), ('user11',), ('user33',), ('user12',), ('user29',), ('user21',), ('user6',), ('user14',), ('user30',), ('user7',), ('user26',), ('user22',), ('user5',), ('user35',), ('user2',), ('user32',)]
    

## Task 2

Let us now find the total number of log entries for each user. Display the user_id, username, and the count of log entries.
Log entries are some kind of activity that a user does. In our case we have **login, signup, reset_password**. So we want to find the total numbers of such activities for each user. Lets do that using SQL.

We will use "SELECT" for the user_id and username with function COUNT(*) AS log_entry_count FROM user_actions.
This will count the number of each combination of log_entries for each user. We will then use GROUP BY to simply group the data by the columns that we spesify. We will then have a new datatable with userid, username, total number of log entrys.


```python
connection = sql.connect('user_actions.db')

# Once again create a query based on our conditions
query = """
    SELECT user_id, username, COUNT(*) AS log_entry_count
    FROM user_actions
    GROUP BY user_id, username;
"""
results = connection.execute(query).fetchall()
df_log_entrys = pd.read_sql_query(query, connection)
# Display the results
for row in results:
    print(row)

# Close the connection
connection.close()
```

    (1, 'user1', 104)
    (2, 'user2', 149)
    (3, 'user3', 108)
    (4, 'user4', 436)
    (5, 'user5', 192)
    (6, 'user6', 457)
    (7, 'user7', 362)
    (8, 'user8', 329)
    (9, 'user9', 118)
    (10, 'user10', 170)
    (11, 'user11', 328)
    (12, 'user12', 209)
    (13, 'user13', 470)
    (14, 'user14', 320)
    (15, 'user15', 35)
    (16, 'user16', 379)
    (17, 'user17', 367)
    (18, 'user18', 122)
    (19, 'user19', 58)
    (20, 'user20', 362)
    (21, 'user21', 323)
    (22, 'user22', 275)
    (23, 'user23', 309)
    (24, 'user24', 162)
    (25, 'user25', 136)
    (26, 'user26', 217)
    (27, 'user27', 211)
    (28, 'user28', 91)
    (29, 'user29', 49)
    (30, 'user30', 165)
    (31, 'user31', 389)
    (32, 'user32', 32)
    (33, 'user33', 32)
    (34, 'user34', 180)
    (35, 'user35', 394)
    


```python

```

## Task 3

Now, our goal is to identify users who have both logged in (action = 'login') and signed up (action = 'signup') on the same day. Display the user_id and username. To approach this we will use a self join where we will filter so that we will only choose those members whose dates match.


```python
connection = sql.connect('user_actions.db') # connect



#Here we define the query based on conditionsin hte task
query = """SELECT a.user_id, a.username FROM user_actions a 
JOIN user_actions b ON a.user_id = b.user_id
    WHERE a.action = 'login' AND b.action = 'signup' AND DATE(a.timestamp) = DATE(b.timestamp);"""

df2 = pd.read_sql_query(query, connection) #display the query


# Close the connection
connection.close()
```


```python
df2
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>user_id</th>
      <th>username</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>8</td>
      <td>user8</td>
    </tr>
    <tr>
      <th>1</th>
      <td>12</td>
      <td>user12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>30</td>
      <td>user30</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7</td>
      <td>user7</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>user22</td>
    </tr>
    <tr>
      <th>5</th>
      <td>22</td>
      <td>user22</td>
    </tr>
    <tr>
      <th>6</th>
      <td>5</td>
      <td>user5</td>
    </tr>
    <tr>
      <th>7</th>
      <td>5</td>
      <td>user5</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2</td>
      <td>user2</td>
    </tr>
    <tr>
      <th>9</th>
      <td>32</td>
      <td>user32</td>
    </tr>
  </tbody>
</table>
</div>



# Regex

The file comments.txt in the data repo contains lines of text, each representing a user comment. Users sometimes include tags in their comments using the format "#tag". Analyse the file and solve the following tasks.

## Task 1

Write a regular expression to extract all hashtags from a given comment. For example, applying the regex to comment 1 should return ["#programming", "#tips"]. Let us first import the textfile and read the lines as **comments** . We will then be able to access a given comment by **comment[n]** for n = 0,1,...,n+1 which will give us comment 1,2,...,n. We will then search for words that contians a hashtag that is followed by any word. For that we will use **findall** function which will give us all the substrings that contains certain pattern ( in our case the regular expression **r'#\w+'**) which means that we looking for a hashtag followed by any word with any letter size. Lets write our code and try apply it to the first comment.


```python
import re
```


```python
with open('comments.txt', 'r') as t:
    comments = t.readlines() # comments stores all the lines from the textfile
hashtags = re.findall(r'#\w+', comments[0]) # comments[n] for n = 0,1,2,..n+1 is comment 1,2,...,n 

hashtags

```




    ['#programming', '#tips']



## Task 2

Create a regular expression to find comments that mention both "#programming" and "#python". Apply the regex to comment 2 and check if it matches. 

We want to first create a regex object with **re.compile** . The pattern here will be #programming followed by any word and then #python or vice versa. The advantage of using compile is that we maybe want to use the same pattern several times ( for different comments for instance). We want then to search for this regex object that we created , for that we will use the **search** function. Lastly we will check if it match or dont match 


```python
comment_2 = comments[1] #creating a second comment 
expression = re.compile(r'#programming.*#python|#python.*#programming') #creating the regex with desired condition
match_or_not = expression.search(comment_2) # searching for the regesx that we created

if match_or_not:
    print("Match")
else:
    print("Dont match")
```

    Dont match
    



We can now use the same function for checking some other comment just to see that it works properly. From the all comments
we could see that comment 6 indeed had both "programming" and "python" in it. So our function is supposed to give us a match.
Lets test that.


```python
comment_6 = comments[5]
match_or_not = expression.search(comment_6)

if match_or_not:
    print("Match")
else:
    print("Dont match")
```

    Match
    

# Task 3

Using your regular expression, extract all unique hashtags from the entire text file. (*)

Now the logic in this task will be following. We will first write a regulate expression  for finding hashtags. We will then creaty an empty list and for each hashtag in the data we will append that list with one. After that we will filter the list in such a way so that it doesnt cointains duplicates. In that way we will get all the unique hashtags.


```python
expression2 = re.compile(r'#\w+') #we compile hashtag followed by a word


all_hashtags = [] #create a list where we will store the hashtags

for comment in comments: # for each comment in comments
    hashtags = expression2.findall(comment) # apply our regEx and find them all :D
    all_hashtags.extend(hashtags) #Appends every hashtag to the all_hashtags list

unique_hashtags = set(all_hashtags) #Remove duplicated

print(unique_hashtags) # print
```

    {'#tech', '#research', '#python', '#analysis', '#data', '#innovation', '#tips', '#analytics', '#coding', '#insights', '#programming'}
    


```python
!jupyter nbconvert --to markdown hw5.ipynb
```

    [NbConvertApp] Converting notebook hw5.ipynb to markdown
    [NbConvertApp] Writing 9587 bytes to hw5.md
    


```python

```
