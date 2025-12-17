<h3>Common Terms</h3>

Penetration testing/hacking is an enormous field. We will encounter countless technologies throughout our careers. Here are some of the most common terms and technologies that we will come across repeatedly and must have a firm grasp of. This is not an exhaustive list but is enough to get started with fundamental Modules and easy HTB boxes.

<h3>What is a Shell?</h3>

Shell is a very common term that we will hear again and again during our journey. It has a few meanings. On a Linux system, the shell is a program that takes input from the user via the keyboard and passes these commands to the operating system to perform a specific function. In the early days of computing, the shell was the only interface available for interacting with systems. Since then, many more operating system types and versions have emerged along with the graphic user interface (GUI) to complement command-line interfaces (shell), such as the Linux terminal, Windows command-line (cmd.exe), and Windows PowerShell.

Most Linux systems use a program called Bash (Bourne Again Shell) as a shell program to interact with the operating system. Bash is an enhanced version of sh, the Unix systems' original shell program. Aside from bash there are also other shells, including but not limited to Zsh, Tcsh, Ksh, Fish shell, etc.

We will often read about or hear others talking about "getting a shell" on a box (system). This means that the target host has been exploited, and we have obtained shell-level access (typically bash or sh) and can run commands interactively as if we are sitting logged in to the host. A shell may be obtained by exploiting a web application or network/service vulnerability or obtaining credentials and logging into the target host remotely. There are three main types of shell connections:

<table border="1" cellpadding="6" cellspacing="0">
  <thead>
    <tr>
      <th>Shell Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Reverse shell</td>
      <td>Initiates a connection back to a listener on the attack box.</td>
    </tr>
    <tr>
      <td>Bind shell</td>
      <td>Binds to a specific port on the target host and waits for a connection from the attack box.</td>
    </tr>
    <tr>
      <td>Web shell</td>
      <td>
        Runs operating system commands via a web browser; typically not interactive or semi-interactive.
        Often used to run single commands (e.g., via a file upload vulnerability using a PHP script).
      </td>
    </tr>
  </tbody>
</table>

Each type of shell has its use case, and the same way there are many ways to obtain a shell, the helper program that we use to get a shell can be written in many languages (Python, Perl, Go, Bash, Java, awk, PHP, etc.). These can be small scripts or larger, more complex programs to facilitate a connection from the target host back to our attacking system and obtain "shell" access. Shell access will be discussed in-depth in a later section.

<h3>What is a Port?</h3>

A port can be thought of as a window or door on a house (the house being a remote system), if a window or door is left open or not locked correctly, we can often gain unauthorized access to a home. This is similar in computing. Ports are virtual points where network connections begin and end. They are software-based and managed by the host operating system. Ports are associated with a specific process or service and allow computers to differentiate between different traffic types (SSH traffic flows to a different port than web requests to access a website even though the access requests are sent over the same network connection).

Each port is assigned a number, and many are standardized across all network-connected devices (though a service can be configured to run on a non-standard port). For example, HTTP messages (website traffic) typically go to port 80, while HTTPS messages go to port 443 unless configured otherwise. We will encounter web applications running on non-standard ports but typically find them on ports 80 and 443. Port numbers allow us to access specific services or applications running on target devices. At a very high level, ports help computers understand how to handle the various types of data they receive.

There are two categories of ports, Transmission Control Protocol (TCP), and User Datagram Protocol (UDP).
TCP is connection-oriented, meaning that a connection between a client and a server must be established before data can be sent. The server must be in a listening state awaiting connection requests from clients.
UDP utilizes a connectionless communication model. There is no "handshake" and therefore introduces a certain amount of unreliability since there is no guarantee of data delivery. UDP is useful when error correction/checking is either not needed or is handled by the application itself. UDP is suitable for applications that run time-sensitive tasks since dropping packets is faster than waiting for delayed packets due to retransmission, as is the case with TCP and can significantly affect a real-time system. There are 65,535 TCP ports and 65,535 different UDP ports, each denoted by a number. Some of the most well-known TCP and UDP ports are listed below:

<table border="1" cellpadding="6" cellspacing="0">
  <thead>
    <tr>
      <th>Port(s)</th>
      <th>Protocol</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>20 / 21 (TCP)</td>
      <td>FTP</td>
    </tr>
    <tr>
      <td>22 (TCP)</td>
      <td>SSH</td>
    </tr>
    <tr>
      <td>23 (TCP)</td>
      <td>Telnet</td>
    </tr>
    <tr>
      <td>25 (TCP)</td>
      <td>SMTP</td>
    </tr>
    <tr>
      <td>80 (TCP)</td>
      <td>HTTP</td>
    </tr>
    <tr>
      <td>161 (TCP / UDP)</td>
      <td>SNMP</td>
    </tr>
    <tr>
      <td>389 (TCP / UDP)</td>
      <td>LDAP</td>
    </tr>
    <tr>
      <td>443 (TCP)</td>
      <td>SSL/TLS (HTTPS)</td>
    </tr>
    <tr>
      <td>445 (TCP)</td>
      <td>SMB</td>
    </tr>
    <tr>
      <td>3389 (TCP)</td>
      <td>RDP</td>
    </tr>
  </tbody>
</table>

As information security professionals, we must be able to quickly recall large amounts of information on a wide variety of topics. It is essential for us, especially as pentesters, to have a firm grasp of many TCP and UDP ports and be able to recognize them from just their number quickly (i.e., know that port 21 is FTP, port 80 is HTTP, port 88 is Kerberos) without having to look it up. This will come with practice and repetition and eventually become second nature as we attack more boxes, labs, and real-world networks and help us work more efficiently and better prioritize our enumeration efforts and attacks.

Guides such as this and this are great resources for learning standard and less common TCP and UDP ports. Challenge yourself to memorize as many of these as possible and do some research about each of the protocols listed in the table above. This is a great reference on the top 1,000 TCP and UDP ports from nmap along with the top 100 services scanned by nmap.

<h3>What is a Web Server</h3>

A web server is an application that runs on the back-end server, which handles all of the HTTP traffic from the client-side browser, routes it to the requests destination pages, and finally responds to the client-side browser. Web servers usually run on TCP ports 80 or 443, and are responsible for connecting end-users to various parts of the web application, in addition to handling their various responses:

As web applications tend to be open for public interaction and facing the internet, they may lead to the back-end server being compromised if they suffer from any vulnerabilities. Web applications can provide a vast attack surface, making them a high-value target for attackers and pentesters.

Many types of vulnerabilities can affect web applications. We will often hear about/see references to the OWASP Top 10. This is a standardized list of the top 10 web application vulnerabilities maintained by the Open Web Application Security Project (OWASP). This list is considered the top 10 most dangerous vulnerabilities and is not an exhaustive list of all possible web application vulnerabilities. Web application security assessment methodologies are often based around the OWASP top 10 as a starting point for the top categories of flaws that an assessor should be checking for. The current OWASP Top 10 list is:

<table border="1" cellpadding="6" cellspacing="0">
  <thead>
    <tr>
      <th>Number</th>
      <th>Category</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>Broken Access Control</td>
      <td>
        Restrictions are not appropriately implemented to prevent users from accessing other users’ accounts,
        viewing sensitive data, accessing unauthorized functionality, or modifying data.
      </td>
    </tr>
    <tr>
      <td>2</td>
      <td>Cryptographic Failures</td>
      <td>
        Failures related to cryptography which often lead to sensitive data exposure or system compromise.
      </td>
    </tr>
    <tr>
      <td>3</td>
      <td>Injection</td>
      <td>
        User-supplied data is not validated, filtered, or sanitized by the application.
        Examples include SQL injection, command injection, and LDAP injection.
      </td>
    </tr>
    <tr>
      <td>4</td>
      <td>Insecure Design</td>
      <td>
        Security weaknesses that occur when an application is not designed with security principles in mind.
      </td>
    </tr>
    <tr>
      <td>5</td>
      <td>Security Misconfiguration</td>
      <td>
        Missing security hardening, insecure default configurations, open cloud storage,
        or verbose error messages that disclose excessive information.
      </td>
    </tr>
    <tr>
      <td>6</td>
      <td>Vulnerable and Outdated Components</td>
      <td>
        Use of components (client-side or server-side) that are vulnerable, unsupported, or out of date.
      </td>
    </tr>
    <tr>
      <td>7</td>
      <td>Identification and Authentication Failures</td>
      <td>
        Failures related to authentication, identity management, and session handling.
      </td>
    </tr>
    <tr>
      <td>8</td>
      <td>Software and Data Integrity Failures</td>
      <td>
        Code or infrastructure that does not protect against integrity violations,
        such as relying on plugins or libraries from untrusted sources or repositories.
      </td>
    </tr>
    <tr>
      <td>9</td>
      <td>Security Logging and Monitoring Failures</td>
      <td>
        Insufficient logging and monitoring, making it difficult to detect, escalate,
        and respond to active security breaches.
      </td>
    </tr>
    <tr>
      <td>10</td>
      <td>Server-Side Request Forgery (SSRF)</td>
      <td>
        Occurs when a web application fetches a remote resource without validating the user-supplied URL,
        allowing attackers to force requests to unintended destinations.
      </td>
    </tr>
  </tbody>
</table>

It is essential to become familiar with each of these categories and the various vulnerabilities that fit each. Web application vulnerabilities will be covered in-depth in later modules. To learn more about web applications, check out the Introduction to Web Applications module.

