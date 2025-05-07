# Notes: A Peek at Some More Advanced Topics (Section 5)

## Find Information about your Linux Distribution (Video 1)

```bash
ls -l /etc/*release
cat /etc/*release

uname -a
```

## Find System Hardware and Disk Information (Video 2)

```bash
free -h

cat /proc/cpuinfo

lscpu

df -h

sudo du -hd1 /
```

## Install and Update Software with a Package Manager (Video 3)

### Package Managers

1. Advanced Package Tool (APT): Ubuntu, Mint, Debian, etc.
2. Yum: Red Hat, CentOS
3. DNF: Red Hat and Fedora
4. YaST: SUSE
5. pacman: Arch

All PMs allow user to search for, install, remove, and update packages

```bash
apt search tree
apt show tree

sudo apt update
sudo apt install tree

tree

man tree

sudo apt update
sudo apt upgrade
```
