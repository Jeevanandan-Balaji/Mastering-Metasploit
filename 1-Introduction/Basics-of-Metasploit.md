# Basics of Metasploit

The Metasploit Framework consists of several components that enable penetration testing, vulnerability scanning, and post-exploitation.

## Key Components
- **Msfconsole**: The command-line interface for interacting with Metasploit.
- **Modules**:
  - Exploits: Attack code targeting specific vulnerabilities.
  - Payloads: Code executed on a target system after exploitation.
  - Auxiliary: Tools for scanning, fingerprinting, and network attacks.
  - Post-Exploitation: Tools to maintain access and gather information.
- **Encoders**: Obfuscate payloads to bypass detection.
- **Nops**: Ensure payload stability.

## Basic Workflow
1. **Start Metasploit**:

         msfconsole
3.  Search for a Module:

         Search <keyword>

3. Use a Module:

        use <module-path>

4. Set Required Options:

       set RHOST <target-IP>
       set LHOST <attacker-IP>

5. Run the Exploit:

       exploit

## Example: Scanning a Target

    use auxiliary/scanner/portscan/tcp
    set RHOSTS <target-IP>
    run


Workspaces

Organize projects using workspaces:

    workspace add <workspace-name>
    workspace <workspace-name>

Practical Tips

- Test in isolated environments (e.g., virtual machines).
- Regularly update modules using msfupdate.
- Use help or info commands to learn about modules.

