<h3>The Concept of Attacks</h3>

To effectively understand attacks on the different services, we should look at how these services can be attacked. A concept is an outlined plan that is applied to future projects. As an example, we can think of the concept of building a house. Many houses have a basement, four walls, and a roof. Most homes are built this way, and it is a concept that is applied all over the world. The finer details, such as the material used or the type of design, are flexible and can be adapted to individual wishes and circumstances. This example shows that a concept needs a general categorization (floor, walls, roof).

In our case, we need to create a concept for the attacks on all possible services and divide it into categories that summarize all services but leave the individual attack methods.

To explain a little more clearly what we are talking about here, we can try to group the services SSH, FTP, SMB, and HTTP ourselves and figure out what these services have in common. Then we need to create a structure that will allow us to identify the attack points of these different services using a single pattern.

Analyzing commonalities and creating pattern templates that fit all conceivable cases is not a finished product but rather a process that makes these pattern templates grow larger and larger. Therefore, we have created a pattern template for this topic for you to better and more efficiently teach and explain the concept behind the attacks.

<h3>The Concept of Attacks</h3>

<img width="633" height="341" alt="image" src="https://github.com/user-attachments/assets/a8c5265e-4c32-4bff-9a17-a0a40f2f9f62" />

The concept is based on four categories that occur for each vulnerability. First, we have a Source that performs the specific request to a Process where the vulnerability gets triggered. Each process has a specific set of Privileges with which it is executed. Each process has a task with a specific goal or Destination to either compute new data or forward it. However, the individual and unique specifications under these categories may differ from service to service.

Every task and piece of information follows a specific pattern, a cycle, which we have deliberately made linear. This is because the Destination does not always serve as a Source and is therefore not treated as a source of a new task.

For any task to come into existence at all, it needs an idea, information (Source), a planned process for it (Processes), and a specific goal (Destination) to be achieved. Therefore, the category of Privileges is necessary to control information processing appropriately.

<h3>Source</h3>

We can generalize Source as a source of information used for the specific task of a process. There are many different ways to pass information to a process. The graphic shows some of the most common examples of how information is passed to the processes.

<table border="1" cellpadding="6" cellspacing="0">
  <thead>
    <tr>
      <th>Information Source</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Code</td>
      <td>
        This means that the already executed program code results are used as a source of information.
        These can come from different functions of a program.
      </td>
    </tr>
    <tr>
      <td>Libraries</td>
      <td>
        A library is a collection of program resources, including configuration data, documentation,
        help data, message templates, prebuilt code and subroutines, classes, values, or type specifications.
      </td>
    </tr>
    <tr>
      <td>Config</td>
      <td>
        Configurations are usually static or prescribed values that determine how the process handles information.
      </td>
    </tr>
    <tr>
      <td>APIs</td>
      <td>
        The application programming interface (API) is mainly used as the interface of programs
        for retrieving or providing information.
      </td>
    </tr>
    <tr>
      <td>User Input</td>
      <td>
        If a program allows the user to enter specific values that are used to process information,
        this represents manual entry of information by a person.
      </td>
    </tr>
  </tbody>
</table>

The source is, therefore, the source that is exploited for vulnerabilities. It does not matter which protocol is used because HTTP header injections can be manipulated manually, as can buffer overflows. The source for this can therefore be categorized as Code. So let us take a closer look at the pattern template based on one of the latest critical vulnerabilities that most of us have heard of.

<h3>Log4j</h3>

A great example is the critical Log4j vulnerability (CVE-2021-44228) which was published at the end of 2021. Log4j is a framework or Library used to log application messages in Java and other programming languages. This library contains classes and functions that other programming languages can integrate. For this purpose, information is documented, similar to a logbook. Furthermore, the scope of the documentation can be configured extensively. As a result, it has become a standard within many open source and commercial software products. In this example, an attacker can manipulate the HTTP User-Agent header and insert a JNDI lookup as a command intended for the Log4j library. Accordingly, not the actual User-Agent header, such as Mozilla 5.0, is processed, but the JNDI lookup.

<h3>Processes</h3>

The Process is about processing the information forwarded from the source. These are processed according to the intended task determined by the program code. For each task, the developer specifies how the information is processed. This can occur using classes with different functions, calculations, and loops. The variety of possibilities for this is as diverse as the number of developers in the world. Accordingly, most of the vulnerabilities lie in the program code executed by the process.

<table border="1" cellpadding="6" cellspacing="0">
  <thead>
    <tr>
      <th>Process Components</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>PID</td>
      <td>
        The Process ID (PID) identifies a process that is being started or is already running.
        Running processes already have assigned privileges, and new ones are started accordingly.
      </td>
    </tr>
    <tr>
      <td>Input</td>
      <td>
        Refers to the input of information that may be provided by a user or generated
        as a result of a programmed function.
      </td>
    </tr>
    <tr>
      <td>Data processing</td>
      <td>
        The hard-coded functions of a program determine how the received information is processed.
      </td>
    </tr>
    <tr>
      <td>Variables</td>
      <td>
        Variables act as placeholders for information that different functions can further
        process during task execution.
      </td>
    </tr>
    <tr>
      <td>Logging</td>
      <td>
        During logging, certain events are documented and usually stored in a register or file.
        This ensures that specific information persists within the system.
      </td>
    </tr>
  </tbody>
</table>

<h3>Log4j</h3>

The process of Log4j is to log the User-Agent as a string using a function and store it in the designated location. The vulnerability in this process is the misinterpretation of the string, which leads to the execution of a request instead of logging the events. However, before we go further into this function, we need to talk about privileges.

<h3>Privileges</h3>

Privileges are present in any system that controls processes. These serve as a type of permission that determines what tasks and actions can be performed on the system. In simple terms, it can be compared to a bus ticket. If we use a ticket intended for a particular region, we will be able to use the bus, and otherwise, we will not. These privileges (or figuratively speaking, our tickets) can also be used for different means of transport, such as planes, trains, boats, and others. In computer systems, these privileges serve as control and segmentation of actions for which different permissions, controlled by the system, are needed. Therefore, the rights are checked based on this categorization when a process needs to fulfill its task. If the process satisfies these privileges and conditions, the system approves the action requested. We can divide these privileges into the following areas:

<table border="1" cellpadding="6" cellspacing="0">
  <thead>
    <tr>
      <th>Privileges</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>System</td>
      <td>
        These are the highest privileges that can be obtained, allowing full system modification.
        In Windows, this privilege is called <strong>SYSTEM</strong>, and in Linux, it is called <strong>root</strong>.
      </td>
    </tr>
    <tr>
      <td>User</td>
      <td>
        User privileges are permissions assigned to a specific user.
        For security reasons, separate users are often created for particular services
        during Linux distribution installations.
      </td>
    </tr>
    <tr>
      <td>Groups</td>
      <td>
        Groups are a categorization of one or more users that share permissions
        to perform specific actions.
      </td>
    </tr>
    <tr>
      <td>Policies</td>
      <td>
        Policies control the execution of application-specific commands and can apply
        to individual users or groups and their actions.
      </td>
    </tr>
    <tr>
      <td>Rules</td>
      <td>
        Rules define permissions to perform actions that are handled from within
        the applications themselves.
      </td>
    </tr>
  </tbody>
</table>

<h3>Log4j</h3>

What made the Log4j vulnerability so dangerous was the Privileges that the implementation brought. Logs are often considered sensitive because they can contain data about the service, the system itself, or even customers. Therefore, logs are usually stored in locations that no regular user should be able to access. Accordingly, most applications with the Log4j implementation were run with the privileges of an administrator. The process itself exploited the library by manipulating the User-Agent so that the process misinterpreted the source and led to the execution of user-supplied code.

<h3>Destination</h3>

Every task has at least one purpose and goal that must be fulfilled. Logically, if any data set changes were missing or not stored or forwarded anywhere, the task would be generally unnecessary. The result of such a task is either stored somewhere or forwarded to another processing point. Therefore we speak here of the Destination where the changes will be made. Such processing points can point either to a local or remote process. Therefore, at the local level, local files or records may be modified by the process or be forwarded to other local services for further use. However, this does not exclude the possibility that the same process could reuse the resulting data too. If the process is completed with the data storage or its forwarding, the cycle leading to the task's completion is closed.

<table border="1" cellpadding="6" cellspacing="0">
  <thead>
    <tr>
      <th>Destination</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Local</td>
      <td>
        The local area refers to the system environment in which the process occurred.
        Results and outcomes of a task are either processed further by another process,
        included in data set changes, or stored locally.
      </td>
    </tr>
    <tr>
      <td>Network</td>
      <td>
        The network area involves forwarding the results of a process to a remote interface.
        This may be an IP address, a specific service, or even an entire network.
        In certain circumstances, such processes can also influence routing.
      </td>
    </tr>
  </tbody>
</table>

<h3>Log4j</h3>

The misinterpretation of the User-Agent leads to a JNDI lookup which is executed as a command from the system with administrator privileges and queries a remote server controlled by the attacker, which in our case is the Destination in our concept of attacks. This query requests a Java class created by the attacker and is manipulated for its own purposes. The queried Java code inside the manipulated Java class gets executed in the same process, leading to a remote code execution (RCE) vulnerability.

GovCERT.ch has created an excellent graphical representation of the Log4j vulnerability worth examining in detail.

<img width="690" height="463" alt="image" src="https://github.com/user-attachments/assets/5d239a33-f2ce-4731-840d-cd2d25399704" />

Source: https://www.govcert.ch/blog/zero-day-exploit-targeting-popular-java-library-log4j/

This graphic breaks down the Log4j JNDI attack based on the Concept of Attacks.

<h3>Initiation of the Attack</h3>

<table border="1" cellpadding="6" cellspacing="0">
  <thead>
    <tr>
      <th>Step</th>
      <th>Log4j</th>
      <th>Concept of Attacks – Category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>
        The attacker manipulates the user agent with a JNDI lookup command.
      </td>
      <td>Source</td>
    </tr>
    <tr>
      <td>2</td>
      <td>
        The process misinterprets the assigned user agent, leading to the execution of the command.
      </td>
      <td>Process</td>
    </tr>
    <tr>
      <td>3</td>
      <td>
        The JNDI lookup command is executed with administrator privileges due to logging permissions.
      </td>
      <td>Privileges</td>
    </tr>
    <tr>
      <td>4</td>
      <td>
        The JNDI lookup command points to a server controlled by the attacker, which hosts
        a malicious Java class containing attacker-defined commands.
      </td>
      <td>Destination</td>
    </tr>
  </tbody>
</table>

This is when the cycle starts all over again, but this time to gain remote access to the target system.

<h3>Trigger Remote Code Execution</h3>

<table border="1" cellpadding="6" cellspacing="0">
  <thead>
    <tr>
      <th>Step</th>
      <th>Log4j</th>
      <th>Concept of Attacks – Category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>5</td>
      <td>
        After the malicious Java class is retrieved from the attacker's server,
        it is used as a source for further actions in the subsequent process.
      </td>
      <td>Source</td>
    </tr>
    <tr>
      <td>6</td>
      <td>
        The malicious Java class code is read and processed, which in many cases
        results in remote access to the affected system.
      </td>
      <td>Process</td>
    </tr>
    <tr>
      <td>7</td>
      <td>
        The malicious code is executed with administrator privileges due to logging permissions.
      </td>
      <td>Privileges</td>
    </tr>
    <tr>
      <td>8</td>
      <td>
        The executed code communicates back over the network to the attacker,
        providing functions that enable remote control of the system.
      </td>
      <td>Destination</td>
    </tr>
  </tbody>
</table>

Finally, we see a pattern that we can repeatedly use for our attacks. This pattern template can be used to analyze and understand exploits and debug our own exploits during development and testing. In addition, this pattern template can also be applied to source code analysis, which allows us to check certain functionality and commands in our code step-by-step. Finally, we can also think categorically about each task's dangers individually.

