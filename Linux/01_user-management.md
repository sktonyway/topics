# Linux User Management

I was trying to share an instance with multiple user access, so needed to learn these concepts

- Linux user creation, deletion, changing it provided permissions``

## Networking Commands

### Core Diagnostic & Path Commands

- `ping`: Transmits and receives ICMP packets to verify host reachability.
- `netstat`: Displays active network connections, routing tables, and interface statistics.
- `ifconfig`: Displays and configures active network interfaces like eth0 or docker.
- `traceroute <url>`: Traces and displays every network hop taken to reach a destination.
- `tracepath <url>`: Traces the network path while mapping MTU values and hop IPs.
- `mtr`: Combines ping and traceroute into a live, real-time diagnostic stream.

### Domain, Lookup & Info Commands

- `nslookup`: Queries internet name servers to find IP addresses or DNS records.
- `dig`: Performs flexible DNS lookups and prints detailed domain server responses.
- `whois`: Queries global databases for domain ownership and registration info.
- `hostname`: Displays or alters the system's current network name.


### Connectivity & Port Testing Commands

- `telnet`: Connects to a remote host over a specific port via plaintext.
- `nc`: Reads and writes data across network connections using TCP or UDP.
- `curl`: Transfers data to or from a server using various application protocols.
- `wget`: Downloads files from web or FTP servers non-interactively in backgrounds.

### Hardware, Wireless & Status Commands


- `ip`: Modern replacement for ifconfig to manage routing, devices, and policies.
- `iwconfig`: Configures and views wireless network interfaces and signal parameters.
- `ipconfig`: Displays and flushes network interface profiles on Windows operating systems.
- `ifplugstatus`: Detects whether a physical Ethernet cable is plugged into a port.
- `arp`: Displays and alters the local IPv4-to-MAC hardware address mapping cache.

### Security, Monitoring & Routing Commands


- `iptables`: Configures the Linux kernel's built-in packet filtering and firewall rules.
- `nmap`: Scans remote hosts to discover open ports and running services.
- `route`: Displays and alters the system's static IP routing table entries.
- `watch`: Runs any command repeatedly at intervals to monitor live output changes.