# OS Security Settings Guide

Virginia Tech requires all Linux machines to meet minimum security standards. This guide covers how to audit and harden your machines.

---

## Resources

| Resource | Link |
|----------|------|
| CS Security Guide | https://wiki.cs.vt.edu/wiki/CS_Security_Guide |
| Linux Audit Scripts | https://version.cs.vt.edu/techstaff/linux-audit |
| Hardening Script | https://version.cs.vt.edu/rhunter/cs-linux-hardening-script |

---

## Applying Security Standards

### Step 1: Audit Current State

Run the [linux-audit](https://version.cs.vt.edu/techstaff/linux-audit) scripts to check compliance with VT minimum standards.

### Step 2: Run Hardening Script

Use the [cs-linux-hardening-script](https://version.cs.vt.edu/rhunter/cs-linux-hardening-script) to automatically apply security settings.

---

## Notes on Hardening Script

The script will prompt for additional firewall ports:

```
If you have another port that need access enter the port number
(Press Enter if none):
```

- Port 22 (SSH) is enabled by default
- Add any other ports your services require
- This prompt appears at line 47 in `linux_security_update.sh`

---

## Common Ports to Consider

| Port | Service | Notes |
|:----:|---------|-------|
| 22 | SSH | Default, always enabled |
| 80 | HTTP | Web server |
| 443 | HTTPS | Secure web server |
| Custom | Research services | As needed |

---

## Questions?

Contact VT CS Tech Staff: techstaff@cs.vt.edu
