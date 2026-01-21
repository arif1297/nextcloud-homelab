# Issue: No Internet Connection After Ubuntu Installation

## Issues Observed
- Ethernet cable was connected to the server
- No internet access after installing Ubuntu Server
- Commands requiring internet access failed

## Investigation
Checked whether the network interface was detected and had an IP address:
ip link
ip addr

Confirmed default route was missing
ip route

Pinged Google to check no internet connection
ping 8.8.8.8

## Resolution
Manually enabled ehthernet interface
sudo ip link set eth0 up

Testing internet connection
ping 8.8.8.8

## Outcome
The Ethernet interface became active
Internet connectivity was restored
The server was able to download updates and packages successfully
Was able to continue configuring the server

