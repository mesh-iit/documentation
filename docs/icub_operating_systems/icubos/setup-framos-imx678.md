# Setup Orin NX for using with FRAMOS-IMX678-C

This guide aims to highlight the correct procedure to configure the setup for using the [`FRAMOS-IMX678`](https://framos.com/products/modules/fsmgo-modules/fsmgo-with-imx678-sensor-and-110-hfov-lens-27361/) cameras with the [`Orin NX`](https://www.nvidia.com/it-it/autonomous-machines/embedded-systems/jetson-orin/) from Nvidia + [`Boson for FRAMOS`](https://connecttech.com/product/boson-for-framos-carrier-board-for-nvidia-jetson-xavier-nx/) carrier from ConnectTech.

!!! info

    Be sure that the [Jetpack installation](./jetpack.md) procedure up to the BSP installation on the setup has been completed. At this point we are ready to flash the image.

### Flash the image

In the host:

1. Navigate into `~/nvidia/nvidia_sdk/JetPack_6.2.1_Linux_JETSON_ORIN_NX_TARGETS/Linux_for_Tegra`
2. Run the flash script (as root or sudo):

   ```
   sudo ./cti-nvme-flash.sh cti/orin-nx/boson-orin/fsm-imx678-2cam
   ```

3. Once the flash has completed, the board will reboot.

If you need more details about the complete procedure check out the [ConnectTech tutorial](https://connecttech.com/resource-center/kdb373/) guide that contains all the details.

### Complete the OEM installation
!!! note
    In order to proceed in the following steps, connect the board to a display through an HDMI cable and to a keyboard. Then disconnect the type-C cable previously connected.
    If the OS startup cannot be seen on the screen restart the board power supply after disconnecting the type-C cable.


After booting into the OS, follow the OEM installation with the default options.

Set the user name to `icub` with the hostname `icub-head`. Allow login without password and let the installation process finish.

After rebooting into the graphical OS, connect to an available network and run the following commands in a terminal to update the system:

```bash
sudo apt install -f
sudo apt update && sudo apt upgrade
reboot
```

!!! important

    Check that the correct kernel has been installed on the board by running the following command:

    ```
    ls /boot/dtb/
    ```

    You should expect the following output:

    ```
    kernel_tegra234-orin-nx-cti-NGX020-FSM-IMX678-2CAM.dtb
    ```

### Switch profile on Orin NX
After the reboot process:

1. Open a new terminal on the Orin NX and run `sudo cti-orin-nx-nano-fdt.sh`
2. Follow the interactive procedure and select `Boson for Orin (NGX020)`, the profile for the FRAMOS IMX678 cameras, i.e. `Base + FSM IMX678 (2 CAM)` and finally `orin-nx`.
3. Once the script exits, run `sync` and `reboot` to finalize the changes.

    ![post-flash](../img/post-flash.png)

## Post-flashing operations

### Install FRAMOS drivers

Browsing the [`FRAMOS Github`](https://github.com/framosimaging) organization, it's possible to download and install the [`framos-jetson-drivers`](https://github.com/framosimaging/framos-jetson-drivers/blob/l4t-r36.4.3/README.md) and [`framos-jetson-libsv`](https://github.com/framosimaging/framos-jetson-libsv/wiki/Clone,-Install-and-Run-on-target-system(Jetson-platform)) by following the detailed procedure in the README.md of the repositories. A further guide is proposed here to help even more in the installation.

!!! important
    It is fundamental to note that the `framos-jetson-drivers` should be installed only if the BSP version installed is older than `v36.4.4`, since from this version the BSP and SDK already install the necessary module for configuring the camera device. Therefore, the optimal way to proceed in any case is to check if after the installation of the BSP and the configuration of the carrier the camera device is already found by running the command: `ls /dev/video*`. If that is not found, it is necessary to proceed with the installation of `framos-jetson-drivers`.

#### framos-jetson-drivers

First of all, it is necessary to follow the [guide](https://github.com/framosimaging/framos-jetson-drivers/wiki/Clone,-Compile-and-Install-on-target-system(Jetson-platform)) to install the source code on the target system, which, in this case, is the Jetson board.

After that, you need to configure the sensor: to be more flexible, it is recommended to follow the [command line procedure](https://github.com/framosimaging/framos-jetson-drivers/wiki/Command-line-version) rather than the interactive one. For a configuration consisting of 2 FRAMOS IMX678 sensors, it is necessary to run the following command:

```
sudo jetson-config-camera-cli.py -n "Framos FPA-A/P22" "Framos IMX678-CAM0-2Lane" "Framos IMX678-CAM1-2Lane"
```
!!! note
    The exact name of the FPA can be checked by running the command with only the -l option
    ```
    sudo jetson-config-camera-cli.py -l
    ```
More information can be found in the README.md of the repository linked above.

#### framos-jetson-libsv

Here the [procedure](https://github.com/framosimaging/framos-jetson-libsv/wiki/Clone,-Install-and-Run-on-target-system(Jetson-platform)) is easier: after cloning the repository and checkout on to the branch of your Jetpack (if you follow the instruction till this section, it would be `l4t-r36.4.3`), you need to run the follow:

```
cd ~/framos-jetson-libsv/bin
sudo ./install.sh
```

As soon as the installation procedure has finished, please power off the Orin NX. Then plug-in your cameras to the `CAM1` and `CAM2` connectors, and finally power on the board again.

!!! warning  

    During the flashing procedure, the profile `fsm-imx678-2cam` has been selected, which means that two cameras could be used with this configuration. For this reason, only `CAM1` and `CAM2` connectors are enabled to read the data from the FRAMOS-IMX678, while CAM3 and CAM4 are not. Please, be sure that they are properly connected.

Check if the cameras are detected running `ls /dev/video*` from the command line.