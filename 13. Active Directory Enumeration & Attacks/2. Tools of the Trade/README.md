<h3>Tools of Trade</h3>

Many of the module sections require tools such as open-source scripts or precompiled binaries. These can be found in the C:\Tools directory on the Windows hosts provided in the sections aimed at attacking from Windows. In sections that focus on attacking AD from Linux, we provide a Parrot Linux host customized for the target environment as if you were an anonymous user with an attack host within the internal network. All necessary tools and scripts are preloaded on this host (either installed or in the /opt directory). Here is a listing of many of the tools that we will cover in this module:

<table border="1" cellpadding="6" cellspacing="0">
  <thead>
    <tr>
      <th>Tool</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>PowerView / SharpView</td>
      <td>PowerShell and .NET tools used to gain situational awareness in Active Directory. Useful for identifying additional access, targeting users or computers, and finding quick wins such as Kerberoasting or ASREPRoasting opportunities.</td>
    </tr>
    <tr>
      <td>BloodHound</td>
      <td>Visually maps Active Directory relationships to identify attack paths using data collected by SharpHound and analyzed with a Neo4j graph database.</td>
    </tr>
    <tr>
      <td>SharpHound</td>
      <td>C# data collector that gathers information on AD users, groups, computers, ACLs, GPOs, sessions, and more for BloodHound analysis.</td>
    </tr>
    <tr>
      <td>BloodHound.py</td>
      <td>Python-based BloodHound ingestor built on Impacket. Can be run from a non-domain joined host.</td>
    </tr>
    <tr>
      <td>Kerbrute</td>
      <td>Go-based tool for enumerating AD accounts and performing password spraying using Kerberos pre-authentication.</td>
    </tr>
    <tr>
      <td>Impacket Toolkit</td>
      <td>Collection of Python tools for interacting with network protocols and attacking or enumerating Active Directory.</td>
    </tr>
    <tr>
      <td>Responder</td>
      <td>Tool for poisoning LLMNR, NBT-NS, and MDNS to capture credentials.</td>
    </tr>
    <tr>
      <td>Inveigh.ps1</td>
      <td>PowerShell-based network spoofing and poisoning tool similar to Responder.</td>
    </tr>
    <tr>
      <td>C# Inveigh (InveighZero)</td>
      <td>C# version of Inveigh with a semi-interactive console for captured credential interaction.</td>
    </tr>
    <tr>
      <td>rpcinfo</td>
      <td>Queries available RPC services on a remote host.</td>
    </tr>
    <tr>
      <td>rpcclient</td>
      <td>Samba utility used to enumerate Active Directory information via RPC.</td>
    </tr>
    <tr>
      <td>CrackMapExec (CME)</td>
      <td>Enumeration, attack, and post-exploitation framework that abuses built-in AD protocols.</td>
    </tr>
    <tr>
      <td>Rubeus</td>
      <td>C# tool for Kerberos abuse.</td>
    </tr>
    <tr>
      <td>GetUserSPNs.py</td>
      <td>Impacket module used to enumerate Service Principal Names for Kerberoasting.</td>
    </tr>
    <tr>
      <td>Hashcat</td>
      <td>Password recovery and hash cracking tool.</td>
    </tr>
    <tr>
      <td>enum4linux</td>
      <td>Enumerates information from Windows and Samba systems.</td>
    </tr>
    <tr>
      <td>enum4linux-ng</td>
      <td>Modern reimplementation of enum4linux with improved functionality.</td>
    </tr>
    <tr>
      <td>ldapsearch</td>
      <td>Command-line tool for querying LDAP directories.</td>
    </tr>
    <tr>
      <td>windapsearch</td>
      <td>Python script for enumerating AD users, groups, and computers via LDAP.</td>
    </tr>
    <tr>
      <td>DomainPasswordSpray.ps1</td>
      <td>PowerShell tool for performing password spray attacks against domain users.</td>
    </tr>
    <tr>
      <td>LAPSToolkit</td>
      <td>PowerShell toolkit for auditing and attacking environments using Microsoft LAPS.</td>
    </tr>
    <tr>
      <td>smbmap</td>
      <td>Enumerates SMB shares across a domain.</td>
    </tr>
    <tr>
      <td>psexec.py</td>
      <td>Impacket tool providing PsExec-like remote shell functionality.</td>
    </tr>
    <tr>
      <td>wmiexec.py</td>
      <td>Impacket tool for remote command execution over WMI.</td>
    </tr>
    <tr>
      <td>Snaffler</td>
      <td>Searches accessible file shares for sensitive information such as credentials.</td>
    </tr>
    <tr>
      <td>smbserver.py</td>
      <td>Simple SMB server for file transfer within a network.</td>
    </tr>
    <tr>
      <td>setspn.exe</td>
      <td>Windows utility to manage Service Principal Names in Active Directory.</td>
    </tr>
    <tr>
      <td>Mimikatz</td>
      <td>Tool for credential extraction, pass-the-hash, and Kerberos ticket dumping.</td>
    </tr>
    <tr>
      <td>secretsdump.py</td>
      <td>Impacket tool to remotely dump SAM and LSA secrets.</td>
    </tr>
    <tr>
      <td>evil-winrm</td>
      <td>Provides an interactive shell over the WinRM protocol.</td>
    </tr>
    <tr>
      <td>mssqlclient.py</td>
      <td>Impacket tool for interacting with MSSQL databases.</td>
    </tr>
    <tr>
      <td>noPac.py</td>
      <td>Exploit for CVE-2021-42278 and CVE-2021-42287 to escalate privileges.</td>
    </tr>
    <tr>
      <td>rpcdump.py</td>
      <td>Impacket tool for enumerating RPC endpoints.</td>
    </tr>
    <tr>
      <td>CVE-2021-1675.py</td>
      <td>PrintNightmare proof-of-concept exploit.</td>
    </tr>
    <tr>
      <td>ntlmrelayx.py</td>
      <td>Impacket tool for performing NTLM relay attacks.</td>
    </tr>
    <tr>
      <td>PetitPotam.py</td>
      <td>PoC tool to coerce Windows hosts to authenticate via MS-EFSRPC.</td>
    </tr>
    <tr>
      <td>gettgtpkinit.py</td>
      <td>Tool for manipulating certificates and Kerberos TGTs.</td>
    </tr>
    <tr>
      <td>getnthash.py</td>
      <td>Uses an existing TGT to request a PAC via U2U.</td>
    </tr>
    <tr>
      <td>adidnsdump</td>
      <td>Dumps DNS records from Active Directory.</td>
    </tr>
    <tr>
      <td>gpp-decrypt</td>
      <td>Decrypts credentials stored in Group Policy Preferences.</td>
    </tr>
    <tr>
      <td>GetNPUsers.py</td>
      <td>Impacket tool for ASREPRoasting to obtain AS-REP hashes.</td>
    </tr>
    <tr>
      <td>lookupsid.py</td>
      <td>SID brute-forcing tool.</td>
    </tr>
    <tr>
      <td>ticketer.py</td>
      <td>Creates and customizes Kerberos tickets (Golden Tickets, trust attacks).</td>
    </tr>
    <tr>
      <td>raiseChild.py</td>
      <td>Automates child-to-parent domain privilege escalation.</td>
    </tr>
    <tr>
      <td>Active Directory Explorer</td>
      <td>GUI tool for viewing, editing, and snapshotting Active Directory databases.</td>
    </tr>
    <tr>
      <td>PingCastle</td>
      <td>Audits Active Directory security based on a risk and maturity framework.</td>
    </tr>
    <tr>
      <td>Group3r</td>
      <td>Audits Group Policy Objects (GPOs) for security misconfigurations.</td>
    </tr>
    <tr>
      <td>ADRecon</td>
      <td>Extracts and reports Active Directory data, often exported to Excel for analysis.</td>
    </tr>
  </tbody>
</table>
