---
title: Install Linux Subsystem on Windows Server
description: Learn how to install the Linux Subsystem on Windows Server. WSL is available for installation on Windows Server 2019 (version 1709) and later.
ms.date: 11/12/2021
ms.topic: article
---

# Windows Server Installation Guide

The Windows Subsystem for Linux is available for installation on Windows Server 2019 (version 1709) and later. This guide will walk through the steps of enabling WSL on your machine.

## Enable the Windows Subsystem for Linux

Before you can run Linux distributions on Windows, you must enable the "Windows Subsystem for Linux" optional feature and reboot.

Open PowerShell **as Administrator** and run:

```powershell
    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux

```

## Download a Linux distribution

See the [Downloading distributions](install-manual.md#downloading-distributions) section of the manual installation page for instructions and links to download your preferred Linux distribution.

## Extract and install a Linux distribution

Now that you've downloaded a Linux distribution, in order to extract its contents and manually install, follow these steps:

1. Extract the `<DistributionName>.appx` package's contents, using PowerShell:

    ```powershell
    Rename-Item .\Ubuntu.appx .\Ubuntu.zip
    Expand-Archive .\Ubuntu.zip .\Ubuntu
    ```

2. Once the distribution has been downloaded, navigate to the folder containing the download and run the following command in that directory, where `app-name` is the name of the Linux distribution .appx file.

```Powershell
Add-AppxPackage .\app_name.appx
```


> [!CAUTION]
> **Installation failed with error 0x8007007e**: If you receive this error, then your system doesn't support WSL. Ensure that you're running Windows build 16215 or later. [Check your build](troubleshooting.md#check-your-build-number). Also check to [confirm that WSL is enabled](troubleshooting.md#confirm-wsl-is-enabled) and your computer was restarted after the feature was enabled.  

3.Add your Linux distribution path to the Windows environment PATH (`C:\Users\Administrator\Ubuntu` in this example), using PowerShell:

```powershell
$userenv = [System.Environment]::GetEnvironmentVariable("Path", "User")
[System.Environment]::SetEnvironmentVariable("PATH", $userenv + ";C:\Users\Administrator\Ubuntu", "User")
```

You can now launch your distribution from any path by typing `<DistributionName>.exe`. For example: `ubuntu.exe`.

Once installation is complete, you can [create a user account and password for your new Linux distribution](./setup/environment.md#set-up-your-linux-username-and-password).
