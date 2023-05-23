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

# Move location of Docker containers in WSL2

source: 
- https://stackoverflow.com/questions/62441307/how-can-i-change-the-location-of-docker-images-when-using-docker-desktop-on-wsl2
- https://stackoverflow.com/questions/40465979/change-docker-native-images-location-on-windows-10-pro
- https://docs.docker.com/desktop/install/windows-install/#install-from-the-command-line
- https://forums.docker.com/t/docker-installation-directory/32773/11

Date tested: 2023.05.23

**What is it**: This is a guide to move the distro image to a location of our choosing. Docker installs the distro images (files in .vhdx format) in %userprofile% which is the `C:\` drive for most of us. And we usually partition our system drive to be smaller and the bulk of the storage space is designated for the applications and documents. 

Most of the guides in the sources cited above have some info that does not apply as they may be for different Operating Systems or the steps have become outdated as things changed. So take note of dates when you follow a how-to guide.

**Who is it for**:  Anyone who uses Docker Desktop in Windows

**Why is it relevant**: My system become laggy and jupyter kernel keeps hanging. For everyone who uses Docker Desktop and wants to reclaim their `C:\` storage space back. 

If you're here from the #mlopszoomcamp [module 01-Intro class](https://github.com/DataTalksClub/mlops-zoomcamp/blob/main/01-intro/README.md), please take note of the following.

```{important}
This set of instructions is for Windows OS only, and it differs from the instructions in the above-linked README.md from class, as that is for Linux.

Note the line.
Recommended development environment: Linux

In Linux (and maybe in MacOS), `docker` and `docker-compose` have to be installed separately. While in Windows, the installer does both at the same time.
```

## Existing install

If docker images already exist and wanna keep, go to [](move_wsl_distro.md)


## New fresh install
1. Create folders on target location for symlinks / directory junctions

COMMAND `mklink /j <source/path/to/link/from> <target/path/to/link/to>`

```bash
> mklink /j "C:\ProgramData\Docker" "<target/path/to/link/to>"
> mklink /j "C:\ProgramData\DockerDesktop" "<target/path/to/link/to>"
> mklink /j "C:\Program Files\Docker" "<target/path/to/link/to>" <--- omit this, done by --installation-dir= args below>
> mklink /j "C:\Users\xxx\AppData\Local\Docker" "<target/path/to/link/to>"
> mklink /j "C:\Users\xxx\AppData\Roaming\Docker Desktop" "<target/path/to/link/to>"
> mklink /j "C:\Users\xxx\AppData\Roaming\Docker" "<target/path/to/link/to>"
```

```{important}
- left side paths cannot exist, created by mklink
- right side paths must be created prior to running the "mklink" command
- 3rd line can be ommited, taken care of by installer's "--installation-dir=" now
- userprofile paths: added the roaming ones as well (may not be necessary)
```

2. Get your user profile using `%userprofile%\AppData\Local\` and `%userprofile%\AppData\Roaming\` in the Windows Explorer address bar.

- "%userprofile%\AppData\Local\Docker\"
- "%userprofile%\AppData\Roaming\Docker\"
- "%userprofile%\AppData\Roaming\Docker Desktop\"

3. Verfiy above source folders (on the left side) are not present, remove them if they are. 


4. Open an elevated command prompt (ie with Administrator priviliges), using `CTRL+Click` (in image below). Also take note of the Important Notes above. My target path is in my `E:\` drive. Copy+paste the commands one line at a time.

Doing the Program files,
```bash
mklink /D "C:\ProgramData\Docker" "E:\docker\programdata\docker"
mklink /D "C:\ProgramData\DockerDesktop" "E:\docker\programdata\dockerdesktop"
```

```{warning}
mklink /j "C:\Program Files\Docker" " -- omit -- "              <--- done by install args below>
```

Doing the user profiles files,
```
mklink /D "C:\Users\Ella\AppData\Local\Docker\" "E:\docker\appdata\local\docker"
mklink /D "C:\Users\Ella\AppData\Roaming\Docker\" "E:\docker\appdata\roaming\docker"
mklink /D "C:\Users\Ella\AppData\Roaming\Docker Desktop\" "E:\docker\appdata\roaming\docker desktop"
```

```{note}
default path: C:\Program Files\Docker\Docker
new path: d:\Program Files\Docker\
```

5. Download the "**Docker Desktop for Windows**" from https://docs.docker.com/desktop/install/windows-install/. Take note of the download folder path (CTRL+J from your web browser). 

5. Navigate to downloaded location of the installer i.e. (CTRL+J) from web browser. When the Windows Explorer is opened, you may want to copy the path to the clipboard for the next step. `Copy path` from the ribbon or right-click on the folder name and `copy path as text`.

Instead of letting the installer install to the default path as in the note above, we're going to use the CLI (Command Line Interface) to specify the preferred install location that we want to install to.

7. Change directory to your downloads folder where you've downloaded the executable then execute the installer, specifying the argument and parameter as follows, using my preferred path for example

COMMAND `cd <downloads-path>` <br/>
COMMAND `"Docker Desktop Installer.exe" install --installation-dir="<preferred-install-path>"``

`cd b:\downloads`
`"Docker Desktop Installer.exe" install --installation-dir="d:\Program Files\Docker\"`


```{warning}
System.Exception: For security reasons C:\ProgramData\DockerDesktop cannot be a symlink.
   at CommunityInstaller.Program.Main(String[] args)
```

8. If you encounter above error, removed the ProgramData symlinks, and try again and this time the installer runs successfully.

9. If you run below `wsl -l -v` command in your shell (_powershell_ or _command prompt_), you might see that docker is already running. If not, launch it in the next step. 

```{note}
You may not have other distros, if you haven't installed them in WSL before. So your list is going to look different from mine.
```

```bash
❯ wsl -l -v
  NAME                   STATE           VERSION
* Ubuntu-22.04           Running         2
  docker-desktop         Running         2
  Ubuntu-20.04           Running         2
  docker-desktop-data    Running         2
```

10. Before you test Docker, let's change the default docker path for images: 

   - launch Docker Desktop from Windows
   `WIN+s` -> input `dock..` in the input field, and the app name would be autofilled, press `ENTER`
   - set path to images in Docker Desktop -> Settings -> Resources -> Advanced -> Disk Image Location -> click Browse button
   - select the location in your system where you want the images to be downloaded to and stored
   - above instruction would take a while, and the screen may be unresponsive. Just wait until the path reflects the changes you set.


11. Test with a new image. In a _terminal_ or _powershell_ or _command_ prompt, type below command and press `ENTER`

`docker run hello-world`

```{note}
If you prefer using the GUI client of the Docker Desktop, you can also do this from the search bar in Docker Desktop (look for the `CTRL+K` button and type hello-world). 
```

The result is the same either way, Docker would perform the steps it outlines. And now you can try other containers/images.


