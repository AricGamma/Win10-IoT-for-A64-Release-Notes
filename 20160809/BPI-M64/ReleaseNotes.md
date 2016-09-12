# Windows 10 IoT Core for BPI-M64 Release Note (Beta_20160809)

* * *

*   **Release Date:** 2016-08-09
*   **Kernel Version:** Windows 10 IoT Core version 1511

    This is the first released version of Windows 10 IoT Core for BananaPi M64. Only part of features enabled and  we will keep developing and update in time.This document will introduce how to deploy Windows 10 IoT Core to a BPI-M64 board and note known issues.

* * *


## 1. [How to deploy](#1)

    There are 3 tools that can be used to flash the ffu to a Pine64 board:

1.  Using [Windows 10 IoT Dash Board](https://iottools.blob.core.windows.net/iotdashboardpreview/setup.exe);

![Windows 10 IoT Dashboard](https://github.com/Leeway213/Win10-IoT-for-A64-Release-Notes/blob/master/Pic/IoTDashboardMainPage.png)

2.  Using "IoTCoreImageHelper" tool which is part of "IoT Core Kits";

![IoTCoreImageHelper](https://github.com/Leeway213/Win10-IoT-for-A64-Release-Notes/blob/master/Pic/IoTImageHelper.png)

3.  Using "dism.exe" in under "C:\Windows\System32".
    > **Notice:** In fact, both tool 1 and tool 2 depend on "dism.exe". They just provide a graphic user interface to call "dism.exe".

### 1.1 [Using Windows 10 IoT Dash Board](#1.1)

* Switch to "Set up a new device" tab;
* Select "Custom" option for "Device type". Click "browse" button to pick your ffu file and select a correct drive;
* Provide some provision information such as device name, password and wlan profile;
* Check the licence item box to accept the software licence and install.

> **PS:** After the progress finished, an error message "Failed to write provisioning file to microSD card" will be shown. The reason is that "IoT Dash Board" cannot write the provision configuration(device name, password & wlan profile) into microSD card. We are dealing with this issue. Please just ignore. Device name and password will be set to default.

### 1.2 [Using IoTCoreImageHelper](#1.2)

This tool is very simple. Just select the SD card and browse to pick image file to flash.

> **How to get this tool:** 
>
> Download the Raspberry Pi setup tool from [here](http://go.microsoft.com/fwlink/?LinkId=691711) and install. Then get the "IoTCoreImageHelper" tool under the "C:\Program Files (x86)\Microsoft IoT\" directory.

### 1.3 [Using command line to call "dism.exe" directly](#1.3)

*   Start command prompt as an administrator;
*   Insert your microSD card to your PC;
*   Type "diskpart" to enter diskpart tool, then type "list disk" to show all disks;
*   Note the disk ID of your microSD card(0, 1 or 2 etc);

```shell
    DISKPART\> list disk

          Disk ###  Status         Size     Free     Dyn  Gpt
          ----------------------------------------------------
          Disk 0    Online          931 GB      0 B
          Disk 1    Online         7456 MB  5120 KB        *
```

* Type command below to flash image to SD card.

    `Dism.exe /Apply-Image /ImageFile:[ffu_path] /ApplyDrive:\\.\PhysicalDrive[disk_number] /SkipPlatformCheck`

    > **Notice:** Please confirm the disk id seriously. It may damage your important data if flashing a wrong disk.

## 2. [Manage Windows 10 IoT Core](#2)

### 2.1 [Using "Device Portal" to manage](#2.1)

*   Connect the network of board to your computer.
*   Open a web browser and type address `http://IP Address:8080`.
*   Login as default account whose username and password is `Administrator` & `p@ssw0rd`

### 2.2 [Using PowerShell to manage](#2.2)

*   Start PowerShell as an administrator.
*   From the PowerShell console, type the following command to start a remote session:
```C
//Start Windows Remote Management
net start WinRM 

//Add destination host to trusted hosts list. You can use an IP address as a value.
Set-Item WSMan:\localhost\Client\TrustedHosts -Value [Hostname or IP address]

//Start a PowerShell remote session.
Enter-PSSession -ComputerName [Hostname or IP address] -Credential [Hostname or IP address]\[username]
```
>**PS:** The default username and password is `Administrator` & `p@ssw0rd`.

## 3. [Known Issues](#3)

*   **Network:** Wifi and Ethernet are not available. Please use a USB ethernet adapter or USB wifi adapter instead temporarily.
*   When booting, it's possible to throw an error of *KERNEL_SECURITY_CHECK_FAILURE*. You can just ignore it and retry about 2-3 times. It will bring up successfully.