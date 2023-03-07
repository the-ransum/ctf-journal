# Notes


## Workflow Process

1. **Reconnaissance**
   - Identify the target system and its IP address.
   - Determine the operating system and software running on the system.
   - Conduct port scanning to identify open ports and services.
   - Conduct network mapping to determine the network topology.
   - Search for any publicly available information about the target system or organization.
2. **Enumeration**
   - Use tools like Nmap, Dirb, or Nikto to identify hidden files, directories, or vulnerabilities.
   - Gather information about user accounts and passwords.
   - Determine the software versions and configurations of the target system.
   - Identify any weak points or misconfigurations in the system.
3. **Exploitation**
   - Use a pre-existing exploit or develop a custom exploit to gain access to the target system.
   - Test the exploit on a sandbox environment to ensure it works as expected.
   - Use social engineering techniques to trick users into revealing sensitive information or granting access to the system.
4. **Privilege Escalation**
   - Identify the user privileges and permissions on the system.
   - Use privilege escalation techniques to gain higher-level access to the system.
   - Exploit any misconfigured permissions or system weaknesses to escalate privileges.
5. **Maintaining Access**
   - Create a backdoor to maintain access to the system even after logging out.
   - Establish a persistent connection to the system to maintain access.
   - Use rootkits or other stealthy techniques to avoid detection.
6. **Covering Tracks**
   - Delete any logs or evidence of your presence on the system.
   - Cover your tracks by modifying timestamps or other system information.
   - Remove any backdoors or other access points that you have created.


## Tools

- **Nmap**: A network exploration and port scanning tool.
- **Shodan**: A search engine for discovering internet-connected devices.
- **Recon-ng**: A reconnaissance framework that can be used for information gathering and OSINT.
- **theHarvester**: A tool for gathering email accounts, subdomains, hosts, employee names, open ports, and banners from different public sources (search engines, PGP key servers).
- **Dirb**: A web content scanner used to find hidden web objects.
- **Nikto**: A web server scanner designed to scan for web server vulnerabilities and misconfigurations.
- **Enum4linux**: A tool for enumerating user accounts and passwords from a Windows or Samba server.
- **Enumerate Users**: A script to enumerate Windows user accounts and groups from a target domain.
- **Metasploit Framework**: A powerful tool used for developing and executing exploits against remote targets.
- **Burp Suite**: A web application penetration testing tool that can be used to identify vulnerabilities in web applications.
- **SQLMap**: A SQL injection exploitation tool that automates the process of detecting and exploiting SQL injection flaws.
- **LinEnum**: A script used to enumerate Linux systems and identify privilege escalation vectors.
- **Windows-Exploit-Suggester**: A script that compares a Windows system's patch level against a database of known vulnerabilities and suggests exploits.
- **Mimikatz**: A tool for extracting plaintext passwords and hashes from Windows memory.
- **Sudo_killer**: A tool that can identify misconfigured sudoers file permissions and exploit them for privilege escalation.
- **Netcat**: A tool for establishing a persistent connection to a remote system.


| Tool | Description | Sample Commands |
| --- | --- | --- |
| Nmap | Network exploration and port scanning tool. | `nmap -sS targetIP` (TCP SYN scan), `nmap -sU targetIP` (UDP scan), `nmap -A targetIP` (Aggressive scan) |
| Shodan | Search engine for discovering internet-connected devices. | `shodan search apache` (Search for Apache web servers), `shodan host targetIP` (Get detailed information about a host) |
| Recon-ng | Reconnaissance framework for information gathering and OSINT. | `recon-ng` (Launch the framework), `recon-ng> use recon/domains-hosts/bing_domain_web` (Use a module), `recon-ng> show options` (View available options) |
| theHarvester | Tool for gathering email accounts, subdomains, hosts, employee names, open ports, and banners from different public sources. | `theHarvester -d example.com -l 500 -b all` (Search for information about a domain), `theHarvester -d example.com -b bing` (Search for information using Bing search engine) |
| Dirb | Web content scanner used to find hidden web objects. | `dirb http://targetIP/` (Scan a website), `dirb -o output.txt http://targetIP/` (Save the output to a file) |
| Nikto | Web server scanner designed to scan for web server vulnerabilities and misconfigurations. | `nikto -h targetIP` (Scan a web server), `nikto -update` (Update Nikto's database) |
| Enum4linux | Tool for enumerating user accounts and passwords from a Windows or Samba server. | `enum4linux -a targetIP` (Enumerate all available information), `enum4linux -u username -p password targetIP` (Specify username and password) |
| Enumerate Users | Script to enumerate Windows user accounts and groups from a target domain. | `enumerate-users -U -G -S -D domainController -u username -p password` (Enumerate users, groups, and shares on a domain controller) |
| Metasploit Framework | Powerful tool used for developing and executing exploits against remote targets. | `msfconsole` (Launch the framework), `msfconsole> use exploit/multi/handler` (Use a handler), `msfconsole> set PAYLOAD windows/meterpreter/reverse_tcp` (Specify the payload) |
| Burp Suite | Web application penetration testing tool that can be used to identify vulnerabilities in web applications. | `burpsuite` (Launch the tool), `Target > Site map` (View the site map), `Target > Scope` (Configure the scope) |
| SQLMap | SQL injection exploitation tool that automates the process of detecting and exploiting SQL injection flaws. | `sqlmap -u "http://targetIP/page.php?id=1"` (Detect SQL injection), `sqlmap -u "http://targetIP/page.php?id=1" --dump` (Dump the database contents) |
| LinEnum | Script used to enumerate Linux systems and identify privilege escalation vectors. | `./LinEnum.sh -t` (Run a thorough scan), `./LinEnum.sh -k password` (Search for passwords) |
| Windows-Exploit-Suggester | Script that compares a Windows system's patch level against a database of known vulnerabilities and suggests exploits. | `windows-exploit-suggester.py --update` (Update the database), `windows-exploit-suggester.py


## Nmap

```bash
$ nmap -sV HOSTNAME
$ nmap -p- -sV HOSTNAME
$ nmap -p1-1000 -sV HOSTNAME
$ nmap -p- --max-rate=5000 -sV HOSTNAME
```


## Webservers

Directory Brute Forcing

```bash
$ gobuster dir -w /usr/share/wordlists/dirb/common.txt -x .php,.html,.txt -u HOSTNAME -o ./gobuster.txt
```

**or**

```bash
$ dirb HOSTNAME /usr/share/dirb/wordlists/common.txt -w -X .php,.html,.txt
```

Vulnerability Searching
```bash
$ nikto -h HOSTNAME -output ./nikto.txt
```

Fuzzing
```bash
$ wfuzz -c -z file,/usr/share/wfuzz/wordlist/general/common.txt --hc 400,404,403 -u 'http://HOSTNAME/help.php' -d 'page=Fuzz'
```


## Metasploit

Metasploit initial startup
```bash
$ msfdb init
```

Start the metasploit console
```bash
$ msfconsole -q
```

---

## Unorganized
```
sublist3r -d domain.tld -t 3 -e google
```

```
gobuster dns -d domain.tld -w /usr/share/wordlists/amass/subdomains.lst -o gobuster.subdomains.txt
```

```
wfuzz -c -f sub-fighter.txt -Z -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt --sc 200,202,204,301,302,307,403 domain.tld
```
