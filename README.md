# Dhiraagu SIP Trunk Static Route Generator

A web-based tool to generate static route commands for Dhiraagu SIP trunk configurations across multiple operating systems.

![Dhiraagu SIP Trunk Static Route Generator](https://www.dhiraagu.com.mv/themes/custom/dhiraagu/logo.svg)

## Overview

This utility helps network administrators and VoIP technicians quickly generate the necessary static route commands to properly configure SIP trunks with Dhiraagu, the primary telecommunications provider in the Maldives.

The tool generates appropriate routing commands for various operating systems:

- **Windows**: Route commands for Windows command prompt
- **Linux**: Commands for Debian/Ubuntu, CentOS/RHEL, and FreeBSD

## Features

- **Multi-Platform Support**: Generate commands for Windows and various Linux distributions
- **Domain Validation**: Automatically validates Dhiraagu SIP server domains
- **Permanent Route Generation**: Instructions for creating persistent routes that survive reboots
- **Copy to Clipboard**: One-click copying of commands
- **Mobile Responsive**: Works on desktop and mobile devices

## Usage Instructions

1. Visit the appropriate page for your operating system (Windows or Linux)
2. For Linux, select your distribution from the dropdown menu
3. Enter your network details:
   - PBX IP address
   - Gateway IP address
   - SIP Server (domain will be validated against Dhiraagu domains)
   - Additional details as required by your OS
4. Click "Generate Routes" to create the commands
5. Copy the commands to your clipboard and execute them on your system

## Supported Configurations

### Windows

Generates persistent route commands with the `-p` flag:
```
route add -p 172.18.0.0 mask 255.255.0.0 [GATEWAY] metric 1
route add -p 172.31.0.0 mask 255.255.0.0 [GATEWAY] metric 1
```

### Linux Distributions

#### Debian/Ubuntu
```
ip route add 172.18.0.0/16 via [GATEWAY] metric 1
ip route add 172.31.0.0/16 via [GATEWAY] metric 1
```

#### CentOS/RHEL
Temporary routes:
```
ip route add 172.18.0.0/16 via [GATEWAY] dev [INTERFACE]
ip route add 172.31.0.0/16 via [GATEWAY] dev [INTERFACE]
```

Permanent routes (in `/etc/sysconfig/network-scripts/route-[INTERFACE]`):
```
# Static routes for Dhiraagu SIP Trunk
172.18.0.0/16 via [GATEWAY] dev [INTERFACE]
172.31.0.0/16 via [GATEWAY] dev [INTERFACE]
```

#### FreeBSD
Temporary routes:
```
route add -net 172.18.0.0/16 [GATEWAY]
route add -net 172.31.0.0/16 [GATEWAY]
```

Permanent routes (in `/etc/rc.conf`):
```
# Static routes for Dhiraagu SIP Trunk
static_routes="dhiraagu_subnet1 dhiraagu_subnet2"
route_dhiraagu_subnet1="-net 172.18.0.0/16 [GATEWAY]"
route_dhiraagu_subnet2="-net 172.31.0.0/16 [GATEWAY]"
```

## Technical Details

The application is built with:
- HTML5
- CSS (Tailwind CSS)
- JavaScript (Vanilla)

No server-side components or databases are required - this is a purely client-side tool.

## License

This project is open source and available for use by Dhiraagu customers and partners.

## Author

Created by [Dvexter](https://github.com/Dvexter)