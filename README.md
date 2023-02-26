elf2dfuse
=========

  This tool targeted to  developers to generate a image file for DFUse (DFU ver 1.1a) primary firmware bootloaders directly from an ELF object file.

Generated DfuSe image file can contain data collected from one or multiple ELF files (e.g. secondary bootloader, OTP options and application itself).


## Limitations

DFU (and DFUse) images must encode the VID:PID of the target being programmed.  The source code has #defines for the VID:PID to be 0x0483:0xdf11 (as this was applicable to the target used for testing), but it is unclear to me how many different variants STMicro may be using.	

### Break the wall

 No VID:PID limitations when using `dfu-suffix` utility from http://dfu-util.sourceforge.net or one of forks on GitHub e.g. https://github.com/azorg/dfu-util.git
 
 DFU file suffix containing VID:PID need to be changed to adopt generated DFU file for DfuSe bootloader other then STM32. 


``` 
 	 MPU 		 VID:PI
```
```
 	STM32		0483:DF11
 	APM32		314B:0106
	GD32V		28E9:0189
```
## Sample Usage

For STM32 bootloader enough
```
elf2dfuse app.elf [bl.elf [opt.elf [...]] myapp.dfu
```

Other DFUse bootloader need additional steps
```
dfu-suffix --delete myapp.dfu

dfu-suffix --add myapp.dfu -S 11A -v <VID> -p <PID> -d FFFF

```

## Debug tips
File `elf2dfuse.cbp` is project for Code::Blocks IDE to debug 64bit executable linked with static libraries.

Used compiler is `gcc version 11.2.0 (Rev10, Built by MSYS2 project)`





