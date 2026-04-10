# Robot user environment

!!! info
    This guide applies to both **iCub** and **ergoCub** robots. Throughout this guide, references to `icub` should be replaced with your specific robot name:

    - For **iCub**: use `icub` 
    - For **ergoCub**: use `ergocub`

The main user configured on all robot Setup machines is usually `icub` (SID: 1000 - GID 1000), however it can be changed with `ergocub` as stated above (the SID and GID are typically the same).

All the environment configurations required for this user are stored in a separate file that is loaded every time a bash session is started.

## Note
If you installed your system starting from an image (eg. the [iCubOS - Installation from image](installation-from-image.md) chapter, or equivalently the [ergoCubOS - OS Installation](../../ergocub_operating_systems/index.md)), the steps below have already been added into the image.

# Users and Passwords

The default user account is

**Username** : `icub`
**Password** : `icub`

If you want to change the default password simply execute (*this works only if you are using persistence*)

`passwd icub`

**NOTE**: As in any Ubuntu installation, the root user has no password, this means that the direct login (i.e. *ssh root\@icub-head*) is disabled, but you can always do

`sudo su - `


# The bashrc

The user enviroment configurations (for bash sessions) are stored in the file

`~/.bashrc_iCub`

## Online updated version

You can find the updated default .bashrc_iCub file online.
There are two versions of the iCub environment file:

- [`bashrc_iCub_superbuild`](https://raw.githubusercontent.com/mesh-iit/icub-os-files/master/user-environment/bashrc_iCub_superbuild) - a special version of icub user environment, in case of compilation of the repository [robotology-superbuild](https://github.com/robotology/robotology-superbuild)
- [`bashrc_iCub`](https://raw.githubusercontent.com/mesh-iit/icub-os-files/master/user-environment/bashrc_iCub) - the standard version of icub user environment, if you DO NOT intend to use the repository `robotology-superbuild`

the above files must be renamed to `.bashrc_iCub` and saved in the user home directory, along with the `.bashrc` file.

## How to setup the enviroment properly

To use the `~/.bashrc_iCub` file to setup the environment, the following lines:
```bash
if [[ $- == *i* ]] || [[ -n "$SSH_CLIENT" ]] || [[ -n "$SSH_TTY" ]]; then
  #Load the iCub custom bashrc
  if [ "$HOME" != "" ]; then
      ICUBRC_FILE="${HOME}/.bashrc_iCub"
  else
      ICUBRC_FILE="/home/icub/.bashrc_iCub"
  fi
  if [ -f "$ICUBRC_FILE" ]; then
      source $ICUBRC_FILE
  fi
fi
```
should be added at the beginning of file `~/.bashrc` just _BEFORE_ the following lines:
```bash
# If not running interactively, don't do anything
case $- in
   *i*) ;;
     *) return;;
esac
```

The reason why the `.bashrc_iCub` needs to be added at the beginning of `~/.bashrc` is that file must be loaded every time an interactive or ssh bash sessions are started. The lines of code after `# If not running interactively, don't do anything` make the `~/.bashrc` file exit if executed in a non-interactive shell.

## Required configuration

To customize the above user environment, you ought to manually make some changes:

- The **YARP_ROBOT_NAME** - you must insert your robot name, in the following line and remove the leading "#"
```bash
#export YARP_ROBOT_NAME=
```

# Groups

Add the user icub to the following groups

- video
- audio
- tty
- dialout
- i2c
- bluetooth

use the next command to perform that action
```
usermod -a -G video,audio,tty,dialout,i2c,bluetooth icub
```

