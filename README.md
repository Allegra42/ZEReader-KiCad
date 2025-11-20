<!-- # ZEReader-PCB
ZEReader-PCB is a custom hardware design, intended to be used with the [ZEReader firmware](https://github.com/Allegra42/ZEReader).  
The project is supported by [AISLER](https://aisler.net/en?utm_source=zereader), which sponsor prototying PCBs. See [Production](#production) for more information.  
Thanks [AISLER](https://aisler.net/en?utm_source=zereader)!

- [ZEReader-PCB](#zereader-pcb)
  - [PCB Revisions](#pcb-revisions)
    - [Revision 2](#revision-2)
      - [Known Issues Rev 2](#known-issues-rev-2)
    - [Revision 1](#revision-1)
      - [Known Issues Rev 1](#known-issues-rev-1)
  - [CI and Automation](#ci-and-automation)
  - [Production](#production)
  - [License](#license)

## PCB Revisions
### Revision 2
![PCB rendering rev2](pictures/ZEReader-Pico%20v2.png)

ZEReader revision 2 is a major redesign of the PCB.
Major improvements and changes in rev 2:
- connected USB-C datalines and added additional ESD and overvoltage protection with USB optimized ESD diodes and a polyfuse
- switched to BQ25170 as a charging controller
- removed the on-PCB NTC for monitoring the lipo temperature in favor for an integrated one
- implemented a new button-based on/off mechanism [based on a self-holding circuit](https://marx.engineer/blog/a-gentle-power-off/)
- fixed FFC connector inversion from rev 1
- removed switch in the display's booster circuit, if you want to use an EPD that needs a 3 ohms resistor populate R11 accordingly
- connect all SD card connector datalines
- reworked and improved general schematic clarity
  - take advantage of the hierarchical sheets
  - use new Pi Pico footprint
  - adopt netclasses in the schematic

#### Known Issues Rev 2
- None, the PCB *is not produced yet*!

### Revision 1
Caution: v1 is working, but the FFC connector is inverted.
Twisting the cable solves the issue for now.
This is to be fixed in the next revision!

![PCB rendering](pictures/ze-ray-front.png)

#### Known Issues Rev 1
- FFC connector is inverted, twisting the cable is a quick fix
- R11, which defines ISET for the charging controller BQ24092 is too large. 2.7 kohms set a charging current of 200 mA and thus 200 mA for ISET2. In this configuration, the device can not be driven standalone by USB-C. 

## CI and Automation
This project uses GitHub Actions and KiBot for CI/CD.

Outputs can be downloaded in the Actions section. They include:
- BoM (interactive for manual assembly and classical HTML)
- Drill file (.drl)
- Gerber files (.gbr)
- KiRi KiCad Revision Inspector files and server
  To make use of KiRi, move everything besides 'kiri-server' in a subdirectory called 'web'
  and start the server using 'python kiri-server .' from the KiRi directory
- PCB Renderings
- PDF Schematic/PCB printout from KiCad
- ERC Output (HTML)
- DRC Output (HTML)
- Fabrication Ready Zip

All CI generated output files like schematic and pcb should contain the git revision hash
of the commit they were generated from to clearly identify the exact design version.
The git revision hash is also added as a silk screen label to the manufacturing files.

This intended to help with a more agile approach in hardware development.
Besides, KiRi makes it easy to visualize and understand changes in schematic and pcb files tracked by git.

## Production
[AISLER](https://aisler.net/en?utm_source=zereader) supports the ZEReader project with prototyping PCBs. Hugh thank you for that!

To get the lastest git head manufactured, just follow this link for [Uploading to AISLER](https://aisler.net/p/new?url=https://raw.githubusercontent.com/Allegra42/ZEReader-KiCad/refs/heads/main/ZEReader-Pico.kicad_pcb&ref=github).

Alternatively, the GitHub Actions output already contains a prepacked ZIP file with everything needed for production (Gerber files as well as the .kicad_pcb) and correct git revisions filled in.

## License
While the project is license as CERN-OHL-S v2, the squirrel logo is a registered design and not allowed to be used in other contexts. -->


# ZEReader KiCad

The ZEReader PCB is the custom open-hardware board designed for the [ZEReader](https://github.com/Allegra42/ZEReader) project — an open hardware eBook reader approach.

The project is supported by [AISLER](https://aisler.net/en?utm_source=zereader), which sponsors prototype boards. See [Production](#production) for more information.
Huge thanks to [AISLER](https://aisler.net/en?utm_source=zereader) for their support!

---

## Table of Contents

- [ZEReader KiCad](#zereader-kicad)
  - [Table of Contents](#table-of-contents)
  - [PCB Revisions](#pcb-revisions)
    - [Revision 2](#revision-2)
      - [Known Issues Rev 2](#known-issues-rev-2)
    - [Revision 1](#revision-1)
      - [Known Issues Rev 1](#known-issues-rev-1)
  - [CI and Automation](#ci-and-automation)
  - [Production](#production)
    - [Option 1: Tip of the Tree Production](#option-1-tip-of-the-tree-production)
    - [Option 2: Using Pre-Generated Artifacts](#option-2-using-pre-generated-artifacts)
  - [Thanks](#thanks)
  - [License](#license)

---

## PCB Revisions

### Revision 2

**Current Status:** The design is complete, but the board ***is not produced yet***!  

This revision is a major redesign, focused on fixing Rev 1 issues and significantly improving power handling and robustness.

![PCB rendering rev2](pictures/ZEReader-Pico%20v2.png)

Major improvements and changes in rev 2:

- Connected **USB-C datalines** and added additional **ESD and overvoltage protection** with USB optimized ESD diodes and a polyfuse.
- Switched to **BQ25170** as a charging controller.
- Removed the on-board NTC for monitoring the LiPo temperature in favor of an integrated one.
- Implemented a new **button-based on/off mechanism** [based on a self-holding circuit](https://marx.engineer/blog/a-gentle-power-off/).
- Fixed **FFC connector inversion** from rev 1.
- Removed switch in the display's booster circuit; populate R11 accordingly for EPDs that require a 3-ohm resistor.
- Connected all SD card connector datalines.
- Reworked and improved general schematic clarity (hierarchical sheets, new Pi Pico footprint, netclasses adoption).

#### Known Issues Rev 2

| Issue | Workaround/Impact |
| :--- | :--- |
| None | The board **is not produced yet** and awaits production and testing. |

### Revision 1

**Current Status:** The board is **working**, but the FFC connector is inverted.
Twisting the cable solves the issue for now.

![PCB rendering](pictures/ze-ray-front.png)

#### Known Issues Rev 1

| Issue | Workaround/Impact |
| :--- | :--- |
| **FFC Connector** | **Inverted!** Requires **twisting the FFC cable** before connection. |
| **Charging Circuit**| R11 (ISET for BQ24092) is too large (2.7-kohms). This sets charging current to 200 mA, which is insufficient to drive the device standalone by USB-C. |

---

## CI and Automation

This project uses **GitHub Actions** and **KiBot** for continuous integration and delivery. This ensures that all manufacturing files are up-to-date and directly traceable to the source code.

Outputs can be downloaded in the Actions section. They include:

- **Fabrication Ready Zip**
- Gerber files (.gbr)
- Drill file (.drl)
- Bill of Materials (BoM) (interactive for manual assembly and classical HTML)
- Board Renderings and PDF Schematic/Board printouts
- Verification Reports: ERC Output (HTML), DRC Output (HTML)
- KiRi KiCad Revision Inspector files (for visualizing design changes)

> **Version Control:** All CI-generated output files like schematic and board should contain the **git revision hash** of the commit they were generated from to clearly identify the exact design version. The git revision hash is also added as a silkscreen label to the manufacturing files.

---

## Production

[AISLER](https://aisler.net/en?utm_source=zereader) supports the ZEReader project with prototyping boards. Huge thank you for that!

### Option 1: Tip of the Tree Production

To get the design from the latest commit manufactured, just follow this link for **[Uploading to AISLER](https://aisler.net/p/new?url=https://raw.githubusercontent.com/Allegra42/ZEReader-KiCad/refs/heads/main/ZEReader-Pico.kicad_pcb&ref=github)**.

### Option 2: Using Pre-Generated Artifacts

The GitHub Actions output already contains a **prepacked ZIP file** with everything needed for production (Gerber files as well as the `.kicad_pcb`) and correct git revisions filled in. This is the **best way to order a specific, verified commit version**.  
The generated output is optimized for AISLER. If using a different manufacturing service, please verify that the production files meet their specific requirements.

1.  Navigate to the **GitHub Actions** page for the desired commit.
2.  Download the **`KiBot_Outputs`** artifact.
3.  Upload the Gerber files or the `.kicad_pcb` to [AISLER](https://aisler.net/en?utm_source=zereader).

---
## Thanks
- to @casartar for reviewing the design and some great tips and ideas!

## License

While the project is licensed as **CERN Open Hardware Licence Version 2 - Strongly Reciprocal (CERN-OHL-S v2)**, the squirrel logo is a registered design and not allowed to be used in other contexts.