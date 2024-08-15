## Appointment

Started with running the basic nmap command: `nmap 10.129.2.83`. After that I added the `-sV-` and `-sC` options to get information about the discovered service. 

```
PORT   		STATE 	SERVICE 	VERSION
80/tcp 		open  	http    	Apache httpd 2.4.38 ((Debian))
|_http-title: Login
|_http-server-header: Apache/2.4.38 (Debian)
```

When navigating to the IP in the browser, there is a login page.
To get more information I used Dirbuster to scan for webfolders. First I gave the medium wordlist a go, but that would take hours to finish, so I decided to go for the small list found at `/usr/share/wordlists/dirbuster/`. The following folders where found:

```
/images/
/css/
/js/
/vendor/
/fonts/
```
No useful information was found, this is pretty basic for a website.

Next up is to try some basic username:password combinations in the login form:

```
admin:admin
guest:guest
user:user
root:root
administrator:password
```

None of these worked. Could try to brute force it, but it might set off a security warning.

Next up is trying to inject SQL in one of the fields (I didn't come up with this myself, but this is what the walktrough tells you to do). But still, I try to understand as much of it as I can. Below is the SQL code that is vulnerable for SQL injection.

```
<?php

mysql_connect("localhost", "db_username", "db_password"); # Connection to the SQL Database.

mysql_select_db("users"); # Database table where user information is stored.

$username=$_POST['username']; # User-specified username.
$password=$_POST['password']; #User-specified password.

$sql="SELECT * FROM users WHERE username='$username' AND password='$password'";
# Query for user/pass retrieval from the DB.

$result=mysql_query($sql);
# Performs query stored in $sql and stores it in $result.

$count=mysql_num_rows($result);
# Sets the $count variable to the number of rows stored in $result.

if ($count==1){
	# Checks if there's at least 1 result, and if yes:
	$_SESSION['username'] = $username; # Creates a session with the specified $username.
	$_SESSION['password'] = $password; # Creates a session with the specified $password.
	header("location:home.php"); # Redirect to homepage.
}

else { # If there's no singular result of a user/pass combination:
	header("location:login.php");
	# No redirection, as the login failed in the case the $count variable is not equal to 1, HTTP Response code 200 OK.
}

?>
```

This code is vulnerable because it directly uses the user input in the SQL statement. It doens't sanitize anything or forbids the use of special characters. This means using `admin'#` in the username field, that the password query is now commented out, because of the hashtag. The password input can now be anything, since it's commented out. 

Since there is 1 admin account, the `if` statement is activated, because the count equals 1. The session is now created and thus it was possible to login without a password. Ofcourse you would still have to guess the username, but there is a good chance at least one common username is present. 

## Screenshots

![login_page_appointment.png](..%2Fmedia%2Flogin_page_appointment.png)

![dirbuster_appointment.png](..%2Fmedia%2Fdirbuster_appointment.png)

![pwnd Appointment.png](..%2Fmedia%2Fpwnd%20Appointment.png)

## Quiz Questions

What does the acronym SQL stand for? 
- Strcutured Query Language

What is one of the most common type of SQL vulnerabilities?
- SQL Injection

What is the 2021 OWASP Top 10 classification for this vulnerability?
- A03:2021-Injection

What does Nmap report as the service and version that are running on port 80 of the target?
- Apache httpd 2.4.38 ((Debian)) 

What is the standard port used for the HTTPS protocol?
- 443

What is a folder called in web-application terminology? 
- Directory

What is the HTTP response code is given for 'Not Found' errors?
- 404

Gobuster is one tool used to brute force directories on a webserver. What switch do we use with Gobuster to specify we're looking to discover directories, and not subdomains?
- dir

What single character can be used to comment out the rest of a line in MySQL?
- `#`

If user input is not handled carefully, it could be interpreted as a comment. Use a comment to login as admin without knowing the password. What is the first word on the webpage returned?
- Congratulations

Root flag 
- e3d0796d002a446c0e622226f42e9672