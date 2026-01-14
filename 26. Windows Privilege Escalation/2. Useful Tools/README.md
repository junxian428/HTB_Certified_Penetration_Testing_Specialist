<h3>Useful Tools</h3>

There are many tools available to us to assist with enumerating Windows systems for common and obscure privilege escalation vectors. Below is a list of useful binaries and scripts, many of which we will cover within the coming module sections.

<table border="1" cellpadding="6" cellspacing="0">
  <thead>
    <tr>
      <th>Tool</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Seatbelt</td>
      <td>C# project for performing a wide variety of local privilege escalation checks.</td>
    </tr>
    <tr>
      <td>winPEAS</td>
      <td>Script that searches for possible paths to escalate privileges on Windows hosts. All checks are well documented.</td>
    </tr>
    <tr>
      <td>PowerUp</td>
      <td>PowerShell script for finding common Windows privilege escalation vectors based on misconfigurations. Can also exploit some issues found.</td>
    </tr>
    <tr>
      <td>SharpUp</td>
      <td>C# implementation of PowerUp.</td>
    </tr>
    <tr>
      <td>JAWS</td>
      <td>PowerShell 2.0 script for enumerating Windows privilege escalation vectors.</td>
    </tr>
    <tr>
      <td>SessionGopher</td>
      <td>PowerShell tool that finds and decrypts saved session data from tools like PuTTY, WinSCP, SuperPuTTY, FileZilla, and RDP.</td>
    </tr>
    <tr>
      <td>Watson</td>
      <td>.NET tool that enumerates missing Windows KBs and suggests privilege escalation exploits.</td>
    </tr>
    <tr>
      <td>LaZagne</td>
      <td>Tool for retrieving passwords stored locally in browsers, databases, email clients, Git, Wi-Fi configs, Windows credential storage, and more.</td>
    </tr>
    <tr>
      <td>Windows Exploit Suggester – Next Generation (WES-NG)</td>
      <td>Analyzes Windows systeminfo output to identify missing patches and potential vulnerabilities across Windows XP to Windows 10 and Server editions.</td>
    </tr>
    <tr>
      <td>Sysinternals Suite</td>
      <td>Collection of Microsoft tools used for enumeration, including AccessChk, PipeList, and PsService.</td>
    </tr>
  </tbody>
</table>

We can also find pre-compiled binaries of Seatbelt and SharpUp here, and standalone binaries of LaZagne here. It is recommended that we always compile our tools from the source if using them in a client environment.

Note: Depending on how we gain access to a system we may not have many directories that are writeable by our user to upload tools. It is always a safe bet to upload tools to C:\Windows\Temp because the BUILTIN\Users group has write access.

This is not an exhaustive list of tools available to us. Furthermore, we should strive to learn what each tool does if one does not work as expected, or we cannot load them onto the target system. Tools like the ones listed above are extremely useful in narrowing down our checks and focusing our enumeration. Enumerating a Windows system can be a daunting task with an immense amount of information to sift through and make sense of. Tools can make this process faster and also give us more output in an easy-to-read format. A disadvantage to this can be information overload, since some of these tools, such as winPEAS, return an incredible amount of information that is mostly not useful to us. Tools can be a double-edged sword. While they help speed up the enumeration process and provide us with highly detailed output, we could be working less efficiently if we do not know how to read the output or narrow it down to the most interesting data points. Tools can also produce false positives, so we must have a deep understanding of many possible privilege escalation techniques to troubleshoot when things go wrong or are not what they seem to be. Learning the enumeration techniques manually will help to ensure that we do not miss obvious flaws due to an issue with a tool, like a false negative or false positive.

Throughout this module, we will show manual enumeration techniques for the various examples we cover and tool output where applicable. Aside from the enumeration techniques, it is also vital to learn how to perform the exploitation steps manually and not rely on "autopwn" scripts or tools that we cannot control. It is fine (and encouraged!) to write our own tools/scripts to perform both enumeration and exploitation steps. Still, we should be confident enough in both phases to explain precisely what we are doing to our client at any stage in the process. We should also be able to operate in an environment where we cannot load tools (such as an air-gapped network or systems that do not have internet access or allow us to plug in an external device such as a USB flash drive).

These tools are not only beneficial for penetration testers but can also assist systems administrators with their jobs by helping to identify low-hanging fruit to fix before an assessment, periodically checking the security posture of a few machines, analyzing the impact of an upgrade or other changes, or performing an in-depth security review on a new gold image before deploying it into production. The tools and methods shown in this module can significantly benefit anyone in charge of systems administration, architecture, or internal security & compliance.

Like with any automation, there can be risks to using these tools. Though rare, performing excessive enumeration could cause system instability or issues with a system (or systems) that are already known to be fragile. Furthermore, these tools are well known, and most (if not all) of them will be detected and blocked by common anti-virus solutions, and most certainly, by more advanced EDR products such as Cylance or Carbon Black. Let's look at the latest release of the LaZagne tool at the time of writing version 2.4.3. Uploading the precompiled binary to Virus Total shows that 47/70 products detect it.

<img width="674" height="339" alt="image" src="https://github.com/user-attachments/assets/d2163996-f4d7-4179-a52b-98ac61314963" />

We likely would have been caught on the spot if we were attempting to run this during an evasive engagement. During other assessments, we may encounter protections that we need to bypass to run our tools. Though out of scope for this module, we can use a variety of methods to get our tools past common AV products, such as removing comments, changing function names, encrypting the executable, etc. These techniques will be taught in a later module. We will assume that our target client has temporarily set Windows Defender on the hosts we are assessing not to block our activities for this module. They are looking for as many issues as possible and are not looking to test their defenses at this stage in the game.

