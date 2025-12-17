<h3>Introduction</h3>

Web Reconnaissance is the foundation of a thorough security assessment. This process involves systematically and meticulously collecting information about a target website or web application. Think of it as the preparatory phase before delving into deeper analysis and potential exploitation. It forms a critical part of the "Information Gathering" phase of the Penetration Testing Process.

The primary goals of web reconnaissance include:

- Identifying Assets: Uncovering all publicly accessible components of the target, such as web pages, subdomains, IP addresses, and technologies used. This step provides a comprehensive overview of the target's online presence.

- Discovering Hidden Information: Locating sensitive information that might be inadvertently exposed, including backup files, configuration files, or internal documentation. These findings can reveal valuable insights and potential entry points for attacks.

- Analysing the Attack Surface: Examining the target's attack surface to identify potential vulnerabilities and weaknesses. This involves assessing the technologies used, configurations, and possible entry points for exploitation.

- Gathering Intelligence: Collecting information that can be leveraged for further exploitation or social engineering attacks. This includes identifying key personnel, email addresses, or patterns of behaviour that could be exploited.

Attackers leverage this information to tailor their attacks, allowing them to target specific weaknesses and bypass security measures. Conversely, defenders use recon to proactively identify and patch vulnerabilities before malicious actors can leverage them.

<h3>Types of Reconnaissance</h3>

Web reconnaissance encompasses two fundamental methodologies: active and passive reconnaissance. Each approach offers distinct advantages and challenges, and understanding their differences is crucial for adequate information gathering.

<h3>Active Reconnaissance</h3>

In active reconnaissance, the attacker directly interacts with the target system to gather information. This interaction can take various forms:

<table border="1" cellpadding="6" cellspacing="0">
  <thead>
    <tr>
      <th>Technique</th>
      <th>Description</th>
      <th>Example</th>
      <th>Tools</th>
      <th>Risk of Detection</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Port Scanning</td>
      <td>Identifying open ports and services running on the target.</td>
      <td>Using Nmap to scan a web server for open ports such as 80 (HTTP) and 443 (HTTPS).</td>
      <td>Nmap, Masscan, Unicornscan</td>
      <td>High: Direct interaction with the target can trigger intrusion detection systems (IDS) and firewalls.</td>
    </tr>
    <tr>
      <td>Vulnerability Scanning</td>
      <td>Probing the target for known vulnerabilities, such as outdated software or misconfigurations.</td>
      <td>Running Nessus against a web application to check for SQL injection or cross-site scripting (XSS).</td>
      <td>Nessus, OpenVAS, Nikto</td>
      <td>High: Vulnerability scanners send payloads that security solutions can detect.</td>
    </tr>
    <tr>
      <td>Network Mapping</td>
      <td>Mapping the target's network topology, including connected devices and relationships.</td>
      <td>Using traceroute to determine the path packets take to reach a target server.</td>
      <td>Traceroute, Nmap</td>
      <td>Medium to High: Excessive or unusual network traffic can raise suspicion.</td>
    </tr>
    <tr>
      <td>Banner Grabbing</td>
      <td>Retrieving information from banners displayed by services running on the target.</td>
      <td>Connecting to a web server on port 80 and examining the HTTP banner.</td>
      <td>Netcat, curl</td>
      <td>Low: Minimal interaction, though actions may still be logged.</td>
    </tr>
    <tr>
      <td>OS Fingerprinting</td>
      <td>Identifying the operating system running on the target.</td>
      <td>Using Nmap OS detection (-O) to determine if the target runs Windows or Linux.</td>
      <td>Nmap, Xprobe2</td>
      <td>Low: Often passive, but advanced techniques may be detectable.</td>
    </tr>
    <tr>
      <td>Service Enumeration</td>
      <td>Determining the specific versions of services running on open ports.</td>
      <td>Using Nmap service detection (-sV) to identify Apache or Nginx versions.</td>
      <td>Nmap</td>
      <td>Low: Can be logged but is less likely to trigger alerts.</td>
    </tr>
    <tr>
      <td>Web Spidering</td>
      <td>Crawling a website to identify pages, directories, and files.</td>
      <td>Using Burp Suite Spider or OWASP ZAP Spider to discover hidden resources.</td>
      <td>Burp Suite Spider, OWASP ZAP Spider, Scrapy</td>
      <td>Low to Medium: Detectable if crawler behavior does not mimic normal users.</td>
    </tr>
  </tbody>
</table>


Active reconnaissance provides a direct and often more comprehensive view of the target's infrastructure and security posture. However, it also carries a higher risk of detection, as the interactions with the target can trigger alerts or raise suspicion.

<h3>Passive Reconnaissance</h3>

In contrast, passive reconnaissance involves gathering information about the target without directly interacting with it. This relies on analysing publicly available information and resources, such as:

<table border="1" cellpadding="6" cellspacing="0">
  <thead>
    <tr>
      <th>Technique</th>
      <th>Description</th>
      <th>Example</th>
      <th>Tools</th>
      <th>Risk of Detection</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Search Engine Queries</td>
      <td>
        Using search engines to uncover information about the target, including websites,
        social media profiles, and news articles.
      </td>
      <td>
        Searching Google for "<em>[Target Name] employees</em>" to find employee or social media information.
      </td>
      <td>
        Google, DuckDuckGo, Bing, specialised search engines (e.g., Shodan)
      </td>
      <td>
        Very Low: Normal internet activity and unlikely to trigger alerts.
      </td>
    </tr>
    <tr>
      <td>WHOIS Lookups</td>
      <td>
        Querying WHOIS databases to retrieve domain registration details.
      </td>
      <td>
        Performing a WHOIS lookup on a target domain to identify registrant and name server details.
      </td>
      <td>
        whois command-line tool, online WHOIS services
      </td>
      <td>
        Very Low: Legitimate queries that do not raise suspicion.
      </td>
    </tr>
    <tr>
      <td>DNS Analysis</td>
      <td>
        Analysing DNS records to identify subdomains, mail servers, and infrastructure.
      </td>
      <td>
        Using <code>dig</code> to enumerate subdomains of a target domain.
      </td>
      <td>
        dig, nslookup, host, dnsenum, fierce, dnsrecon
      </td>
      <td>
        Very Low: DNS queries are essential to normal internet operation.
      </td>
    </tr>
    <tr>
      <td>Web Archive Analysis</td>
      <td>
        Examining historical snapshots of a website to identify changes or hidden information.
      </td>
      <td>
        Using the Wayback Machine to review previous versions of a target website.
      </td>
      <td>
        Wayback Machine
      </td>
      <td>
        Very Low: Viewing archived websites is common and non-intrusive.
      </td>
    </tr>
    <tr>
      <td>Social Media Analysis</td>
      <td>
        Gathering information from public social media platforms.
      </td>
      <td>
        Searching LinkedIn for employees of a target organisation to understand roles and structure.
      </td>
      <td>
        LinkedIn, Twitter, Facebook, specialised OSINT tools
      </td>
      <td>
        Very Low: Accessing public profiles is not considered intrusive.
      </td>
    </tr>
    <tr>
      <td>Code Repositories</td>
      <td>
        Analysing publicly accessible code repositories for exposed credentials or vulnerabilities.
      </td>
      <td>
        Searching GitHub for repositories related to a target that may expose sensitive information.
      </td>
      <td>
        GitHub, GitLab
      </td>
      <td>
        Very Low: Public repositories are designed to be accessed and searched.
      </td>
    </tr>
  </tbody>
</table>

Passive reconnaissance is generally considered stealthier and less likely to trigger alarms than active reconnaissance. However, it may yield less comprehensive information, as it relies on what's already publicly accessible.

In this module, we will delve into the essential tools and techniques used in web reconnaissance, starting with WHOIS. Understanding the WHOIS protocol provides a gateway to accessing vital information about domain registrations, ownership details, and the digital infrastructure of targets. This foundational knowledge sets the stage for more advanced recon methods we'll explore later.

