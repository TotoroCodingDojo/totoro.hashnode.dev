---
title: "Simple Steps to Install XAMPP on Your Linux System"
datePublished: Wed Oct 30 2024 07:39:38 GMT+0000 (Coordinated Universal Time)
cuid: cm2vkgaf8000009kzdiv1cg0k
slug: simple-steps-to-install-xampp-on-your-linux-system
tags: linux, xampp

---

XAMPP is a popular PHP development environment. It stands for - Apache + MariaDB + PHP + Perl.

> Before following this guide read [https://www.apachefriends.org/faq_linux.html](https://www.apachefriends.org/faq_linux.html).

Follow these steps to setup xamp on linux:

- Download the latest version of `xampp` for GNU/Linux form here [https://www.apachefriends.org/index.html](https://www.apachefriends.org/index.html).
- Open terminal, `cd` into the directory where the installer is, give execute permission for the installer using `chmod +x [filename]`, and then run the installer giving root permissions (`sudo`).
- The installer will install the binaries in `/opt/lampp` directory.
- Now run this command, `cd /opt/lampp; ls -all`, this will list files in `/opt/lampp` directory.
- Some important files and directories in `/opt/lampp` are
    - `xampp`, this is the main binary file for starting and stopping the server
    - `uninstall`, this is the binary for uninstalling `xampp`
    - `manager-linux-x64.run`, this is used for running the graphical interface, just run this in root privilege.
    - `bin`, this directory contains the binaries for `mysql` `perl` `apache` ...
    - `configuration.ini`, this file contains the setting for running the servers, if you want to change the configuration of the server, like port no, root directory, edit this file.
- Once, you start the servers, either using `xampp` or `manager-linux-x64.run` (GUI), then go and open the `localhost:80` on browser.

Don't include this directory in the `PATH` variable, just make aliases for some specific program you want, or softlink them in the `/usr/bin` directory. Otherwise it may conflict with system software.
