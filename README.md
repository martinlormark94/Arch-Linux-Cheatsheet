# Arch Linux Cheat Sheet

A practical Linux and Arch Linux command reference.

Made by myself, for myself, as a reference guide while learning Linux.

> **Important:** Arch Linux does not support partial upgrades. For normal system updates, use:
>
> ```bash
> sudo pacman -Syu
> ```

---

# 1. Navigation

## `pwd`

**Syntax**

```bash
pwd
```

**Example**

```bash
pwd
```

**Description**
Print the full path of the directory you are currently in.

---

## `cd`

**Syntax**

```bash
cd <directory>
```

**Examples**

```bash
cd /etc
cd ..
cd ~
cd -
```

**Description**
Change directory.

* `..` = one directory up
* `~` = home directory
* `-` = previous directory

---

## `ls`

**Syntax**

```bash
ls -lah <directory>
```

**Example**

```bash
ls -lah /etc
```

**Description**
List files and directories.

* `-l` = detailed list
* `-a` = include hidden files
* `-h` = human-readable file sizes

---

## `tree`

**Syntax**

```bash
tree -a -L <depth> <directory>
```

**Example**

```bash
tree -a -L 2 ~/.config
```

**Description**
Display directories and files as a tree.

---

# 2. Reading Files

## `cat`

**Syntax**

```bash
cat <file>
```

**Example**

```bash
cat /etc/os-release
```

**Description**
Print the entire contents of a file.

Best for short files.

---

## `less`

**Syntax**

```bash
less <file>
```

**Example**

```bash
less /var/log/pacman.log
```

**Description**
Read larger files interactively.

Useful keys:

```text
/text    Search
n        Next result
N        Previous result
q        Quit
```

---

## `head`

**Syntax**

```bash
head -n <number> <file>
```

**Example**

```bash
head -n 20 /etc/passwd
```

**Description**
Show the first lines of a file.

---

## `tail`

**Syntax**

```bash
tail -n <number> <file>
```

**Example**

```bash
tail -n 50 /var/log/pacman.log
```

**Description**
Show the last lines of a file.

---

## `tail -f`

**Syntax**

```bash
tail -f <file>
```

**Example**

```bash
tail -f /var/log/pacman.log
```

**Description**
Follow a file and display new lines as they are written.

---

# 3. Files and Directories

## `touch`

**Syntax**

```bash
touch <file>
```

**Example**

```bash
touch test.txt
```

**Description**
Create an empty file.

---

## `mkdir`

**Syntax**

```bash
mkdir -p <directory>
```

**Example**

```bash
mkdir -p ~/projects/linux/scripts
```

**Description**
Create a directory.

`-p` also creates missing parent directories.

---

## `cp`

**Syntax**

```bash
cp -av <source> <destination>
```

**Example**

```bash
cp -av ~/.config/konsole ~/backup/
```

**Description**
Copy files or directories.

* `-a` = preserve attributes and copy recursively
* `-v` = verbose output

---

## `mv`

**Syntax**

```bash
mv -iv <source> <destination>
```

**Example**

```bash
mv -iv old.txt new.txt
```

**Description**
Move or rename files.

* `-i` = ask before overwriting
* `-v` = verbose

---

## `rm`

**Syntax**

```bash
rm -i <file>
```

**Example**

```bash
rm -i test.txt
```

**Description**
Delete a file.

---

## Remove a directory

**Syntax**

```bash
rm -rI <directory>
```

**Example**

```bash
rm -rI old-directory/
```

**Description**
Delete a directory recursively.

Be especially careful with:

```bash
rm -rf
```

---

## `ln`

**Syntax**

```bash
ln -s <target> <link>
```

**Example**

```bash
ln -s /mnt/data ~/data
```

**Description**
Create a symbolic link.

---

# 4. Finding Things

## `find`

**Syntax**

```bash
find <path> -type f -iname "<pattern>"
```

**Example**

```bash
find ~ -type f -iname "*.conf"
```

**Description**
Recursively search for files.

* `-type f` = files
* `-type d` = directories
* `-iname` = case-insensitive name search

---

## Find directories

**Example**

```bash
find ~ -type d -iname "Steam"
```

---

## `command -v`

**Syntax**

```bash
command -v <command>
```

**Example**

```bash
command -v python
```

**Description**
Show which executable or shell command will run.

---

## `whereis`

**Syntax**

```bash
whereis <command>
```

**Example**

```bash
whereis bash
```

**Description**
Locate binaries, source files and manual pages.

---

## `type`

**Syntax**

```bash
type <command>
```

**Example**

```bash
type cd
```

**Description**
Show whether something is a binary, alias, function or shell builtin.

---

# 5. Searching Text

## `grep`

**Syntax**

```bash
grep -in "<text>" <file>
```

**Example**

```bash
grep -in "error" logfile.txt
```

**Description**
Search for text inside files.

* `-i` = ignore case
* `-n` = show line number

---

## Recursive grep

**Syntax**

```bash
grep -Rin "<text>" <directory>
```

**Example**

```bash
grep -Rin "nvidia" /etc/
```

**Description**
Search through files recursively.

---

## Multiple patterns

**Syntax**

```bash
grep -Ei 'pattern1|pattern2'
```

**Example**

```bash
sudo dmesg -T | grep -Ei 'error|failed|warning'
```

---

# 6. Pipes and Redirection

## Pipe

**Syntax**

```bash
<command1> | <command2>
```

**Example**

```bash
ps aux | grep firefox
```

**Description**
Send the output of one command into another command.

---

## `>`

**Syntax**

```bash
<command> > <file>
```

**Example**

```bash
ip addr > network.txt
```

**Description**
Write output to a file.

Existing contents are overwritten.

---

## `>>`

**Syntax**

```bash
<command> >> <file>
```

**Example**

```bash
date >> log.txt
```

**Description**
Append output to the end of a file.

---

## `tee`

**Syntax**

```bash
<command> | tee <file>
```

**Example**

```bash
ip addr | tee network.txt
```

**Description**
Display output and save it to a file simultaneously.

Especially useful with `sudo`:

```bash
echo performance | sudo tee /sys/example/profile
```

---

# 7. Permissions

## `chmod`

**Syntax**

```bash
chmod <permissions> <file>
```

**Examples**

```bash
chmod +x script.sh
chmod 644 config.conf
chmod 755 script.sh
```

**Description**
Change file permissions.

Common modes:

```text
600 = rw-------
644 = rw-r--r--
700 = rwx------
755 = rwxr-xr-x
```

---

## `chown`

**Syntax**

```bash
sudo chown <user>:<group> <file>
```

**Example**

```bash
sudo chown martin:martin file.txt
```

**Description**
Change the owner and group of a file.

---

## Recursive ownership change

**Syntax**

```bash
sudo chown -R <user>:<group> <directory>
```

---

## `stat`

**Syntax**

```bash
stat <file>
```

**Example**

```bash
stat script.sh
```

**Description**
Display ownership, permissions, size and timestamps.

---

# 8. Processes

## `ps`

**Syntax**

```bash
ps aux
```

**Example**

```bash
ps aux | grep firefox
```

**Description**
List running processes.

---

## `pgrep`

**Syntax**

```bash
pgrep -af <process>
```

**Example**

```bash
pgrep -af steam
```

**Description**
Find processes by name and display their PID and command line.

---

## `kill`

**Syntax**

```bash
kill <PID>
```

**Example**

```bash
kill 12345
```

**Description**
Ask a process to terminate cleanly.

---

## Force kill

**Syntax**

```bash
kill -9 <PID>
```

**Description**
Immediately force a process to stop.

Use only if normal `kill` does not work.

---

## `pkill`

**Syntax**

```bash
pkill <process>
```

**Example**

```bash
pkill firefox
```

**Description**
Terminate processes by name.

---

## `htop`

**Syntax**

```bash
htop
```

**Description**
Interactive process, CPU and memory monitor.

---

## `watch`

**Syntax**

```bash
watch -n <seconds> '<command>'
```

**Example**

```bash
watch -n 1 'nvidia-smi'
```

**Description**
Run a command repeatedly and refresh its output.

---

# 9. System Information

## `uname`

**Syntax**

```bash
uname -a
```

**Example**

```bash
uname -a
```

**Description**
Display Linux kernel and system information.

Kernel version only:

```bash
uname -r
```

---

## `hostnamectl`

**Syntax**

```bash
hostnamectl
```

**Description**
Display hostname, operating system, kernel and architecture.

---

## `lscpu`

```bash
lscpu
```

Display detailed CPU information.

---

## `free`

```bash
free -h
```

Display RAM and swap usage.

---

## `uptime`

```bash
uptime
```

Show system uptime and load average.

---

## `lspci`

```bash
lspci -nnk
```

Display PCI hardware and which kernel drivers are in use.

---

## `lsusb`

```bash
lsusb
```

List USB devices.

---

## `lsmod`

```bash
lsmod
```

List loaded kernel modules.

Example:

```bash
lsmod | grep nvidia
```

---

## `modinfo`

```bash
modinfo <module>
```

Example:

```bash
modinfo nvidia
```

Display information about a kernel module.

---

## `dkms`

```bash
dkms status
```

Show installed DKMS modules and which kernels they are built for.

---

# 10. Disks and Filesystems

## `lsblk`

```bash
lsblk -f
```

Display disks, partitions, filesystems, UUIDs and mountpoints.

---

## `df`

```bash
df -hT
```

Display filesystem disk usage.

* `-h` = human-readable
* `-T` = filesystem type

---

## `du`

```bash
du -sh <directory>
```

Example:

```bash
du -sh ~/.cache
```

Display the size of a directory.

---

## Find large directories

```bash
du -h --max-depth=1 <directory> | sort -h
```

Example:

```bash
du -h --max-depth=1 ~ | sort -h
```

---

## `findmnt`

```bash
findmnt
```

Example:

```bash
findmnt /
```

Display mounted filesystems and mount options.

---

## `blkid`

```bash
sudo blkid
```

Display filesystem UUIDs and types.

---

# 11. Networking

## IP addresses

```bash
ip -br addr
```

Display interfaces and IP addresses.

---

## Interfaces

```bash
ip -br link
```

Display network interface state.

---

## Routing table

```bash
ip route
```

Display routes and default gateway.

---

## Route lookup

```bash
ip route get <IP>
```

Example:

```bash
ip route get 1.1.1.1
```

Show which interface, source IP and gateway Linux will use.

---

## `ping`

```bash
ping -c <count> <host>
```

Example:

```bash
ping -c 5 1.1.1.1
```

Test connectivity and latency.

---

## `tracepath`

```bash
tracepath <host>
```

Example:

```bash
tracepath 1.1.1.1
```

Trace the network path and discover Path MTU.

---

## `ss`

```bash
sudo ss -tulpn
```

Display listening TCP/UDP ports and processes.

---

## `dig`

```bash
dig <hostname>
```

Example:

```bash
dig archlinux.org
```

DNS lookup.

Against a specific DNS server:

```bash
dig @1.1.1.1 archlinux.org
```

---

## `nmcli`

```bash
nmcli device status
```

Display NetworkManager interface status.

Connections:

```bash
nmcli connection show
```

Wi-Fi networks:

```bash
nmcli device wifi list
```

---

## `iw`

```bash
iw dev <interface> link
```

Display Wi-Fi connection information.

---

## `ethtool`

```bash
sudo ethtool <interface>
```

Display Ethernet speed, duplex and link information.

---

## `curl`

```bash
curl -fL <URL>
```

Download or retrieve data over HTTP/HTTPS.

HTTP headers only:

```bash
curl -I <URL>
```

---

## `tcpdump`

```bash
sudo tcpdump -ni <interface> <filter>
```

Example:

```bash
sudo tcpdump -ni any port 53
```

Capture network packets.

* `-n` = do not resolve names
* `-i` = interface

---

# 12. Systemd

Common system unit locations:

```text
/usr/lib/systemd/system/
/etc/systemd/system/
```

User units:

```text
~/.config/systemd/user/
```

---

## Running services

```bash
systemctl --type=service --state=running
```

---

## Service status

```bash
systemctl status <unit> --no-pager
```

Example:

```bash
systemctl status NetworkManager --no-pager
```

---

## Start

```bash
sudo systemctl start <unit>
```

---

## Stop

```bash
sudo systemctl stop <unit>
```

---

## Restart

```bash
sudo systemctl restart <unit>
```

---

## Enable at boot

```bash
sudo systemctl enable <unit>
```

---

## Enable and start immediately

```bash
sudo systemctl enable --now <unit>
```

---

## Disable and stop

```bash
sudo systemctl disable --now <unit>
```

---

## Failed units

```bash
systemctl --failed
```

---

## Reload systemd configuration

```bash
sudo systemctl daemon-reload
```

Use after creating or modifying unit files.

---

## User services

```bash
systemctl --user status <unit>
```

Example:

```bash
systemctl --user status plasma-powerdevil.service
```

Reload user units:

```bash
systemctl --user daemon-reload
```

---

# 13. Logs

## Current boot

```bash
journalctl -b
```

---

## Previous boot

```bash
journalctl -b -1
```

Very useful after a crash, freeze or failed suspend.

---

## Service logs

```bash
journalctl -u <unit> -b --no-pager
```

Example:

```bash
journalctl -u NetworkManager -b --no-pager
```

---

## Follow logs live

```bash
journalctl -fu <unit>
```

---

## Warnings and errors

```bash
journalctl -b -p warning
```

---

## Kernel messages

```bash
sudo dmesg -T
```

Last 100 lines:

```bash
sudo dmesg -T | tail -n 100
```

Filter:

```bash
sudo dmesg -T | grep -Ei 'error|failed|warning|timeout'
```

---

# 14. Arch Linux System Maintenance

## Update system

```bash
sudo pacman -Syu
```

Synchronize package databases and perform a full system upgrade.

---

## Check available updates

Requires `pacman-contrib`.

```bash
checkupdates
```

Safely show updates without modifying Pacman's normal sync database.

---

## List orphan packages

```bash
pacman -Qdtq
```

Display packages installed as dependencies that are no longer required.

---

## Remove orphan packages

First inspect:

```bash
pacman -Qdtq
```

Then remove:

```bash
sudo pacman -Rns $(pacman -Qdtq)
```

Only run the removal command when the orphan list is not empty.

---

## Pacman cache size

```bash
du -sh /var/cache/pacman/pkg/
```

---

## Clean old package versions

Requires `pacman-contrib`.

```bash
sudo paccache -r
```

Keeps the newest three versions of cached packages.

Keep two:

```bash
sudo paccache -rk2
```

---

## Journal disk usage

```bash
journalctl --disk-usage
```

---

## Clean old journal logs

By size:

```bash
sudo journalctl --vacuum-size=100M
```

By age:

```bash
sudo journalctl --vacuum-time=2weeks
```

---

## User cache size

```bash
du -sh ~/.cache/
```

Find large cache directories:

```bash
du -h --max-depth=1 ~/.cache | sort -h
```

Prefer removing specific application caches rather than blindly deleting the entire `~/.cache` directory.

---

# 15. Pacman

Pacman log:

```text
/var/log/pacman.log
```

---

## List installed packages

```bash
pacman -Q
```

---

## Search installed packages

```bash
pacman -Qs <name>
```

Example:

```bash
pacman -Qs nvidia
```

---

## Search repositories

```bash
pacman -Ss <name>
```

Example:

```bash
pacman -Ss vulkan
```

---

## Install package

```bash
sudo pacman -S <package>
```

Multiple packages:

```bash
sudo pacman -S git curl htop
```

---

## Install only when needed

```bash
sudo pacman -S --needed <package>
```

Example:

```bash
sudo pacman -S --needed git base-devel
```

---

## Installed package information

```bash
pacman -Qi <package>
```

---

## Repository package information

```bash
pacman -Si <package>
```

---

## List package files

```bash
pacman -Ql <package>
```

Example:

```bash
pacman -Ql vulkan-tools
```

---

## Find which package owns a file

```bash
pacman -Qo <file>
```

Example:

```bash
pacman -Qo /usr/bin/vulkaninfo
```

---

## Search which package contains a file

Update file database:

```bash
sudo pacman -Fy
```

Search:

```bash
pacman -F <filename>
```

Example:

```bash
pacman -F vulkaninfo
```

---

## Install local package

```bash
sudo pacman -U <package-file>
```

---

## Remove package

```bash
sudo pacman -Rns <package>
```

Remove the package, unused dependencies and Pacman-created config backups.

---

## List explicitly installed packages

```bash
pacman -Qqe
```

Backup the list:

```bash
pacman -Qqe > packages.txt
```

---

## Verify package files

```bash
pacman -Qkk <package>
```

Example:

```bash
sudo pacman -Qkk sddm
```

Check for missing or modified package files.

---

## Pacman log

```bash
less /var/log/pacman.log
```

---

# 16. Manual AUR Installation

AUR packages are unofficial user-maintained build recipes.

Always inspect the `PKGBUILD`.

---

## Required tools

```bash
sudo pacman -S --needed base-devel git
```

---

## Clone AUR package

```bash
git clone https://aur.archlinux.org/<package>.git
```

Example:

```bash
git clone https://aur.archlinux.org/google-chrome.git
```

---

## Enter directory

```bash
cd <package>
```

---

## Inspect PKGBUILD

```bash
less PKGBUILD
```

---

## Build and install

```bash
makepkg -si
```

**Do not run `makepkg` with `sudo`.**

---

## Update manually cloned AUR package

```bash
git pull
makepkg -si
```

---

# 17. Boot and Kernel

## Current kernel command line

```bash
cat /proc/cmdline
```

---

## Suspend modes

```bash
cat /sys/power/mem_sleep
```

The mode inside brackets is currently selected.

Example:

```text
[s2idle] deep
```

---

## Rebuild mkinitcpio presets

```bash
sudo mkinitcpio -P
```

---

## systemd-boot status

```bash
sudo bootctl status
```

---

## Boot entries

```bash
sudo bootctl list
```

---

## Secure Boot status with sbctl

```bash
sbctl status
```

Verify signed files:

```bash
sudo sbctl verify
```

---

# 18. Btrfs

## List subvolumes

```bash
sudo btrfs subvolume list /
```

---

## Filesystem usage

```bash
sudo btrfs filesystem usage /
```

---

## Device statistics

```bash
sudo btrfs device stats /
```

Useful for checking filesystem/device error counters.

---

## Scrub filesystem

```bash
sudo btrfs scrub start -Bd /
```

Verify checksums across the filesystem.

* `-B` = wait for completion
* `-d` = display statistics

---

# 19. Git

## Clone repository

```bash
git clone <URL>
```

---

## Status

```bash
git status --short --branch
```

---

## Show changes

```bash
git diff
```

---

## Stage file

```bash
git add <file>
```

---

## Stage everything

```bash
git add -A
```

---

## Commit

```bash
git commit -m "<message>"
```

Example:

```bash
git commit -m "Update Arch Linux cheat sheet"
```

---

## Pull

```bash
git pull --rebase
```

---

## Push

```bash
git push
```

---

## History

```bash
git log --oneline --graph --decorate --all
```

---

## Remotes

```bash
git remote -v
```

---

## Branches

```bash
git branch -av
```

---

## Switch branch

```bash
git switch <branch>
```

---

# 20. Shell Shortcuts

## Command history

```bash
history
```

Search:

```bash
history | grep pacman
```

---

## Repeat previous command

```bash
!!
```

Example:

```bash
sudo !!
```

Useful when you forgot `sudo`.

---

## Search command history

```text
Ctrl + R
```

---

## Interrupt current command

```text
Ctrl + C
```

---

## Suspend current process

```text
Ctrl + Z
```

---

## Clear terminal

```text
Ctrl + L
```

or:

```bash
clear
```

---

## Reload Bash configuration

```bash
source ~/.bashrc
```

---

# 21. Help

## Manual

```bash
man <command>
```

Example:

```bash
man find
```

---

## Quick help

```bash
<command> --help
```

Example:

```bash
find --help
```

---

## Search manual descriptions

```bash
apropos <keyword>
```

Example:

```bash
apropos filesystem
```

Useful when you know what you want to do but cannot remember the command.

---

# Recommended Utility Packages

```bash
sudo pacman -S --needed \
  base-devel \
  git \
  curl \
  wget \
  htop \
  tree \
  ripgrep \
  plocate \
  pacman-contrib \
  bind \
  traceroute \
  ethtool \
  tcpdump
```

Useful commands provided by these packages:

| Package          | Commands                   |
| ---------------- | -------------------------- |
| `pacman-contrib` | `paccache`, `checkupdates` |
| `bind`           | `dig`                      |
| `plocate`        | `locate`                   |
| `ripgrep`        | `rg`                       |
| `ethtool`        | `ethtool`                  |
| `tcpdump`        | `tcpdump`                  |
| `tree`           | `tree`                     |
| `htop`           | `htop`                     |

---

# Important Arch Linux Notes

* Arch Linux is a rolling-release distribution.
* Perform full upgrades with `sudo pacman -Syu`.
* Avoid partial upgrades.
* Do not normally run `pacman -Sy` or `pacman -Syy` by themselves.
* Check Arch Linux news when an upgrade requires manual intervention.
* Review `.pacnew` and `.pacsave` files after relevant package upgrades.
* AUR packages are unofficial. Review the `PKGBUILD` before building.
* Keep backups before making important system changes.

---

# References

* ArchWiki
* Pacman
* systemd
* Arch User Repository
* Linux manual pages

---

*Last updated for modern Arch Linux usage.*
