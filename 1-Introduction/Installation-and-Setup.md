# Installation and Setup of Metasploit

This guide helps you set up Metasploit on various platforms for penetration testing.

## Supported Platforms
- Linux (Debian-based distributions like Kali Linux and Ubuntu)
- Windows
- macOS
- Docker

## Installation Instructions
### Linux (Kali/Ubuntu)
1. Update the package list:

    ```
    sudo apt update
    ```
2. Install Metasploit:
    ```
    sudo apt install metasploit-framework
    ```
3. Verify installation:
    ```
    msfconsole --version
    ```
### Windows
  - Download the installer from Rapid7's website.
  - Run the installer and follow the wizard.
  - Launch msfconsole from the command prompt.

### macOS

Use Homebrew to install Metasploit:

    brew install metasploit-framework
    Verify installation:
    msfconsole --version

### Docker
Pull the Metasploit Docker image:
    
    docker pull metasploitframework/metasploit-framework

Run Metasploit:

    docker run -it metasploitframework/metasploit-framework

# Post-Installation Configuration

Initialize the database:
    
    msfdb init

Update Metasploit to the latest version:
    
    msfupdate

# Troubleshooting Installation Issues

- Missing dependencies on Linux: Use ```sudo apt --fix-broken install```.
- Database connection errors: Ensure PostgreSQL service is running.
- Testing installation: Run the command msfconsole to confirm successful installation.
