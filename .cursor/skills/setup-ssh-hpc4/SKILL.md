---
name: setup-ssh-hpc4
description: Guides SSH and project setup for HPC4 (hpc4.ust.hk). Split into "new computer" (login, VS Code remote) and "new project" (conda, GitHub, AWS, DVC). Use when setting up HPC4 access, connecting from a new machine, or starting a new project on the cluster.
---

# Set Up SSH for HPC4

Based on [Set up Project in HPC4 (Notion)](https://koheikawaguchi.notion.site/Set-up-Project-in-HPC4-6a06c88e7f6c477c8adc2becd7761a05). Do **new computer** steps once per machine; do **new project** steps once per project on the cluster.

---

# Essential logic (how SSH key login works)

- You have a **key pair** on your Mac: **private key** (stays on your Mac, never send it) and **public key** (you give a copy to the server).
- **HPC4 never sees your private key.** It only stores your **public** key in `~/.ssh/authorized_keys` in your account on the server. When you connect, the server uses the public key to verify that your Mac has the matching private key — without you typing a password.
- **First time (new computer):** You don’t have your public key on HPC4 yet, so you log in with **password + Duo**. Once in, you add your public key to `~/.ssh/authorized_keys` on HPC4 (paste the full line from `cat ~/.ssh/id_rsa.pub`). You do this once per machine.
- **Next time:** The server has your public key, so it can verify you with the key. You skip the password; you still do **Duo** (2FA) each time. So: key = no password, Duo = still required.

---

# New computer (do once per machine)

## 1. Log in to HPC4 (SSH)

**Have a key on your Mac:** If you don’t have one, create it: `ssh-keygen -t ed25519 -C "khsu@connect.ust.hk" -f ~/.ssh/id_ed25519` (or use existing `~/.ssh/id_rsa.pub`). Your **public** key is in `~/.ssh/id_rsa.pub` or `~/.ssh/id_ed25519.pub`.

**Optional — SSH config:** Add to `~/.ssh/config` so you can type `ssh hpc4`:
```text
Host hpc4
    HostName hpc4.ust.hk
    User khsu
    IdentityFile ~/.ssh/id_rsa
```

**First-time login (password + Duo):**
1. Run `ssh khsu@hpc4.ust.hk` (or `ssh hpc4`). First time only: type **yes** at the host key prompt.
2. Enter your HPC4 **password** when prompted.
3. At Duo: type **1** (Push) or **2** (SMS) or enter a passcode. After “Success. Logging you in...” you are on the cluster.

**Add your public key so next time you skip the password:**
1. On your Mac: `cat ~/.ssh/id_rsa.pub` — copy the **entire** line (from `ssh-rsa` through the comment at the end).
2. On HPC4: `nano ~/.ssh/authorized_keys` — paste the line on a new line (one line, no break in the middle). Save: **Ctrl+O**, Enter, then **Ctrl+X** to exit.
3. Run `chmod 600 ~/.ssh/authorized_keys` on HPC4.

Next time you run `ssh khsu@hpc4.ust.hk` you’ll only need **Duo** (no password).

---

## 5. Set up VS Code / Cursor with Remote SSH

**Goal:** Edit files and run terminals on HPC4 from VS Code or Cursor (SSH remote).

1. **Install extension:** Extensions (Ctrl+Shift+X / Cmd+Shift+X) → search **Remote - SSH** (Microsoft) → Install.
2. **Connect:** Ctrl+Shift+P (or Cmd+Shift+P) → **Remote-SSH: Connect to Host...** → choose **hpc4** from the list (if you have `~/.ssh/config`). Or **+ Add New SSH Host...** and enter `ssh khsu@hpc4.ust.hk`, then select the new host.
3. **Login:** A new window opens; a terminal in the editor shows the SSH session. Complete **Duo** (e.g. type **1** for Push). When prompted to install the VS Code Server on the host, choose **Yes**.
4. **Open folder:** File → Open Folder... → enter path on HPC4 (e.g. `/home/khsu/projects/RSI`) → OK. Sidebar shows the remote project.
5. **Terminal:** Terminal → New Terminal (Ctrl+` / Cmd+`) — that shell runs on HPC4. You’ll see **SSH: hpc4** (or your host) in the bottom-left when connected.

See Notion “Set up VScode with Remote Tunneling Extensions” if you use Remote - Tunnels instead. RSI jobs: [hpc4-execution](.cursor/skills/hpc4-execution/SKILL.md).

---

# New project (do once per project on cluster)

## 2. Conda environment and software

Follow Notion “Create Conda Environment and Download Software”. For RSI: use **rsi_clio** env and [hpc4-execution](.cursor/skills/hpc4-execution/SKILL.md) for installing the RSI package.

## 3. GitHub and AWS

**GitHub:** Notion “GitHub Connection and AWS Configure”. **AWS:** On HPC4, `aws configure --profile clio` (with conda env active if needed); region `ap-northeast-1`. Verify: `aws s3 ls s3://rsi-khsu/ --profile clio`. See [hpc4-execution](.cursor/skills/hpc4-execution/SKILL.md).

## 4. Avoid Spack for DVC

Follow Notion “Avoid Spack Environment for DVC” so DVC uses your conda environment.

---

# Quick reference

| Step | When |
|------|------|
| 1. Log in HPC4, add public key to `authorized_keys` | **New computer** |
| 5. VS Code Remote SSH | **New computer** |
| 2. Conda + software | New project |
| 3. GitHub + AWS | New project |
| 4. Avoid Spack for DVC | New project |

**Notion:** https://koheikawaguchi.notion.site/Set-up-Project-in-HPC4-6a06c88e7f6c477c8adc2becd7761a05  

**RSI runs/SLURM:** [hpc4-execution](.cursor/skills/hpc4-execution/SKILL.md)
