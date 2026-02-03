This is an easy method that works for the current version.
1. Use UPX to extract HWiNFO64.EXE, command line: upx.exe -d HWiNFO64.EXE. 
2. Use HxD to modify the extracted HWiNFO64.EXE.
3. Search for the location of the byte sequence “3D 00 2E 93 02 76 7B” and edit the byte “76” to “EB”.
4. Search for the byte sequence “20 75 69 41 63 63 65 73 73 3D 22 74 72 75 65 22” and edit each byte to “20”.
    

[https://github.com/upx/upx/releases/](https://github.com/upx/upx/releases/)

[https://mh-nexus.de/en/downloads.php?product=HxD20](https://mh-nexus.de/en/downloads.php?product=HxD20)