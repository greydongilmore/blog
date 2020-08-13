---
title: WSL 2
template: overrides/main.html
---

The Windows 10 May 2020 update makes installing WSL2 much easier.

## Turn on WSL feature and virtual machine platform

1. Open Windows PowerShell as administrator and run the commands:

    ```console
    dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
    dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
    ```

2. You will need to restart your computer.

## Download the WSL2 update

1. Prior to running WSL2 you will need to download and install the [WSL2 kernel update](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi).

## Download a linux distro

1. Open the Microsoft Store and choose your favorite linux distribution by searching for them (I prefer Ubuntu):
    * Ubuntu
    * Debian

2. From the distro's page, select __Get__

3. Once done installing, open up __Powershell__ as administrator and run (replace distro with the name of the distro you installed):

    ```console
    wsl --set-default-version 2
    ```

    ```console
    wsl --set-version [Distro] 2
    ```

## Finalizing

1. To complete the initialization of your newly installed distro, launch a new instance by searching in the Start menu and launching the distro

2. The first time a newly installed distro runs, a Console window will open, and you'll be asked to wait for a minute or two for the installation to complete

3. Once installation is complete, you will be prompted to create a new user account (and its password)

4. Most distros ship with an empty/minimal package catalog. You should regularly be updating your package catalog, and upgrading your installed packages using your distro's preferred package manager

      ```console
      sudo apt-get update && sudo apt-get upgrade
      ```

