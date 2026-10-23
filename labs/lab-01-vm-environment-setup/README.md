# Lab 01 — VM Environment Setup

**Course:** CYB623 — Network Security and Defense
**Goal:** Stand up a safe, reproducible security lab: install VirtualBox, deploy the pre-built SEED Ubuntu 20.04 VM, and get comfortable working at the Linux command line.

## Objectives

1. Inventory the host hardware and OS (useful later for troubleshooting).
2. Install Oracle VirtualBox with the Extension Pack.
3. Deploy the pre-built SEED Ubuntu 20.04 VM.
4. Practice core Linux commands: navigation, file creation, and network interface inspection.

## Host Environment

| Component | Value |
|-----------|-------|
| OS | macOS Monterey 12.7.6 |
| Model | MacBook Air (13-inch, 2017) |
| CPU | 1.8 GHz Dual-Core Intel Core i5 |
| RAM | 8 GB DDR3 |

The host meets the lab requirements: admin access, 4 GB+ RAM (8 GB recommended), and 20 GB+ free disk space.

## Step 1 — Install VirtualBox

Downloaded the latest VirtualBox for macOS hosts plus the matching Extension Pack from [Oracle's downloads page](https://www.oracle.com/virtualization/technologies/vm/downloads/virtualbox-downloads.html), installed the main application first, then added the Extension Pack on top.

## Step 2 — Deploy the SEED VM

Downloaded the pre-built SEED Ubuntu 20.04 VM from [seedsecuritylabs.org](https://seedsecuritylabs.org/labsetup.html) and imported it into VirtualBox following the [SEED VM manual](https://github.com/seed-labs/seed-labs/blob/master/manuals/vm/seedvm-manual.md) (including appendices A–C). Logged in with the standard SEED VM account.

## Step 3 — Linux Command-Line Fundamentals

All commands were run in the VM's terminal as the `seed` user.

### Home directory & navigation

```bash
echo $HOME      # /home/seed
cd ..           # move up one level
pwd             # confirm current directory
cd              # return home (also: cd $HOME)
```

`pwd` confirmed the home directory is `/home/seed` both before navigating away and after returning.

### Listing directory contents

```bash
ls -l
```

The home directory contains the standard Ubuntu user folders (`Desktop`, `Documents`, `Downloads`, `Music`, `Pictures`, `Public`, `Templates`, `Videos`):

![ls -l output showing the home directory contents](./assets/01-home-directory-listing.png)

### Creating a file

```bash
gedit testing.txt
ls
```

Created `testing.txt` with gedit and verified it appears in the home directory listing:

![gedit and ls output showing testing.txt was created](./assets/02-creating-a-file-with-gedit.png)

### Network interface inspection

```bash
sudo ifconfig
```

| Interface | IP Address |
|-----------|------------|
| `docker0` | 172.17.0.1 |
| `enp0s3` | 10.0.2.15 |

The VM also had working outbound web access from its browser, confirming NAT connectivity through the host.

## Cleanup

Shut the VM down cleanly via the power-off button (upper-right corner of the VM screen) rather than killing the process, so the disk image stays consistent.

## Takeaways

- Setting up VirtualBox + the SEED VM gives an isolated, snapshot-friendly environment for security work — nothing touches the host OS.
- Core navigation (`cd`, `pwd`, `ls`) and file creation (`gedit`) are now routine.
- One gotcha worth remembering: `cd..` (no space) fails with `command not found` — the correct form is `cd ..` with a space. Small syntax details matter at the command line.

## Acknowledgments

This lab is based on the [SEED Labs](https://seedsecuritylabs.org/) project (Wenliang Du, Syracuse University), used in coursework at Pace University.
