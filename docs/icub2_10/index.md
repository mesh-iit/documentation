# iCub 2.10

## Purpose and scope

`iCub v2.10` introduces a new head and onboard computing architecture while
retaining the main body architecture of iCub v2.7. Its principal changes are:

- the tendonless [**neck MK3**](../necks/neck_mk3.md);
- new **eyes MK4** and two **4K FRAMOS IMX678 cameras** ([UKIT009](../upgrade_kits/head_4k/support.md));
- an **NVIDIA Jetson Orin NX** in the head for camera acquisition and GPU processing;
- an **Intel i7 COM Express Type 10** computer in the backpack;
- a network configuration that accounts for both onboard computers.

This page explains what changed, how it affects users, and where to find the
detailed procedures.

## Main differences

| Area | Earlier iCub 2.x | iCub 2.10 | User impact |
| --- | --- | --- | --- |
| **Neck** | Tendon-based neck | [Neck MK3](../necks/neck_mk3.md) | Different mechanics, limits and maintenance |
| **Eyes** | Low resolution cameras | Eyes MK4 with FRAMOS IMX678 cameras | Different camera setup, optics and calibration |
| **GPU** | External GPU workstation | Jetson Orin NX and Boson carrier | JetPack, carrier BSP and camera setup required |
| **CPU** | Intel i7 COM Express Type 10 (Type 6 in older iCub) in the head | Intel i7 COM Express Type 10 in the backpack | Different computer and backpack arrangement |
| **Network** | Earlier onboard-computer arrangement | Two onboard computers | Hostnames, addresses and routing |
| **Head kinematics** | iCub `v2.x` configuration | head_version `v2.10`| Required by software using head/camera geometry (i.e. **iKinGazeCtrl**) |

## Neck MK3

**Neck MK3** replaces the tendon-based neck with a compact tendonless serial
mechanism. Its joints are ordered pitch, roll and yaw, from bottom to top. See
[Neck MK3](../necks/neck_mk3.md) for mechanical details and ranges of motion.

## Eyes MK4 and FRAMOS IMX678 cameras

The **eyes MK4** use two **FRAMOS IMX678** modules connected to the Orin NX through the
Connect Tech Boson carrier. The changed camera transform requires applications
such as the gaze controller to select **head_version `v2.10`**, introduced and documented from
software distribution [2024.11.0](../sw_versioning_table/2024.11.0.md).

Detailed references:

- [UKIT_009 — iCub head with 4K cameras](../upgrade_kits/head_4k/support.md)
- [JetPack installation](../icub_operating_systems/icubos/jetpack.md)
- [FRAMOS IMX678 setup](../icub_operating_systems/icubos/setup-framos-imx678.md)
- [Stereo calibration](../icub_robot_calibration/icub-stereo-calib.md)

## Onboard computers

### icub-head

The head houses a **Jetson Orin NX on a Connect Tech Boson carrier**. The installation procedure is described in the [JetPack](../icub_operating_systems/icubos/jetpack.md) page, while the guide on how to configure it with the **FRAMOS IMX678 cameras** is described in [dedicated setup](../icub_operating_systems/icubos/setup-framos-imx678.md) paragraph.


### icub-torso

The backpack now contains an **Intel i7 COM Express Type 10 computer**. The details can be found in the [UKIT_010](../upgrade_kits/backpack/support.md) and
[iCub CPU boards](../icub_cpu_boards/icub_cpu_boards.md). This board is responsible for doing the motor control and thus running the `yarprobotinterface`.

## Network architecture

The presence of a second onboard computer changes how users connect to the robot and how
camera data reaches setup machines. The [network page](networking.md) collects
the information about hostnames, interfaces, subnets, addresses,
gateways, routing and YARP name-server location.
