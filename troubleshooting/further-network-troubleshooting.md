# SSH and Network Troubleshooting

## Overview

After system updates and reboots, the Ubuntu server became unreachable over SSH from my laptop. This document outlines the troubleshooting process used to diagnose and restore network connectivity and remote access.

The issue helped develop a better understanding of:

- Linux networking
- SSH connectivity
- DHCP and IP addressing
- Netplan configuration
- Remote server management

---

# Symptoms

The server became inaccessible remotely after rebooting.

Issues observed included:

- SSH connection failures
- Ping requests initially returning:

```bash
Host unreachable
```

- Loss of remote management access
- Requirement for direct local access to investigate further

---

# Initial Diagnostics

## 1. Verified Physical Connectivity

The following checks were completed first:

- Server power state
- Ethernet connection
- Router connectivity
- Network interface link lights

This confirmed the issue was likely software or network configuration related rather than physical hardware failure.

---

# Network Testing

## 2. Ping Testing

From the laptop, connectivity tests were performed using:

```bash
ping <server-ip>
```

Initially, the server could not be reached.

After additional troubleshooting, ping responses later succeeded, confirming:

- The server was online
- The network path existed
- The device was reachable over the LAN

However, SSH access was still inconsistent.

---

# Verifying IP Configuration

## 3. Checking the Server IP Address

The server IP configuration was checked locally using:

```bash
ip a
```

This confirmed the server had received a local IP address from the router.

At this stage, the issue appeared to be related to network configuration rather than complete network failure.

---

# Netplan Investigation and Fix

## 4. Investigating Network Configuration

Further troubleshooting identified the issue as potentially relating to Ubuntu’s network configuration.

Ubuntu Server uses **Netplan** to manage networking through YAML configuration files.

The configuration files are located in:

```bash
/etc/netplan/
```

The directory contents were checked using:

```bash
cd /etc/netplan
ls
```

The network configuration file was then edited using:

```bash
sudo nano <config-file>.yaml
```

The configuration was reviewed to ensure:

- The correct network interface was configured
- DHCP was enabled correctly
- Network settings were being applied properly after reboot

---

# Applying the Configuration

## 5. Applying Network Changes

After editing the configuration, the updated settings were applied using:

```bash
sudo netplan apply
```

This restarted and applied the networking configuration without requiring a full reinstall or rebuild.

---

# Restoring SSH Access

## 6. Testing Remote Access

Once the network configuration had been corrected, SSH connectivity was tested again:

```bash
ssh username@server-ip
```

SSH access successfully returned after the networking issue was resolved.

---

# What I Learned

## Linux Networking

This troubleshooting process improved understanding of:

- DHCP and IP assignment
- Linux networking services
- Netplan YAML configurations
- Network interface configuration
- Remote server management

---

## SSH Dependencies

I also learned that SSH access depends on multiple components working correctly, including:

- The server being powered on
- Network services initializing correctly
- A valid IP address being assigned
- The SSH service running properly

---

## Reboot Behaviour

The issue also demonstrated that after reboots:

- Networking services may take time to initialize
- DHCP may reassign IP addresses
- Remote services such as SSH can temporarily fail until networking stabilizes

---

# Outcome

- Restored SSH connectivity to the Ubuntu server
- Corrected the server networking configuration
- Improved understanding of Linux networking and remote administration
- Gained practical experience troubleshooting real-world server connectivity issues
