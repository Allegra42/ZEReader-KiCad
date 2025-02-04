# ZEReader-Pico

KiCad project for the ZEReader PCB.
This project uses GitHub Actions and KiBot for CI/CD.

Output can be downloaded in the Actions section.
Includes:
- BoM (interactive for manual assembly and classical HTML)
- Drill file (.drl)
- Gerber files (.gbr)
- KiRi KiCad Revision Inspector files and server
  To make use of KiRi, move everything besides 'kiri-server' in a subdirectory called 'web'
  and start the server using 'python kiri-server .' from the KiRi directory
- PCB Renderings
- PDF Schematic
- ERC Output (HTML)
- DRC Output (HTML)

All CI generated output files like schematic and pcb should contain the git revision hash
of the commit they were generated from to clearly identify the exact design version.
The git revision hash is also added as a silk screen label to the manufacturing files.

This intended to help with a more agile approach in hardware development.
Besides, KiRi makes it easy to visualize and understand changes in schematic and pcb files tracked by git.
