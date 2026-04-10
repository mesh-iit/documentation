# Setup ergoCub Screen

!!! info

    This procedure applies only to `ergocub-head` and must be performed after the [JetPack installation](../../icub_operating_systems/icubos/jetpack.md) has been completed.

When you start the ergoCub head for the first time, the screen will display a desktop showing the NVIDIA logo. While this is generally fine, it requires the user to manually run the [`ergoCubEmotions`](https://github.com/mesh-iit/ergocub-software/tree/master/src/modules/ergoCubEmotions) module. This procedure allows you to hide all bars on the desktop and set the wallpaper to one of the images stored in the [expressions folder](https://github.com/mesh-iit/ergocub-software/tree/14599254440686b8a373e1635f046a6821ddee78/src/modules/ergoCubEmotions/expressions/images).

---

## Install GNOME Shell Extensions

In order to hide the top bar and remove notifications, you need to install the required GNOME Shell extensions. Follow these steps:

### Download the Extensions

You'll need to download the extensions from the GNOME Shell Extensions website:

1. Visit [https://extensions.gnome.org/](https://extensions.gnome.org/) in your browser
2. Search for and download the extensions you need (e.g., extensions for hiding the top bar and managing notifications). Currently it is used to install the 2 following extensions:

    - https://extensions.gnome.org/extension/545/hide-top-bar/
    - https://extensions.gnome.org/extension/4099/no-overview/
 
3. Download the `.zip` files to your local machine. It is important to select the exact version depending on your gnome shell version (check the table on the bottom of the download page)

### Install Extensions on ergocub-head machine

Once you have downloaded locally you need to install the extension on the `ergocub-head` machine

1. Copy using the `scp` command the `.zip` file in the `ergocub-head` filesystem (e.g in the `home` dir or in temporary directory)

2. Navigate to the extensions directory (if it is not present you can just create it):
    ```bash
    mkdir -p ~/.local/share/gnome-shell/extensions
    cd ~/.local/share/gnome-shell/extensions
    ```

3. Extract the extension to this directory. The folder name must match the extension's UUID (you can find this in the `metadata.json` file inside the zip):
    ```bash
    unzip -d extension-name /path/to/extension.zip
    ```
    
4. Find the extension UUID by checking the `metadata.json` file:
    ```bash
    cat ~/.local/share/gnome-shell/extensions/extension-name/metadata.json | grep '"uuid"'
    ```

5. Rename the extension folder if needed to use its UUID as the folder name:
    ```bash
    mv extension-name <UUID>
    ```

6. Restart GNOME Shell (on X11, press Alt+F2, type r, and press Enter) or log out and back in to apply changes

7. Enable the extension using GNOME Settings or via the command line:
    ```bash
    gnome-extensions enable <UUID>
    ```

### Alternative: Install via Web Browser

The easiest method is to install extensions directly from [extensions.gnome.org](https://extensions.gnome.org):

1. Visit the extension page on the website
2. Click the toggle switch to install
3. When prompted, confirm the installation
4. The extension will be automatically installed and integrated into GNOME Shell

For more detailed information, refer to:
- Official guide: [https://itsfoss.com/gnome-shell-extensions/](https://itsfoss.com/gnome-shell-extensions/)
- Manual installation guide: [https://www.pragmaticlinux.com/2021/06/manually-install-a-gnome-shell-extension-from-a-zip-file/](https://www.pragmaticlinux.com/2021/06/manually-install-a-gnome-shell-extension-from-a-zip-file/)

---

## Hide the Ubuntu Bar

This guide is based on these [instructions](https://askubuntu.com/a/1264692). 

1. Create a script in the `ergocub-head` home directory:

    ```bash
    #!/bin/bash

    status1=$(gdbus call --session --dest org.gnome.Shell --object-path /org/gnome/Shell --method org.gnome.Shell.Eval string:'Main.panel.actor.visible;')
    status2=$(gdbus call --session --dest org.gnome.Shell.Extensions --object-path /org/gnome/Shell/Extensions --method org.gnome.Shell.Extensions.GetExtensionInfo ubuntu-dock@ubuntu.com | grep "'state': <2.0>" >/dev/null && echo "OFF" || echo "ON")

    if [ "$status1" == "(true, 'false')" ]; then
      gdbus call --session --dest org.gnome.Shell --object-path /org/gnome/Shell --method org.gnome.Shell.Eval 'Main.panel.actor.show();'
    else
      gdbus call --session --dest org.gnome.Shell --object-path /org/gnome/Shell --method org.gnome.Shell.Eval 'Main.panel.actor.hide();'
    fi

    if [ "$status2" == "ON" ]; then
      gdbus call --session --dest org.gnome.Shell.Extensions --object-path /org/gnome/Shell/Extensions --method org.gnome.Shell.Extensions.DisableExtension ubuntu-dock@ubuntu.com
    else
      gdbus call --session --dest org.gnome.Shell.Extensions --object-path /org/gnome/Shell/Extensions --method org.gnome.Shell.Extensions.EnableExtension ubuntu-dock@ubuntu.com
    fi
    ```

2. Run the script to toggle hiding or showing the bars.

---

## Change the Desktop Wallpaper

1. SSH into the `ergocub-head` and use the following command to set the wallpaper:

    ```bash
    gsettings set org.gnome.desktop.background picture-uri <uri-of-the-wallpaper>
    ```

2. If [ergocub-software](https://github.com/mesh-iit/ergocub-software) is installed via the robotology-superbuild, you can use this command:

    ```bash
    gsettings set org.gnome.desktop.background picture-uri file:///usr/local/src/robot/robotology-superbuild/src/ergocub-software/src/modules/ergoCubEmotions/expressions/images/exp_img_1.png
    ```

---

## Clean the Icons from the Desktop

1. Create a folder in the home directory to store the desktop files:

    ```bash
    mkdir ~/all_desktop
    ```

2. Move all files from the desktop to the newly created folder:

    ```bash
    mv ~/Desktop/* ~/all_desktop/
    ```
