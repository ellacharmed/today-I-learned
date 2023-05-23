---
jupytext:
  cell_metadata_filter: -all
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.14.5
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---


# Move location of distro in WSL2

Date tested: 2023.05.20

source: https://superuser.com/questions/1550622/move-wsl2-file-system-to-another-drive

**What is it**: This is a guide to move the distro image to a location of our choosing. wsl2 installs the distro images (files in .vhdx format) in %userprofile% which is the `C:\` drive for most of us. And we usually partition our system drive to be smaller and the bulk of the storage space is designated for the applications and documents.

**Who is it for**:  Anyone who uses wsl2

**Why is it relevant**: For everyone who uses wsl2 and wants to reclaim their `C:\` storage space back. My system become laggy and jupyter kernel keeps hanging. 

## The steps

1. Open terminal (or powershell or command prompt) and list all installed and distros and their state, with `wsl -l -v`. (*) indicates that's my default distro. 

`-l` is to list <br/>
`-v` in verbose mode

Copy and paste the commands below, leaving out the `❯ ` prompt

```bash
❯ wsl -l -v
  NAME                   STATE           VERSION
* Ubuntu-22.04           Running         2
  docker-desktop-data    Stopped         2
  Ubuntu-20.04           Running         2
  docker-desktop         Stopped         2
```

2. Shutdown wsl with `wsl --shutdown` and verify distros stopped `wsl --list --verbose` or `wsl -l -v`

```bash
❯ wsl --shutdown

❯ wsl --list --verbose
  NAME            STATE           VERSION
* Ubuntu-22.04    Stopped         2
  Ubuntu-20.04    Stopped         2
```

3. Create folder to store the backups in drive other than `C:\` or final distro location; I'm placing mine in my `N:\` drive in the `backupdistros` folder

```bash
❯ mkdir n:\backupdistros

    Directory: N:\

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d----           21/5/2023 12:31 pm                backupdistros
```

4. Export the distro as .vhdx instead of .tar (it's faster. Older guides say to use .tar); `"Ubuntu-20.04"` is the distro name as identifier in wsl/docker when doing `wsl -l -v`. You can still call the file "ext4.vhdx" but I like to see the file name as the distro name to avoid confusion, that's why mine is renamed as below. The export (and import) process is going to take a while, depending on how much stuff you have on the drive.

COMMAND `wsl --export <distro-name> <temp-path><backup-distro-name>.vhdx`

```bash
❯ wsl --export Ubuntu-20.04 n:\backupdistros\Ubuntu-20.04.backup.vhdx
Export in progress, this may take a few minutes.
The operation completed successfully.
```

5. Unregister distro from current wsl config

COMMAND `wsl --unregister <distro-name>`

```bash
❯ wsl --unregister Ubuntu-20.04
Unregistering.
The operation completed successfully.
```

6. Import distro to new location. Path needs a folder name ie `e:\wsl2\Ubuntu-22.04` if you have multiple distros as they all end up with original `"ext4.vhdx"`. You can still call the file "ext4.vhdx" but I like to see the drive name as the distro name to avoid confusion, that's why mine is renamed as below. 

COMMAND `wsl --import <distro-name> <new-path><folder-name> <temp-path><backup-distro-name>.vhdx`

```bash
❯ wsl --import Ubuntu-22.04 e:\wsl2\Ubuntu-22.04 n:\backupdistros\Ubuntu-22.04.backup.vhdx
Import in progress, this may take a few minutes.
The operation completed successfully.
```
![explorer 0521-1095](https://github.com/ellacharmed/today-I-learned/assets/6437860/35af9b1b-971c-4609-9139-9e54e1268245)

7. Reestablish default username to use with the distro (if it is not root). The executable `ubuntu2204.exe` is located in the `%userprofile%` path below, if it is not on your `$PATH` you need to `cd` to it first.

```bash
❯ cd %userprofile%\AppData\Local\Microsoft\WindowsApps
```
COMMAND `<distro>.exe config --default-user <user-name>`

```bash
❯ ubuntu2204.exe config --default-user ubuntu
```

8. Start distro

COMMAND `wsl ~ -d <distro-name>`
```bash
❯ wsl ~ -d Ubuntu-22.04
```

9. Repeat for other distros that you have
```bash
❯ wsl --export Ubuntu-20.04 n:\backupdistros\Ubuntu-20.04.backup.vhdx
Export in progress, this may take a few minutes.
The operation completed successfully.

❯ wsl --unregister Ubuntu-20.04
Unregistering.
The operation completed successfully.

❯ wsl --import Ubuntu-20.04 e:\wsl2\Ubuntu-20.04 n:\backupdistros\Ubuntu-20.04.backup.vhdx
Import in progress, this may take a few minutes.
The operation completed successfully.

❯ ubuntu2004.exe config --default-user ellanix
```

10. Final state on my system
```bash
❯ wsl -l -v
  NAME            STATE           VERSION
* Ubuntu-22.04    Running         2
  Ubuntu-20.04    Stopped         2
```

![explorer 0521-1096](https://github.com/ellacharmed/today-I-learned/assets/6437860/997de7d3-8476-41f6-a7a2-da545e61af48)

