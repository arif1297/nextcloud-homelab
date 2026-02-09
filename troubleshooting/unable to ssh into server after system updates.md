# Issue: Unable to SSH into server after system updates

## Issues Observed
- SSH access failed after rebooting the server following system updates
- Error returned: `No route to host`
- Server was powered on but unreachable over the network
- No internet access on the server
- Ethernet LEDs only active during reboot, then turned off

---

## Investigation

Attempted SSH connection from another device:
```bash
ssh user@<server-ip>
```

Checked whether the network interface was detected and active:
