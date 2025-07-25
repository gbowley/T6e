# T6e Unpacked
Decompilation of the EFI T6E ECU. Experimental and incomplete.

Based on a full dump of the P138 firmware (Exige/Evora), including Bootloader, Adaptations, Coding, Calibration, Program, and SRAM.

# Usage in Ghidra
Open .gzf in Ghidra.

Importing the r13 correction script to ghidra and binding to a key is recommended - When examining decompiled code the r13 script can be used to produce C which refers directly to existing addresses, rather than abstractions. 

# Usage in RomRaider
Open t6edef.xml in RomRaider 

I have included a definition which allows control of the main injection, ignition, airmass, vvt, and limit parameters. This is intended for development purposes, use at your own risk.

This definition expects the full ECU dump, and maps memory regions accordingly. To modify individual calibration files for use in .CRP, adjust the memory offset and expected filesize accordingly.

# Memory Map

| Name  | Start | End | Length |
| ------------- | ------------- | ------------- | ------------- |
| Bootloader | 00000000  | 0000ffff  | 0x10000  |
| Adaptations  | 00010000 | 0001bfff  | 0xc000 |
| Coding | 0001c000 | 0001bfff | 0x4000 |
| Calibration | 00020000 | 0003ffff | 0x20000 |
| Program | 00040000 | 000fffff | 0xc0000 |
| SRAM Program (Partial) Copy | 40000000 | 400014b7 | 0x14b8 |
| SRAM Coding Copy | 400086a8 | 400086eb | 0x44 |
| SRAM Calibration Copy | 40008e24 | 4000effd | 0x61da |

Note that the ECU uses the SRAM copy of calibration/coding data for runtime operations.

Modification of live SRAM can be done using [TunerV2](https://github.com/gbowley/Tuner-T6e-v2).

Modification of flash program can be done using [LotusFlasher](https://github.com/Alcantor/LotusECU-T4e)

# Key Functions

1. MAIN_PROC_LOOP - Responsible for initialisation of ECU memory and hardware status checks. Then initiates the main infinite loop which includes core engine calculations, knock detection, adaptation, subsystem (TCS, CC, CAN) management.
2. Calculate_Phased_Fuel_Pulse_Widths - Responsible for fuel injection control.
3. Calculate_And_Limit_Engine_Torque - Responsible for load/torque control, and creation of load/airmass target.
4. Calculate_Final_Ignition_Timing - Responsible for ignition timing control.
5. Set_Variable_Valve_Timing - Responsible for control of VVT on both intake and exhaust valves.

Many more functions are labelled in the gzf, but there are too many to document here. These functions and their associated memory regions are a good place to start looking to understand this ECU. 
