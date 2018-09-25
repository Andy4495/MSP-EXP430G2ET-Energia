Energia Support for MSP-EXP430G2ET
==================================

Texas Instruments has released an updated version of the MSP430G2 LaunchPad: [MSP-EXP430G2ET][2]. The updated LaunchPad supports the same DIP-package G2 processors as the [old LaunchPad][1], along with adding an RGB LED to the existing RED and GREEN LEDs. Most significantly, however, is an update to the emulation section to TI's [eZ-FET][3] debugger, including [EnergyTrace][4] support (hence the "ET" in the Launchpad name). This brings the G2 debugging and emulation interface to be on-par with newer LaunchPad products.

Unfortunately, the current version of [Energia][8] (18) and the MSP430 boards package (1.0.3) does not support the LaunchPad, since it assumes that the older emulation interface is used when programming MSP430G2 chips.

This repo contains a somewhat hacked method of supporting the new G2ET LaunchPad in Energia. Hopefully, full support for the new LaunchPad will be available in an upcoming MSP430 board package update.

As of now, this repo only supports Windows. See the [Background](#background) section below for hints on how to support other OSes.

Installing (Windows)
--------------------

1. Close all Energia windows (completely shut down the program).

2. Download all the files in this repo.

3. Create a new directory called `uniflash` at `%LOCALAPPDATA%\Energia15\packages\energia\tools`:

        C:\> mkdir %LOCALAPPDATA%\Energia15\packages\energia\tools\uniflash

4. Copy the files `boards.txt`, `platform.txt`, and `programmers.txt` to `%LOCALAPPDATA%\Energia15\packages\energia\hardware\msp430\1.0.3`.

5. Re-start Energia. You should now have `MSP-EXP430G2ET w/ MSP430G2553 (16 MHz)` available in the `Tools->Board` menu.

Usage Notes
-----------

As with the older G2 LaunchPad, it is necessary to place the RXD and TXD jumpers on J101 in a horizontal position in order to uses the hardware UART.

If you have made any changes to `boards.txt`, `platform.txt`, or `programmers.txt`, then you will need to manually merge in the changes to those files.

Re-installing version 1.0.3 of the MSP430 board package will replace the updated versions of `boards.txt`, `platform.txt`, and `programmers.txt` with the default versions, so they will need to be re-installed again, too.

An updated version of the MSP430 board package may or may not include support for the G2ET LaunchPad, and the changes described here may or may not work with the new package.

In addition to adding support for the G2ET LaunchPad, the `boards.txt` file also adds support for programming the G2553 processor at 8 MHz instead of the default 16 MHz clock speed (for both the old and new LaunchPads). The 8 MHz clock speed is needed when running the G2 at a lower supply voltage (such as when using a coin cell battery).

Background
----------

Energia uses a tool called `mspdebug` for flashing the older MSP-EXP430G2 LaunchPads. This tool does not work with the eZ-FET debugger included with the newer G2ET LaunchPads. All the other MSP430 LaunchPads use the `dslite` tool. However, the version of `dslite` included with Energia 18 (7.4.0.1099) does not support the eZ-FET version on the G2ET LauchPads. The newer version of dslite  included with [CCS 8.x][5] and [UniFlash 4.x][6] is required.

UniFlash includes a feature to export a standalone command line package. This package includes all the executables, libraries, and configuration files to flash a device. The `4.4.0.2009` directory in this repo was created from UniFlash 4.4 using an MSP430G2 configuration, and contains version 8.1.0.1365 of dslite.

For MacOS or Linux support, a similar procedure could be used to create the necessary executables by running the Standalone Command Line package export from the OS-specific version of UniFlash, then following a similar procedure as outlined in the [Installing](#installing-windows) section above.

Energia should be able to officially support the G2ET LaunchPad in the future with an updated MSP430 board package which includes the latest version of the `dslite` tool.

License
-------

The `4.4.0.2009` directory is a package exported from TI's UniFlash tool and is distributed per the UniFlash [license agreement][7]. The UniFlash license agreement [file][9] was manually added to the directory after it was exported from UniFlash.

`boards.txt`, `platform.txt`, or `programmers.txt` are modified versions of files included in Energia, and are distributed per the Energia [license][10].

References
----------

+ Old MSP-EXP430G2 LaunchPad [product info][1].
+ Updated MSP430G2 LauchPad: [MSP-EXP430G2ET][2].
+ Texas Instruments [eZ-FET][3] emulation.
+ Texas Instruments [EnergyTrace][4] technology.
+ Texas Instrumetns [Code Composer Studio][5].
+ Texas Instruments [UniFlash][6].
+ UniFlash [License Agreement][7].
+ [Energia][8] IDE.


[1]: http://www.ti.com/tool/MSP-EXP430G2
[2]: http://www.ti.com/tool/msp-exp430g2et
[3]: http://www.ti.com/lit/slau647
[4]: http://www.ti.com/tool/energytrace
[5]: http://www.ti.com/tool/CCSTUDIO
[6]: http://www.ti.com/tool/UNIFLASH
[7]: http://processors.wiki.ti.com/index.php/File:Uniflash_v4_license.zip
[8]: http://energia.nu/
[9]: ./4.4.0.2009/license.txt
[10]: https://github.com/robertinant/EnergiaNG/blob/master/license.txt
