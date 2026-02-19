# CloudLab Guide

CloudLab provides bare-metal servers for systems research experiments.

---

## Quick Reference

| Field | Value |
|-------|-------|
| **URL** | https://cloudlab.us |
| **Project** | nestfarm |
| **Resource Availability** | https://www.cloudlab.us/resinfo.php |
| **Group Profile** | [p5](https://github.com/MoatLab/cloudLabProfile) |

---

## Getting Started

### Step 1: Sign Up

1. Create an account at [cloudlab.us](https://cloudlab.us/)
2. Request to join project: **nestfarm**
3. Wait for approval (usually 1-2 days)

### Step 2: Configure SSH

SSH keys are required to access CloudLab machines.

| Step | Command |
|:----:|---------|
| 1 | Check if you have a key: `ls ~/.ssh/id_rsa.pub` |
| 2 | If not, generate one: `ssh-keygen` |
| 3 | View your public key: `cat ~/.ssh/id_rsa.pub` |
| 4 | Add to CloudLab: [Login](https://www.cloudlab.us/login.php) → Profile → Manage SSH Keys |

---

## Starting an Experiment

### Step-by-Step

| Step | Section | Action |
|:----:|---------|--------|
| 1 | Go to | `Experiments → Start Experiment` |
| 2 | Profile | Click "Change Profile" → Select **p5** (or custom) |
| 3 | Parameters | Configure nodes, OS, machine type |
| 4 | Finalize | (Optional) Name your experiment |
| 5 | Schedule | Click Finish to start immediately |

### Parameter Options

| Parameter | Recommendation |
|-----------|----------------|
| **Machine Type** | c220g5 (good default) |
| **OS** | Ubuntu 20.04 or 22.04 |
| **Temp Storage** | Max 1024GB, mounted at `/tdata` |

> **Note:** Temporary storage mounts at `/tdata`, NOT your home directory!

### Accessing Your Experiment

After the experiment starts (may take several minutes):

```bash
# Example SSH command (from List View tab)
ssh -p 22 username@c220g5-111327.wisc.cloudlab.us
```

---

## Tips

- [Check resource availability](https://www.cloudlab.us/resinfo.php) before starting experiments
- c220g5 machines at Wisconsin are generally available
- Extend experiments before they expire to avoid losing work
- Use tmux to keep sessions alive during disconnections
