## Overview

After system reboots, server became unreachable over ssh from my laptop. This documents the troubleshooting process used to restore network connection and understand the underlying networking behaviour.

---

# Issues

- ssh connection failed
- ping requests initially returned: host unreachable


- server appeared offline from the network
- required investigation directly on the server

---

# Troubleshooting Process

## 1. Verified Physical State

Checked:

- server power state
- ethernet connection
- router connectivity
- lights on the physcial ethernet port on the pc

---

## 2. Tested Network Connectivity

From laptop:

```
ping server-ip
```

Initially failed, then later succeeded after the server reconnected to the network.

This confirmed:

- Network path existed
- Server was reachable again
- Issue was likely related to boot/network initialization

---

## 3. Verified Server IP

Checked Ubuntu server IP locally:

```bash
ip a
```

Confirmed the server had received a valid lan ip address.

---

## 4. Tested SSH Access

Attempted ssh again:

```bash
ssh username@server-ip
```

SSH access returned successfully after network recovery.

---

# What I Learned

## SSH depends on multiple services

SSH only works if:

- Server is powered on
- Network is active
- SSH service is running
- Correct IP address is used

---

## Reboots can temporarily interrupt networking

After reboots:

- DHCP may assign IPs again
- Network services may take time to initialize
- SSH cannot work until networking is fully online

---

## Existing SSH sessions remain active

I also learned that:

- Existing SSH sessions can sometimes remain active during certain network interruptions
- New SSH sessions may fail until networking stabilizes

---

# Outcome

- Restored SSH connectivity
- Improved understanding of Linux networking and remote management
- Better understanding of how SSH, networking, and server boot processes interact
