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
