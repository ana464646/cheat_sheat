# Penetration Testing Cheat Sheet

This repository is a collection of command references for various tools used in penetration testing.
For educational purposes only.

## Directory Structure

### Initial Phase (01-02)
- **01_Reconnaissance**: Reconnaissance phase tools
  - nmap.md (Windows/Linux/macOS)
  - masscan.md (Linux)
  - dnsrecon.md (Linux/Python)
  - theharvester.md (Linux/Python)
  - gobuster.md (Linux)
  - wpscan.md (Linux/Ruby)
  - nikto.md (Linux/Perl)
  - smbmap.md (Linux/Python)
- **02_Initial_Access**: Initial access phase tools
  - metasploit.md (Linux preferred, Windows possible)
  - set.md (Linux)
  - powersploit.md (Windows)

### Persistence Phase (03-06)
- **03_Privilege_Escalation**: Privilege escalation tools
  - Linux/
    - linpeas.md
  - Windows/
    - winpeas.md
- **04_Persistence**: Persistence tools
  - Linux/
  - Windows/
- **05_Defense_Evasion**: Defense evasion tools
  - Linux/
  - Windows/
- **06_Credential_Access**: Credential access tools
  - Linux/
  - Windows/

### Movement Phase (07-08)
- **07_Lateral_Movement**: Lateral movement tools
  - Linux/
  - Windows/
    - mimikatz.md
- **08_Collection**: Data collection tools
  - Linux/
  - Windows/

### Advanced Techniques (09-20)
- **09_Active_Directory_Attacks**: Active Directory attack tools
  - Linux/
  - Windows/
    - bloodhound.md
- **15_Wireless_Attacks**: Wireless attack tools
  - Linux/
  - Windows/
- **16_Web_Application**: Web application attack tools
  - Linux/
  - Windows/
- **17_Mobile_Analysis**: Mobile application analysis tools
  - Linux/
  - Windows/
- **18_Reverse_Engineering**: Reverse engineering tools
  - Linux/
  - Windows/
- **19_Malware_Analysis**: Malware analysis tools
  - Linux/
  - Windows/
- **20_IoT_Security**: IoT security tools
  - Linux/
  - Windows/

## How to Use

1. Each tool's markdown file contains the following information:
   - Compatible operating systems
   - Basic usage
   - Commonly used options
   - Advanced configuration options
   - Important notes and cautions

2. Navigate to the documentation for the tool you need and refer to the relevant operation information.

## Important Notes

- This repository is for educational purposes only
- Use the tools only in authorized environments
- Usage in production environments may carry legal responsibilities
- All tools are to be used at your own risk

## Contributing

- Please submit bug reports and new tool additions via Issues/Pull Requests
- Documentation improvement suggestions are welcome

## License

This project is released under the MIT License.
