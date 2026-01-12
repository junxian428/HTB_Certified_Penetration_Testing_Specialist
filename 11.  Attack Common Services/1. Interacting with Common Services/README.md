<h3>Interacting with Common Services</h3>

Vulnerabilities are commonly discovered by people who use and understand technology, a protocol, or a service. As we evolve in this field, we will find different services to interact with, and we will need to evolve and learn new technology constantly.

To be successful at attacking a service, we need to know its purpose, how to interact with it, what tools we can use, and what we can do with it. This section will focus on common services and how we can interact with them.

<h3>File Share Services</h3>

A file sharing service is a type of service that provides, mediates, and monitors the transfer of computer files. Years ago, businesses commonly used only internal services for file sharing, such as SMB, NFS, FTP, TFTP, SFTP, but as cloud adoption grows, most companies now also have third-party cloud services such as Dropbox, Google Drive, OneDrive, SharePoint, or other forms of file storage such as AWS S3, Azure Blob Storage, or Google Cloud Storage. We will be exposed to a mixture of internal and external file-sharing services, and we need to be familiar with them.

This section will focus on internal services, but this may apply to cloud storage synced locally to servers and workstations.

<h3>Server Message Block (SMB)</h3>

SMB is commonly used in Windows networks, and we will often find share folders in a Windows network. We can interact with SMB using the GUI, CLI, or tools. Let us cover some common ways of interacting with SMB using Windows & Linux.

<h3>Windows</h3>

There are different ways we can interact with a shared folder using Windows, and we will explore a couple of them. On Windows GUI, we can press [WINKEY] + [R] to open the Run dialog box and type the file share location, e.g.: \\192.168.220.129\Finance\

<img width="733" height="412" alt="image" src="https://github.com/user-attachments/assets/6b9fca71-727d-47e1-87e9-5c8bfccea295" />

Suppose the shared folder allows anonymous authentication, or we are authenticated with a user who has privilege over that shared folder. In that case, we will not receive any form of authentication request, and it will display the content of the shared folder.

<img width="735" height="414" alt="image" src="https://github.com/user-attachments/assets/9fc11e28-5ef5-4a02-b9ce-0970009bca37" />

If we do not have access, we will receive an authentication request.

<img width="741" height="413" alt="image" src="https://github.com/user-attachments/assets/3f3332c1-c97b-42fb-bd2e-06f6395f0f4b" />

Windows has two command-line shells: the Command shell and PowerShell. Each shell is a software program that provides direct communication between us and the operating system or application, providing an environment to automate IT operations.

Let's discuss some commands to interact with file share using Command Shell (CMD) and PowerShell. The command dir displays a list of a directory's files and subdirectories.

<h3>Windows CMD - DIR</h3>

C:\htb> dir \\192.168.220.129\Finance\

The command net use connects a computer to or disconnects a computer from a shared resource or displays information about computer connections. We can connect to a file share with the following command and map its content to the drive letter n.

<h3>Windows CMD - Net Use</h3>

C:\htb> net use n: \\192.168.220.129\Finance

We can also provide a username and password to authenticate to the share.

C:\htb> net use n: \\192.168.220.129\Finance /user:plaintext Password123

With the shared folder mapped as the n drive, we can execute Windows commands as if this shared folder is on our local computer. Let's find how many files the shared folder and its subdirectories contain.

<h3>Windows CMD - DIR</h3>

C:\htb> dir n: /a-d /s /b | find /c ":\"

29302

We found 29,302 files. Let's walk through the command:

dir n: /a-d /s /b | find /c ":\"

<table border="1" cellpadding="6" cellspacing="0">
  <thead>
    <tr>
      <th>Syntax</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>dir</td>
      <td>Application (lists files and folders)</td>
    </tr>
    <tr>
      <td>n:</td>
      <td>Directory or drive to search</td>
    </tr>
    <tr>
      <td>/a-d</td>
      <td><code>/a</code> is the attribute filter, <code>-d</code> means exclude directories (show files only)</td>
    </tr>
    <tr>
      <td>/s</td>
      <td>Displays files in the specified directory and all subdirectories</td>
    </tr>
    <tr>
      <td>/b</td>
      <td>Uses bare format (no heading information or summary)</td>
    </tr>
  </tbody>
</table>

The following command | find /c ":\\" process the output of dir n: /a-d /s /b to count how many files exist in the directory and subdirectories. You can use dir /? to see the full help. Searching through 29,302 files is time consuming, scripting and command line utilities can help us speed up the search. With dir we can search for specific names in files such as:


- cred

- password

- users

- secrets

- key

- Common File Extensions for source code such as: .cs, .c, .go, .java, .php, .asp, .aspx, .html.

C:\htb>dir n:\*cred* /s /b

n:\Contracts\private\credentials.txt


C:\htb>dir n:\*secret* /s /b

n:\Contracts\private\secret.txt

We can find more findstr examples here.

<h3>Windows PowerShell</h3>

PowerShell was designed to extend the capabilities of the Command shell to run PowerShell commands called cmdlets. Cmdlets are similar to Windows commands but provide a more extensible scripting language. We can run both Windows commands and PowerShell cmdlets in PowerShell, but the Command shell can only run Windows commands and not PowerShell cmdlets. Let's replicate the same commands now using Powershell.

<h3>Windows PowerShell</h3>

PS C:\htb> Get-ChildItem \\192.168.220.129\Finance\

Instead of net use, we can use New-PSDrive in PowerShell.

PS C:\htb> New-PSDrive -Name "N" -Root "\\192.168.220.129\Finance" -PSProvider "FileSystem"

To provide a username and password with Powershell, we need to create a PSCredential object. It offers a centralized way to manage usernames, passwords, and credentials.

<h3>Windows PowerShell - PSCredential Object</h3>

PS C:\htb> $username = 'plaintext'

PS C:\htb> $password = 'Password123'

PS C:\htb> $secpassword = ConvertTo-SecureString $password -AsPlainText -Force

PS C:\htb> $cred = New-Object System.Management.Automation.PSCredential $username, $secpassword

PS C:\htb> New-PSDrive -Name "N" -Root "\\192.168.220.129\Finance" -PSProvider "FileSystem" -Credential $cred

Name           Used (GB)     Free (GB) Provider      Root      

CurrentLocation

----           ---------     --------- --------      ----       
---------------

N                                      FileSystem    \\192.168.220.129\Finance

In PowerShell, we can use the command Get-ChildItem or the short variant gci instead of the command dir.

<h3>Windows PowerShell - GCI</h3>

PS C:\htb> N:

PS N:\> (Get-ChildItem -File -Recurse | Measure-Object).Count

29302

We can use the property -Include to find specific items from the directory specified by the Path parameter.

PS C:\htb> Get-ChildItem -Recurse -Path N:\ -Include *cred* -File

The Select-String cmdlet uses regular expression matching to search for text patterns in input strings and files. We can use Select-String similar to grep in UNIX or findstr.exe in Windows.

<h3>Windows PowerShell - Select-String</h3>

PS C:\htb> Get-ChildItem -Recurse -Path N:\ | Select-String "cred" -List

N:\Contracts\private\secret.txt:1:file with all credentials

N:\Contracts\private\credentials.txt:1:admin:SecureCredentials!

CLI enables IT operations to automate routine tasks like user account management, nightly backups, or interaction with many files. We can perform operations more efficiently by using scripts than the user interface or GUI.

<h3>Linux</h3>

Linux (UNIX) machines can also be used to browse and mount SMB shares. Note that this can be done whether the target server is a Windows machine or a Samba server. Even though some Linux distributions support a GUI, we will focus on Linux command-line utilities and tools to interact with SMB. Let's cover how to mount SMB shares to interact with directories and files locally.

<h3>Linux - Mount</h3>

@htb[/htb]$ sudo mkdir /mnt/Finance

@htb[/htb]$ sudo mount -t cifs -o username=plaintext,password=Password123,domain=. //192.168.220.129/Finance /mnt/Finance

As an alternative, we can use a credential file.

@htb[/htb]$ mount -t cifs //192.168.220.129/Finance /mnt/Finance -o credentials=/path/credentialfile

The file credentialfile has to be structured like this:

<h3>CredentialFile</h3>

username=plaintext

password=Password123

domain=.

Note: We need to install cifs-utils to connect to an SMB share folder. To install it we can execute from the command line sudo apt install cifs-utils.

Once a shared folder is mounted, you can use common Linux tools such as find or grep to interact with the file structure. Let's hunt for a filename that contains the string cred:

<h3>Linux - Find</h3>

@htb[/htb]$ find /mnt/Finance/ -name *cred*

/mnt/Finance/Contracts/private/credentials.txt

Next, let's find files that contain the string cred:

@htb[/htb]$ grep -rn /mnt/Finance/ -ie cred

/mnt/Finance/Contracts/private/credentials.txt:1:admin:SecureCredentials!

/mnt/Finance/Contracts/private/secret.txt:1:file with all credentials

<h3>Other Services</h3>

There are other file-sharing services such as FTP, TFTP, and NFS that we can attach (mount) using different tools and commands. However, once we mount a file-sharing service, we must understand that we can use the available tools in Linux or Windows to interact with files and directories. As we discover new file-sharing services, we will need to investigate how they work and what tools we can use to interact with them.

<h3>Email</h3>

We typically need two protocols to send and receive messages, one for sending and another for receiving. The Simple Mail Transfer Protocol (SMTP) is an email delivery protocol used to send mail over the internet. Likewise, a supporting protocol must be used to retrieve an email from a service. There are two main protocols we can use POP3 and IMAP.

We can use a mail client such as Evolution, the official personal information manager, and mail client for the GNOME Desktop Environment. We can interact with an email server to send or receive messages with a mail client. To install Evolution, we can use the following command:

<h3>Linux - Install Evolution</h3>

@htb[/htb]$ sudo apt-get install evolution

Note: If an error appears when starting evolution indicating "bwrap: Can't create file at ...", use this command to start evolution export WEBKIT_FORCE_SANDBOX=0 && evolution.

<h3>Video - Connecting to IMAP and SMTP using Evolution</h3>

Click on the image below to see a short video demonstration.

<img width="707" height="413" alt="image" src="https://github.com/user-attachments/assets/fde4e746-13c9-4229-942c-db590e3ee056" />

We can use the domain name or IP address of the mail server. If the server uses SMTPS or IMAPS, we'll need the appropriate encryption method (TLS on a dedicated port or STARTTLS after connecting). We can use the Check for Supported Types option under authentication to confirm if the server supports our selected method.

<h3>Databases</h3>

Databases are typically used in enterprises, and most companies use them to store and manage information. There are different types of databases, such as Hierarchical databases, NoSQL (or non-relational) databases, and SQL relational databases. We will focus on SQL relational databases and the two most common relational databases called MySQL & MSSQL. We have three common ways to interact with databases:

1.	Command Line Utilities (mysql or sqsh)
   
2. 	Programming Languages
   
3.	A GUI application to interact with databases such as HeidiSQL, MySQL Workbench, or SQL Server Management Studio.

<h3>MySQL example</h3>

<img width="713" height="629" alt="image" src="https://github.com/user-attachments/assets/80b4e15a-7f4f-42c8-bee3-68e3c15aff4f" />

Let's explore command-line utilities and a GUI application.

<h3>Command Line Utilities</h3>

<h3>MSSQL</h3>

To interact with MSSQL (Microsoft SQL Server) with Linux we can use sqsh or sqlcmd if you are using Windows. Sqsh is much more than a friendly prompt. It is intended to provide much of the functionality provided by a command shell, such as variables, aliasing, redirection, pipes, back-grounding, job control, history, command substitution, and dynamic configuration. We can start an interactive SQL session as follows:


<h3>Linux - SQSH</h3>

@htb[/htb]$ sqsh -S 10.129.20.13 -U username -P Password123

The sqlcmd utility lets you enter Transact-SQL statements, system procedures, and script files through a variety of available modes:

- At the command prompt.

- In Query Editor in SQLCMD mode.

- In a Windows script file.

- In an operating system (Cmd.exe) job step of a SQL Server Agent job.

<h3>Windows - SQLCMD</h3>

C:\htb> sqlcmd -S 10.129.20.13 -U username -P Password123

To learn more about sqlcmd usage, you can see Microsoft documentation.

<h3>MySQL</h3>

To interact with MySQL, we can use MySQL binaries for Linux (mysql) or Windows (mysql.exe). MySQL comes pre-installed on some Linux distributions, but we can install MySQL binaries for Linux or Windows using this guide. Start an interactive SQL Session using Linux:

<h3>Linux - MySQL</h3>

@htb[/htb]$ mysql -u username -pPassword123 -h 10.129.20.13

We can easily start an interactive SQL Session using Windows:

<h3>Windows - MySQL</h3>

C:\htb> mysql.exe -u username -pPassword123 -h 10.129.20.13

<h3>GUI Application</h3>

Database engines commonly have their own GUI application. MySQL has MySQL Workbench and MSSQL has SQL Server Management Studio or SSMS, we can install those tools in our attack host and connect to the database. SSMS is only supported in Windows. An alternative is to use community tools such as dbeaver. dbeaver is a multi-platform database tool for Linux, macOS, and Windows that supports connecting to multiple database engines such as MSSQL, MySQL, PostgreSQL, among others, making it easy for us, as an attacker, to interact with common database servers.

To install dbeaver using a Debian package we can download the release .deb package from https://github.com/dbeaver/dbeaver/releases and execute the following command:

<h3>Install dbeaver</h3>

@htb[/htb]$ sudo dpkg -i dbeaver-<version>.deb

To start the application use:

<h3>Run dbeaver</h3>

@htb[/htb]$ dbeaver &

To connect to a database, we will need a set of credentials, the target IP and port number of the database, and the database engine we are trying to connect to (MySQL, MSSQL, or another).

<h3>Video - Connecting to MSSQL DB using dbeaver</h3>

Click on the image below for a short video demonstration of connecting to an MSSQL database using dbeaver.

<img width="725" height="477" alt="image" src="https://github.com/user-attachments/assets/53357dcf-39ef-4d68-874b-d9e1fb02b400" />

Click on the image below for a short video demonstration of connecting to a MySQL database using dbeaver.

<h3>Video - Connecting to MySQL DB using dbeaver</h3>

<img width="746" height="418" alt="image" src="https://github.com/user-attachments/assets/cebd46a5-8361-4e09-9783-ea5983b19c73" />

Once we have access to the database using a command-line utility or a GUI application, we can use common Transact-SQL statements to enumerate databases and tables containing sensitive information such as usernames and passwords. If we have the correct privileges, we could potentially execute commands as the MSSQL service account. Later in this module, we will discuss common Transact-SQL statements and attacks for MSSQL & MySQL databases.

<h3>Tools</h3>

It is crucial to get familiar with the default command-line utilities available to interact with different services. However, as we move forward in the field, we will find tools that can help us be more efficient. The community commonly creates those tools. Although, eventually, we will have ideas on how a tool can be improved or for creating our own tools, even if we are not full-time developers, the more we get familiar with hacking. The more we learn, the more we find ourselves looking for a tool that does not exist, which may be an opportunity to learn and create our tools.

<h3>Tools to Interact with Common Services</h3>

<table border="1" cellpadding="6" cellspacing="0">
  <thead>
    <tr>
      <th>SMB</th>
      <th>FTP</th>
      <th>Email</th>
      <th>Databases</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>smbclient</td>
      <td>ftp</td>
      <td>Thunderbird</td>
      <td>mssql-cli</td>
    </tr>
    <tr>
      <td>CrackMapExec</td>
      <td>lftp</td>
      <td>Claws</td>
      <td>mycli</td>
    </tr>
    <tr>
      <td>SMBMap</td>
      <td>ncftp</td>
      <td>Geary</td>
      <td>mssqlclient.py</td>
    </tr>
    <tr>
      <td>Impacket</td>
      <td>FileZilla</td>
      <td>MailSpring</td>
      <td>DBeaver</td>
    </tr>
    <tr>
      <td>psexec.py</td>
      <td>CrossFTP</td>
      <td>mutt</td>
      <td>MySQL Workbench</td>
    </tr>
    <tr>
      <td>smbexec.py</td>
      <td></td>
      <td>mailutils</td>
      <td>SQL Server Management Studio (SSMS)</td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>sendEmail</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>swaks</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td>sendmail</td>
      <td></td>
    </tr>
  </tbody>
</table>

<h3>General Troubleshooting</h3>

Depending on the Windows or Linux version we are working with or targeting, we may encounter different problems when attempting to connect to a service.

Some reasons why we may not have access to a resource:

- Authentication

- Privileges

- Network Connection

- Firewall Rules

- Protocol Support

Keep in mind that we may encounter different errors depending on the service we are targeting. We can use the error codes to our advantage and search for official documentation or forums where people solved an issue similar to ours.
