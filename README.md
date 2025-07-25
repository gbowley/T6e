# T6e
WIP decompilation of the EFI T6E ECU.
Based on a full dump of the P138 firmware (Exige/Evora), including Bootloader, Adaptations, Coding, Calibration, Program, and SRAM.

# Usage
Open .gzf in Ghidra.

Importing r13 correction script to ghidra and binding to a key is recommended - When examining decompiled code the r13 script can be used to produce C which refers directly to existing addresses, rather than abstractions. 

# 
