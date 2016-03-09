# How to extract MacVenture ROMs from the executables

- Install ResourceHacker and HexEditor (HxD).
- In ResourceHacker, open the exe file.
- Find the only two resources that are not either JavaScript or images.
- Extract the IIgs version:
    - The IIgs file is the resource that begins with 2IMG (32 49 4D 47).
    - In the hex text, right-click->select all, and Ctrl-C (copy).
    - Paste in the Hex Editor.
    - In the hex editor, save the file as [gamename].2mg (e.g. Shadowgate.2mg).
    - Move the file to the webventure folder.
- Extract the Mac version:
    - Locate the resource. It's the other plain hex one.
    - Follow the same steps, but this time save it as [gamename].dsk
    
- Have fun :)