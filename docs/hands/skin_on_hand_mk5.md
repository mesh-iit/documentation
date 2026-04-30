# Hand Sensors

The hands MK5.1 have tactile sensors mounted both in the fingertips (finger sensors)
 and in the palm. 

## Palm skin

The palm skin consists of:
- a dedicated plastic holder with slots for the electronics
- an electronics board from the well-established iCub skin electronics, WINGST code **19079.D**
- a textile made skin covering the electronics for force to electrical signal transduction

The palm skin is connected to the **MMA board (rev. B)** together with the fingertip 
skin.
A JST SUR 5 pin cable is needed for this. One side of the cable has free conductors 
for soldering on the pads of the triangle. The connection scheme is represented 
here below:

<p align="center">
    <img  src=    "../img/palm_mount.png"
          width=  "1200">
</p>
<p align="center">
    <sub>Fig.1 – Left: Triangle connection scheme; Right: palm mount fixtures.</sub>
</p>

The patch shapes are the same for left and right hands, only they are rotated 120 degrees in clockwise or counterclockwise direction to accommodate on the support. 

The sensorized palm is then installed on the hand by:
- passing the cable through the dedicated slot in the metal shell
- clamping the conductive black fixture between the plastic and the metal shell to ensure the ground connection
- fix the palm from the inner side with 3 screws
- connect the cable to the MMA board in the dedicated connector.

Then the skin patch can be activated in the `yarprobotinterface` configuration files. 
The signals are natively routed to the correct streams (i.e. ports) by setting the 
correct `skintype = 3` option in the configuration files. The wrappers need to include all signals from 60 to 119 to contain the palm data.

### Mounting the palm skin

The palm skin is a standalone component, mounted with 3 screws M2 on the metal structure of the palm.
The sequence of operations is, taking fig. 1 as a reference:
1. unmount the hand covers and access the interior of the hand
2. pass the integrated cable **1** in the slot on the palm
3. fix the screws **2** on the back of the palm, taking care that the small lip **3** is clamped between the plastic and the metal 
4. connect the cable **1** to the **palm** connector on the MMA
5. the palm is now ready to be used


## Finger sensors
Tactile sensors are deployed on the fingertip. 
The fingertip comprises a 3DMID piece with the patterned taxels and a conventional PCB (the **FT3D**) reading the capacitances and hosting an IMU. 

The taxel mapping is represented in Fig. 2.

<p align="center">
    <img  src=    "../img/taxel_map.jpg"
          width=  "750">
</p>
<p align="center">
    <sub>Fig.2 – Taxel mapping.</sub>
</p>

### FT3D board configuration - rev. 2 
The AD7147 hosted on the FT3D has configurable **I2C address**  to allow for multiple devices. 

The configuration is made through the jumpers **AD0** and **AD1** reported in Fig. 3 by simply soldering 
the desired connection on the dedicated jumper. Also **R1** is to be removed in this revision. 
Depending on the connection (see below) the **IMU** also needs to be removed.
<p align="center">
    <img  src=    "../img/FT3D_Top.jpg"
          width=  "750">
</p>
<p align="center">
    <sub>Fig.3 – Address configuration: the board represented has Address bits (AD0, AD1) = (0, 0).</sub>
</p>

Since the **IMU** is not equipped with similar configurable address pins, we need to remove all the IMUs from unwanted boards before the installation. This will be fixed in rev. 3 of the FT3D.

The complete configuration set is as follows:

#### ergoCub SN000

!!! note 

    In ergoCub SN000 currently the fingertips are not wired to the MMA board.

| finger |  AD0 | AD1 | IMU | I2C dataline | IIT code | 
|:--:|:--:|:--:|:--:|:--:|:--:|
|thumb   | 0    | 0   | LSM6DSLTR | 0      | 17544 | 
|index   | 0    | 0   | LSM6DSLTR | 1      | 17544 |
|middle  | 1    | 0   | no  | 1            | 17545 |
|ring    | 0    | 1   | no  | 1            | 17546 |
|pink    | 1    | 0   | no  | 0            | 17545 |

#### ergoCub equipped with MMA rev. B (from ergoCub SN001)

These robots are equipped with the MMA rev. B **IITCODE 16872.B**

| finger |  AD0 | AD1 | IMU | I2C dataline |  IIT code |   
|:--:|:--:|:--:|:--:|:--:|:--:|
|thumb   | 0    | 0   |  IIM-42652 | 0     | 15467.B |  
|index   | 0    | 0   |  IIM-42652 | 1     | 15467.B  |
|middle  | 0    | 0   |  IIM-42652 | 2     | 15467.B  |
|ring    | 0    | 0   |  IIM-42652 | 3     | 15467.B  |
|pink    | 0    | 0   |  IIM-42652 | 4     | 15467.B  |

No customization of the boards is needed. They are purchased with the correct jumper configuration.

I2C dataline is decided at the MMA level through the connector assignment. 
To enable the use of **PIN 7** in the connector as an additional I2C line (SDA_4), 
- the **MTB4** needs a **firmware version greater than 1.24**;
- the **MTB4C** needs a **firmware version greater than 2.3**. 

### Mounting the 3DMID 

#### Needed material (for one hand):

|IITCODE | description | quantity |
|--|--|--|
| 17628 | support for soldering | 5 |
| 17627 | base for soldering support | 1 |
| 16619 | 3DMID shells| 5| 
| 15467 | FT3D board| 5 | 
| 17377 | rubber fingertip | 5 |
| | 1.6x6mm screws | 5 | 
| | 1.6x8mm screws | 5 | 

Plus:

1. low temperature solder (LTS): used Indium solder wire **SMDIN52SN48**[^1]
2. dedicated tips for the soldering iron
3. dedicated flux for LTS
4. screwdriver

<p align="center">
    <img  src=    "../img/list_material.png"
          width=  "750">
</p>
<p align="center">
    <sub>Fig.4 – Some material needed to mount the fingertips.</sub>
</p>

[^1]: See [link](https://www.chipquik.com/store/product_info.php?products_id=630003) or buy from usual suppliers of electronics goods.

#### Procedure

<p align="center">
    <img  src=    "../img/3dMID_fixed.png"
          width=  "500">
</p>
<p align="center">
    <sub>Fig.5 - fixing the 3DMID to the soldering support.</sub>
</p>

- Fix the 3DMID to the soldering support with **1.6x6mm** screw.
- Plug the soldering support on the base.

<p align="center">
    <img  src=    "../img/3dmid_plugged.png"
          width=  "500">
</p>
<p align="center">
    <sub>Fig.6 – soldering support plugged into the base.</sub>
</p>

- Set the soldering iron to 250 C, apply flux and pre-tin the pads on the 3DMID.
- Apply flux and pre-tin the castellated holes on FT3DB.
- Configure the FT3DB jumpers (see section above).
- Place the FT3DB on the 3DMID aligning the soldering pads.
- Apply some flux if needed and solder a couple of pads holding the FT3DB in position.
- Go on and solder all the pads.

<p align="center">
    <img  src=    "../img/soldered.png"
          width=  "500">
</p>
<p align="center">
    <sub>Fig.7 – soldered FT3DB on the 3DMID shell.</sub>
</p>

At this point the device is ready for testing, just connect it to the MMA with the dedicated cable. 
To fully mount the fingertip, proceed with the next steps:

- Put on the rubber fingertip cod. 17377.

<p align="center">
    <img  src=    "../img/3DMIDwCap.png"
          width=  "500">
</p>
<p align="center">
    <sub>Fig.8 – adjusted rubber fingertip on 3DMID shell.</sub>
</p>

- Test the fingertip in this condition.

<p align="center">
    <img  src=    "../img/3DMIDwCap_support.png"
          width=  "500">
</p>
<p align="center">
    <sub>Fig.9 – 3DMID fingertips with and without the rubber cap.</sub>
</p>

- To mount on the finger distal phalanx (fig. 9):
    1. Connect the cable exiting from the phalanx.
    2. Slide the rear of the assembly into the bore with a small inclination.
    3. Push up and ahead to insert the locking clip into its slot.

At this point, the assembly should look sturdy and precisely fit, in addition you can tighten it with **1.6x8 mm screw**. Now it's ready for testing the signals. 

<p align="center">
    <img  src=    "../img/insertion.png"
          width=  "750">
</p>
<p align="center">
    <sub>Fig.10 – 3DMID fingertip insertion procedure, left: connection, center: insertion of the device,  right: 3DMID device inserted into the distal phalanx.</sub>
</p>

### Encoders
The finger position (closing and adduction angles) are read out by a set of FAP cards (Finger Absolute Position), each one coupled with a small magnet rigidly connected to the corresponding joint.
Each FAP has the same I2C address, thus **one I2C data line is needed for one FAP**. This is implemented at the PCB level. 

## MMA Connection scheme
Three Molex 8-Pin connectors are the inputs for three dedicated MTB cards:
- One MTB for tactile reading.
- Two MTBs for FAP reading: max. 8 FAPs can be connected (4x MTB).

The power suppy and signals are then routed to the connectors towards the FAPs and Fingertips:
- **JST SURS** 5 contacts for the fingertips.
- **JST XRS** 4 contacts for the FAPs.

The family of connectors on the same device are identified with the REF DES: i.e., Picoblade **J1** goes to connectors **J1** 1, **J1** 2 and so on; Picoblade **J2** goes to **J2** 1 etc. 
Details are summarized in the table below:

| connector | description | sensor | 
|--|--|--|
|**J1** | Molex 8-Pin | MTB for the skin|
|**J2** | Molex 8-Pin | MTB for the 1st set of FAPs |
|**J3** | Molex 8-Pin | MTB for the 2nd set of FAPs |
| J10-J15 | JST SURS  | fingertips and palm - corresponding to **J1** |
| J20-J23 | JST XRS | encoders - corresponding to **J2** |
| J30-J33 | JST XRS | encoders - corresponding to **J3** |

The encoders are connected with the following logic:
- Finger position encoders are to be routed to one MTB-FAP.
- Adduction encoders are to be routed to the other MTB-FAP.


The schematic of the MMA is shown below.

### Tactile sensors
<p align="center">
    <img  src=    "../img/fingertips_connection.png"
          width=  "750">
</p>
<p align="center">
    <sub>Fig.11 – Skin connections. </sub>
</p>

The tactile sensors are connected to the MMA as in Fig. 11. Both fingertips and palm tactile sensors have a 5-pin SUR connector. Each connector on the MMA is dedicated to a specific finger or the palm.

### Encoder connection
The encoders are connected as reported in the table above and in the schematic snapshot in Fig. 12.

<p align="center">
    <img  src=    "../img/encoders_connection.png"
          width=  "750">
</p>
<p align="center">
    <sub>Fig.12 – FAPs connections. The FAP mapping should be reported in the configuration files for proper working of the joints.</sub>
</p>

## Software items
To use correctly the data from the sensors we need to have the following information embedded in the configuration files.

### Signal wrapping in configuration files 
For the configuration of the **Wrapper file** in the robots-configuration tree, for streaming through the **YARP** 
services and signal visualization, the mapping of the signals is reported in the table below:

#### ergoCub SN000 & SN001

| Finger | board nr. | Taxel Index | 
|-- |--|--|
| Thumb  | 4 | 48-59  | 
| Index  | 0 | 0-11   | 
| Middle | 1 | 12-23  | 
| Ring   | 2 | 24-35  | 
| Pink   | 5 | 60-71  | 
| Palm   | NA |NA |  

#### ergoCub with MMA rev.B

| Finger | board nr. | Taxel Index |
|-- |--|--|
| Thumb  | 0 | 0-11  | 
| Index  | 1 | 12-23 |
| Middle | 2 | 24-35 |
| Ring   | 3 | 36-47 |
| Pink   | 4 | 48-59 |
| Palm   | 5,6,7,9 |  60-95, 108-119 |

### AD7147 configuration
The values for the mk2 fingertip are reported here, to be implemented in **.xml files** with the proper labeling:

| Parameter |  Value | 
|--|--|
| Bitshift | 2 |
| CDC offset | 0x0000 | 
| No load value | note[^2] |

[^2]: The No load value can be choosen to be lower than 0xF0 (240) to allow for some room for opposite polarity signals to be recorded. In this case, the set level must be forwarded to high level tools such as SkinGUI etc. for a proper managing of events. A nice choice could be a value of about 0xC0 (192) to have ~60 ADC counts of headroom for opposite sign forces, i.e., shear forces, to be measured with the lateral taxels or elastic effects for non-touched taxels to improve force measurement.

### Encoders mapping in the configuration files
🚧 WIP 🚧
