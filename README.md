# Dump emuMMC titles to NSP

A detailed guide on how to dump titles located on emuMMC to NSP. Useful to backup an entire library in one go.

It implants the SYSTEM partiton (which contains import title data) of an emuMMC to a sysMMC so games can be dumped with SDSwitchTool.

## Requirements
- NxNandManager : https://github.com/eliboa/NxNandManager
- HacDiskMount : https://switchtools.sshnuke.net/
- SwitchSDTool : https://github.com/CaitSith2/SwitchSDTool
- Windows

## Prerequisites

- a sysNAND backup (might need to be on the same FW as your emuNAND, not sure)
- prod.keys (use Lockpick_RCM https://github.com/shchmue/Lockpick_RCM)

## Guide

1. Extract the required software into individual folders.

### Getting the SYSTEM partiton from your emuMMC
1. Turn off your switch and eject the SD card.
2. Mount the SD card on your computer.
3. Open NxNandManager then open new drive (CTRL + D).
4. Select the drive labelled "FULL NAND".
5. Scroll down to the SYSTEM partiton, right click it and select "Dump to file".
6. Save the SYSTEM partiton somewhere handy. 

### Patching the sysNAND with the SYSTEM partiton
1. Open NxNandManager then open file (CTRL + O). 
2. Go to your sysNAND backup folder and open rawnan.bin or rawnand.bin.00.
3. Scroll down to SYSTEM, right click and select "Restore from file".
4. If your backup is split in multiple parts, click on "FULL DUMP" to save your backup to rawnand.bin which is readable by HacDiskMount.
5. Close NxNandManager once it's done.

### Decrypt and mount the SYSTEM partition
1. Open up hac disk mount with administrator priveleges (this is mandatory in order to install the Virtual Drive driver.).
2. Open up rawnand.bin in HacDiskMount.
3. Double click on "PRODINFO".
4. In the "Crypto" field, paste the first half of bis_key_00 from prod.keys. Paste the second half in "Tweak".
5. Click on "Test". Make sure the result says "Entropy OK".
6. Click on "Browse" in the "Dump to File" area, and browse to the location where you extracted SwitchSDTool.
7. Click on "Start".

////

8. Close the PRODINFO window.
Double click on SYSTEM.
9. In the "Crypto" field, paste the first half of bis_key_02 from prod.keys. Paste the second half in "Tweak".
10. Click on "Test". Make sure the result says "Entropy OK".
11. In the "Virtual drive" area, click on "Install".
12. Click on "Mount" to mount the virtual drive to "A:".

### Dump the games to NSP using SwitchSDTool

#### Prepare your SD card
1. At the root of your SD card, rename the "Nintendo" folder to something else (e. g. "NintendoOLD").
2. Cut the emuMMC "Nintendo" folder (typically located in \emuMMC\RAW1) and paste it at the root of your SD card.

#### Setup SwitchSDTool
1. Copy prod.keys to the folder where you extracted SwitchSDTool, and rename it to "keys.txt".
2. Open SwitchSDTool (f it returns an error, make sure .NET Framework 4.7.1 is installed).
3. Click on "Select SD Folder". Choose the Drive that the SD is mounted to.
4. Click on "Select System Path". Choose the drive letter you mounted the SYSTEM partition on. (A: drive by default).
5. Click on "Select Decryption Path". Choose where you want the decrypted NCAs to be (creating a new "NCA" folder is recommended).
6. Click on "Select NSP Output Path". Choose where you want your NSP dumps to be saved(creating a new "NSP" folder is recommended).
7. Get the "eticket_rsa_kek" value (Google it if you don't have it in keys.txt).
8. Click on "Find SD Key". The log should say "SD Key Loaded".
9. Click on "Load RSA KEK". The log should say "RSA Key extracted successfully from PRODINFO.bin".

### Extracting NCAs and dumping NSPs
1. Click on "Extract Tickets". The log should say "Dumping Tickets" followed shortly by "Done. n Tickets dumped".
2. Click on "Decrypt NCAs". The log should show a bunch of "Processing --file--.nca - Decrypting, Done. Verifying, Verified" (may also start with Joining, Done).
3. Click on the Games Tab, then Click on "Parse NCAs".  After it is done parsin, all of your games present on the SD card should be listed, along with any update and DLC.
4. Click on your preferred language, and move it to the top by clicking on "Move Up". Order them by preference, the preferred ones being on top.
5. Click on "Pack ALL NSPs" to pack everything. To select one or more games, click on "Pack Selected NSP" to only pack your selection of NSPs.
6. The process may take a while depending on the size of your selection.

### Final steps
1. Close SwitchSDTool.
2. In HacDiskMount, unmount the SYSTEM partiton and close the software.
3. Cut the emuNAND "Nintendo" folder at the root of your SD to its original location (\emuMMC\RAW1).
4. Rename your original Nintendo folder to "Nintendo".
5. Eject your SD card, plug it into your Switch .


## Thanks

- Eliboa for NxNandManager
- rajkosto for HacDiskMount
- CaitSith2 for SwitchSDTool. This guide is pretty much ripped off from his README, but tweaked for emuNAND











