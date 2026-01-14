<h3>Introduction to Attacking Common Applications</h3>

Web-based applications are prevalent in most if not all environments that we encounter as penetration testers. During our assessments, we will come across a wide variety of web applications such as Content Management Systems (CMS), custom web applications, intranet portals used by developers and sysadmins, code repositories, network monitoring tools, ticketing systems, wikis, knowledge bases, issue trackers, servlet container applications, and more. It's common to find the same applications across many different environments. While an application may not be vulnerable in one environment, it may be misconfigured or unpatched in the next. An assessor needs to have a firm grasp of enumerating and attacking the common applications covered in this module.

Web applications are interactive applications that can be accessed via web browsers. Web applications typically adopt a client-server architecture to run and handle interactions. They usually are made up of front-end components (the website interface, or "what the user sees") that run on the client-side (browser) and other back-end components (web application source code) that run on the server-side (back end server/databases). For an in-depth study of the structure and function of web applications, check out the Introduction to Web Applications module.

All types of web applications (commercial, open-source, and custom) can suffer from the same kinds of vulnerabilities and misconfigurations, namely the top 10 web application risks covered in the OWASP Top 10. While we may encounter vulnerable versions of many common applications that suffer from known (public) vulnerabilities such as SQL injection, XSS, remote code execution bugs, local file read, and unrestricted file upload, it is equally important for us to understand how we can abuse the built-in functionality of many of these applications to achieve remote code execution.

As organizations continue to harden their external perimeter and limit exposed services, web applications are becoming a more attractive target for malicious actors and penetration testers alike. More and more companies are transitioning to remote work and exposing (intentionally or unintentionally) applications to the outside world. The applications discussed in this module are typically just as likely to be exposed on the external network as the internal network. These applications can serve as a foothold into the internal environment during an external assessment or as a foothold, lateral movement, or additional issue to report to our client during an internal assessment.

The state of application security in 2021 was a research survey commissioned by Barracuda to gather information from application security-related decision-makers. The survey includes responses from 750 decision-makers in companies with 500 or more employees across the globe. The survey findings were astounding: 72% of respondents stated that their organization suffered at least one breach due to an application vulnerability, 32% suffered two breaches, and 14% suffered three. The organizations polled broke down their challenges as follows: bot attacks (43%), software supply chain attacks (39%), vulnerability detection (38%), and securing APIs (37%). This module will focus on known vulnerabilities and misconfigurations in open-source and commercial applications (free versions demoed in this module), which make up a large percentage of the successful attacks that organizations face regularly.

<h3>Application Data</h3>

This module will study several common applications in-depth while briefly covering some other less common (but still seen often) ones. Just some of the categories of applications we may come across during a given assessment that we may be able to leverage to gain a foothold or gain access to sensitive data include:

<table border="1" cellpadding="6" cellspacing="0">
  <thead>
    <tr>
      <th>Category</th>
      <th>Applications</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Web Content Management</td>
      <td>Joomla, Drupal, WordPress, DotNetNuke, etc.</td>
    </tr>
    <tr>
      <td>Application Servers</td>
      <td>Apache Tomcat, Phusion Passenger, Oracle WebLogic, IBM WebSphere, etc.</td>
    </tr>
    <tr>
      <td>Security Information and Event Management (SIEM)</td>
      <td>Splunk, Trustwave, LogRhythm, etc.</td>
    </tr>
    <tr>
      <td>Network Management</td>
      <td>PRTG Network Monitor, ManageEngine OpManager, etc.</td>
    </tr>
    <tr>
      <td>IT Management</td>
      <td>Nagios, Puppet, Zabbix, ManageEngine ServiceDesk Plus, etc.</td>
    </tr>
    <tr>
      <td>Software Frameworks</td>
      <td>JBoss, Axis2, etc.</td>
    </tr>
    <tr>
      <td>Customer Service Management</td>
      <td>osTicket, Zendesk, etc.</td>
    </tr>
    <tr>
      <td>Search Engines</td>
      <td>Elasticsearch, Apache Solr, etc.</td>
    </tr>
    <tr>
      <td>Software Configuration Management</td>
      <td>Atlassian JIRA, GitHub, GitLab, Bugzilla, Bugsnag, Bitbucket, etc.</td>
    </tr>
    <tr>
      <td>Software Development Tools</td>
      <td>Jenkins, Atlassian Confluence, phpMyAdmin, etc.</td>
    </tr>
    <tr>
      <td>Enterprise Application Integration</td>
      <td>Oracle Fusion Middleware, BizTalk Server, Apache ActiveMQ, etc.</td>
    </tr>
  </tbody>
</table>

As you can see browsing the links for each category above, there are thousands of applications that we may encounter during a given assessment. Many of these suffer from publicly known exploits or have functionality that can be abused to gain remote code execution, steal credentials, or access sensitive information with or without valid credentials. This module will cover the most prevalent applications that we repeatedly see during internal and external assessments.

Let's take a look at the Enlyft website. We can see, for example, they were able to gather data on over 3.7 million companies that are using WordPress which makes up nearly 70% of the market share worldwide for Web Content Management applications for all companies polled. For SIEM tool Splunk was used by 22,174 of the companies surveyed and represented nearly 30% of the market share for SIEM tools. While the remaining applications we will cover represent a much smaller market share for their respective category, I still see these often, and the skills learned here can be applied to many different situations.

While working through the section examples, questions, and skills assessments, make a concerted effort to learn how these applications work and why specific vulnerabilities and misconfigurations exist rather than just reproducing the examples to move swiftly through the module. These skills will benefit you greatly and could likely help you identify attack paths in different applications that you encounter during an assessment for the first time. I still encounter applications that I have only seen a few times or never before, and approaching them with this mindset has often helped me pull off attacks or find a way to abuse built-in functionality.

<h3>A Quick Story</h3>

For example, during one external penetration test, I encountered the Nexus Repository OSS application from Sonatype, which I had never seen before. I quickly found that the default admin credentials of admin:admin123 for that version had not been changed, and I was able to log in and poke around the admin functionality. In this version, I leveraged the API as an authenticated user to gain remote code execution on the system. I encountered this application on another assessment, was able to log in with default credentials yet again. This time was able to abuse the Tasks functionality (which was disabled the first time I encountered this application) and write a quick Groovy script in Java syntax to execute a script and gain remote code execution. This is similar to how we'll abuse the Jenkins script console later in this module. I have encountered many other applications, such as OpManager from ManageEngine that allow you to run a script as the user that the application is running under (usually the powerful NT AUTHORITY\SYSTEM account) and gain a foothold. We should never overlook applications during an internal and external assessment as they may be our only way "in" in a relatively well-maintained environment.

<h3>Common Applications</h3>

I typically run into at least one of the applications below, which we will cover in-depth throughout the module sections. While we cannot cover every possible application that we may encounter, the skills taught in this module will prepare us to approach all applications with a critical eye and assess them for public vulnerabilities and misconfigurations.

<table border="1" cellpadding="6" cellspacing="0">
  <thead>
    <tr>
      <th>Application</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>WordPress</td>
      <td>
        WordPress is an open-source Content Management System (CMS) used for blogs, forums, and company websites. 
        It is highly customizable and SEO-friendly, but its extensibility through third-party themes and plugins 
        makes it prone to vulnerabilities. WordPress is written in PHP and typically runs on Apache with MySQL as the backend.
      </td>
    </tr>
    <tr>
      <td>Drupal</td>
      <td>
        Drupal is an open-source CMS popular among developers and enterprises. Written in PHP, it supports MySQL, 
        PostgreSQL, and SQLite backends. Like WordPress, Drupal allows extensive customization through themes and modules.
      </td>
    </tr>
    <tr>
      <td>Joomla</td>
      <td>
        Joomla is an open-source PHP-based CMS commonly used for blogs, forums, and e-commerce sites. 
        It typically uses MySQL but can also run on PostgreSQL or SQLite. Joomla is heavily customizable 
        and is one of the most widely used CMS platforms globally.
      </td>
    </tr>
    <tr>
      <td>Apache Tomcat</td>
      <td>
        Apache Tomcat is an open-source web server and servlet container designed for Java applications. 
        Initially built for Java Servlets and JSP, it is now widely used with frameworks like Spring and tools such as Gradle.
      </td>
    </tr>
    <tr>
      <td>Jenkins</td>
      <td>
        Jenkins is an open-source automation server written in Java that supports continuous integration and deployment. 
        It runs in servlet containers like Tomcat. Jenkins has had multiple historical vulnerabilities, including 
        unauthenticated remote code execution in older versions.
      </td>
    </tr>
    <tr>
      <td>Splunk</td>
      <td>
        Splunk is a log analytics and data visualization platform often used as a SIEM solution. 
        It stores sensitive operational and security data, making it a high-value target. 
        Historically, Splunk has had relatively few vulnerabilities, with notable cases including 
        information disclosure and legacy authenticated RCE issues.
      </td>
    </tr>
    <tr>
      <td>PRTG Network Monitor</td>
      <td>
        PRTG is an agentless network monitoring solution used to track uptime, bandwidth, and performance. 
        It uses auto-discovery and protocols such as ICMP, WMI, SNMP, and NetFlow. 
        PRTG is written in Delphi.
      </td>
    </tr>
    <tr>
      <td>osTicket</td>
      <td>
        osTicket is an open-source support ticketing system for managing customer service requests via email, phone, 
        and web interfaces. It is written in PHP and runs on Apache or IIS with MySQL as the backend.
      </td>
    </tr>
    <tr>
      <td>GitLab</td>
      <td>
        GitLab is an open-source DevOps platform providing Git repository management, CI/CD, issue tracking, 
        and code review. It was originally written in Ruby and now uses Ruby on Rails, Go, and Vue.js. 
        GitLab is available in both Community and Enterprise editions.
      </td>
    </tr>
  </tbody>
</table>

<h3>Module Targets</h3>

Throughout the module sections, we will refer to URLs such as http://app.inlanefreight.local. To simulate a large, realistic environment with multiple webservers, we utilize Vhosts to house the web applications. Since these Vhosts all map to a different directory on the same host, we have to make manual entries in our /etc/hosts file on the Pwnbox or local attack VM to interact with the lab. This needs to be done for any examples that show scans or screenshots using a FQDN. Sections such as Splunk that only use the spawned target's IP address will not require a hosts file entry, and you can just interact with the spawned IP address and associated port.

To do this quickly, we could run the following:

htb[/htb]$ IP=10.129.42.195

@htb[/htb]$ printf "%s\t%s\n\n" "$IP" "app.inlanefreight.local dev.inlanefreight.local blog.inlanefreight.local" | sudo tee -a /etc/hosts

After this command, our /etc/hosts file would look like the following (on a newly spawned Pwnbox):

@htb[/htb]$ cat /etc/hosts

You may wish to write your own script or edit the hosts file by hand, which is fine.

If you spawn a target during a section and cannot access it directly via the FQDN be sure to check your hosts file and update any entries!

Module exercises that require vhosts will display a list that you can use to edit your hosts file after spawning the target VM at the bottom of the respective section.

