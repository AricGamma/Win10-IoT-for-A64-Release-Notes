# How To Flash UEFI Image

----

The Unified Extensible Firmware Interface (UEFI]) is a specification that defines a software interface between an operating system and platform firmware. UEFI replaces the Basic Input/Output System (BIOS) firmware interface originally present in all IBM PC-compatible personal computers, with most UEFI firmware implementations providing legacy support for BIOS services. UEFI can support remote diagnostics and repair of computers, even with no operating system installed.
In addition, a UEFI image is also regarded as a powerful replacement of u-boot run on an ARM architecture platform. It's a universal solution to bring up all kinds of OS compared with u-boot.
Allwinner UEFI Image is a universal pre-boot solution running on Allwinner ARM SoCs based on EDK2 open source project.

## How to flash a UEFI image

Firstly, you need install `PhoenixSuit` on a your PC. Here we don't provice a download link, you can search "PhoenixSuit" by google or other web search engines. 

Here I'll take PhoenixSuit on a Windows OS as an example.

1. Start `PhoenixSuit` application and switch to "firmware" tab;  

    ![PhoenixSuit firmware](https://github.com/Leeway213/Win10-IoT-for-A64-Release-Notes/blob/master/Pic/PhoenixFirmware.png?raw=true)

2. Click "Image" button to select your firmware image;  

    ![PhoenixSuit select firmware](https://github.com/Leeway213/Win10-IoT-for-A64-Release-Notes/blob/master/Pic/PhoenixSelectImage.png?raw=true)

3. Connect your board to PC with a USB cable and force to boot into EFEX mode.

    > For a BPI-M64 board, there is an FEL button beside the serial pins. Hold the FEL button and push reset button or re-power the board.

4. Then you will see there is a dialog poped on `PhoenixSuit` like picture below:  

    ![phoenixFormatConfirm](https://github.com/Leeway213/Win10-IoT-for-A64-Release-Notes/blob/master/Pic/phoenixFormatConfirm.png?raw=true)

    There are two options "Yes" and "No". It will clear your disk include the OS on your device. If want to keep the operating system and just update firmware, please select "No".

5. Select one of the options shown above, then it will start to flash.  

    ![phoenixFlashingProgress](https://github.com/Leeway213/Win10-IoT-for-A64-Release-Notes/blob/master/Pic/phoenixFlashingProgress.png?raw=true)

6. After message "Firmware Upload Successful" poped, firmware flashing progress finishes.  

    ![phoenixflashsuccessful](https://github.com/Leeway213/Win10-IoT-for-A64-Release-Notes/blob/master/Pic/phoenixflashsuccessful.png?raw=true)

7. Login a serial console with baudrate 115200 and reset your board. You will see the console output with the "Boot Menu" in the end.

```
[1] boot windows from HDD
[2] Shell
[3] Boot Manager
[4] Boot Android
[5] Boot Efex
[6] Boot Fastboot
[7] Boot PrivateBurn
[8] Boot UsbMass
[9] Boot TestApp
Start:
```


To continue to flash an ffu image, please select 8 to boot into the usb mass storage mode and refer to this [doc](https://github.com/Leeway213/Win10-IoT-for-A64-Release-Notes/blob/master/doc/How%20to%20flash%20ffu.md).