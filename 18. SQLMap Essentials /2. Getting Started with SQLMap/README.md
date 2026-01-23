<h3>Getting Started with SQLMap</h3>

Upon starting using SQLMap, the first stop for new users is usually the program's help message. To help new users, there are two levels of help message listing:

Basic Listing shows only the basic options and switches, sufficient in most cases (switch -h):

@htb[/htb]$ sqlmap -h

Advanced Listing shows all options and switches (switch -hh):

 sqlmap -hh

 For more details, users are advised to consult the project's wiki, as it represents the official manual for SQLMap's usage.

<h3>Basic Scenario</h3>

In a simple scenario, a penetration tester accesses the web page that accepts user input via a GET parameter (e.g., id). They then want to test if the web page is affected by the SQL injection vulnerability. If so, they would want to exploit it, retrieve as much information as possible from the back-end database, or even try to access the underlying file system and execute OS commands. An example SQLi vulnerable PHP code for this scenario would look as follows:

$link = mysqli_connect($host, $username, $password, $database, 3306);

$sql = "SELECT * FROM users WHERE id = " . $_GET["id"] . " LIMIT 0, 1";

$result = mysqli_query($link, $sql);

if (!$result)

    die("<b>SQL error:</b> ". mysqli_error($link) . "<br>\n");

As error reporting is enabled for the vulnerable SQL query, there will be a database error returned as part of the web-server response in case of any SQL query execution problems. Such cases ease the process of SQLi detection, especially in case of manual parameter value tampering, as the resulting errors are easily recognized:

<img width="683" height="317" alt="image" src="https://github.com/user-attachments/assets/32d6abbb-04b2-4d6f-b8f6-bb3941c19089" />

To run SQLMap against this example, located at the example URL http://www.example.com/vuln.php?id=1, would look like the following:

@htb[/htb]$ sqlmap -u "http://www.example.com/vuln.php?id=1" --batch

Note: in this case, option '-u' is used to provide the target URL, while the switch '--batch' is used for skipping any required user-input, by automatically choosing using the default option.

