# How to Deploy a Windows 10 IoT for PINE64 or BPI-M64

---

**First of all, you need to mount your device(such as emmc or sd card) as a mass storage. If wanna flash into an emmc or you cannot get an SD card reader, you need to flash a UEFI image refered to this [document](https://github.com/Leeway213/Win10-IoT-for-A64-Release-Notes/blob/master/doc/How%20to%20flash%20UEFI%20image.md).**

There are 3 tools that can be used to flash the ffu to a Pine64 board:

1.  Using [Windows 10 IoT Dash Board](https://iottools.blob.core.windows.net/iotdashboardpreview/setup.exe);

    ![Windows 10 IoT Dashboard](https://github.com/Leeway213/Win10-IoT-for-A64-Release-Notes/blob/master/Pic/IoTDashboardMainPage.png?raw=true)

2.  Using "IoTCoreImageHelper" tool which is part of "IoT Core Kits";

    ![IoTCoreImageHelper](https://github.com/Leeway213/Win10-IoT-for-A64-Release-Notes/blob/master/Pic/IoTImageHelper.png?raw=true)

3.  Using "dism.exe" in under "C:\Windows\System32".

    ![dism tool in command line](https://github.com/Leeway213/Win10-IoT-for-A64-Release-Notes/blob/master/Pic/dism.png?raw=true)    

    > **Notice:** In fact, both tool 1 and tool 2 depend on "dism.exe". They just provide a graphic user interface to call "dism.exe".

### 1.1 [Using Windows 10 IoT Dash Board](#1.1)

* Switch to "Set up a new device" tab;

    ![Set up a new device](https://github.com/Leeway213/Win10-IoT-for-A64-Release-Notes/blob/master/Pic/Set_up_an_new_device.png?raw=true)

* Select "Custom" option for "Device type". Click "browse" button to pick your ffu file and select a correct drive;

    ![Browse ffu file](https://github.com/Leeway213/Win10-IoT-for-A64-Release-Notes/blob/master/Pic/Browse_ffu.png?raw=true)

* Provide some provision information such as device name, password and wlan profile;

    ![Set provision information](https://github.com/Leeway213/Win10-IoT-for-A64-Release-Notes/blob/master/Pic/Set_password%26WLAN_provision.png?raw=true)

* Check the licence item box to accept the software licence and install.

    ![Check licence item box and install](https://github.com/Leeway213/Win10-IoT-for-A64-Release-Notes/blob/master/Pic/Flash_processing.png?raw=true)

> **PS:** After the progress finished, an error message "Failed to write provisioning file to microSD card" will be shown. The reason is that "IoT Dash Board" cannot write the provision configuration(device name, password & wlan profile) into microSD card. We are dealing with this issue. Please just ignore. Device name and password will be set to default.

### 1.2 [Using IoTCoreImageHelper](#1.2)

This tool is very simple. Just select the SD card and browse to pick image file to flash.

![IoTCoreImageHelper](https://github.com/Leeway213/Win10-IoT-for-A64-Release-Notes/blob/master/Pic/IoTImageHelper.png?raw=true)

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


![dism with diskpart](https://github.com/Leeway213/Win10-IoT-for-A64-Release-Notes/blob/master/Pic/dism_with_diskpart.png?raw=true)