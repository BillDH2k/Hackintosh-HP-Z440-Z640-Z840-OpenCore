# Hackintosh-HP-Z440-Z640-Z840-OpenCore

OpenCore loader for HP workstations Z440/Z640/Z840. Support macOS Big Sur and Monterey.

**Supported Hardware**

- HP Z440/Z640/Z840 (BIOS V2.59, latest)
- CPUs: E5-1600/2600 V3/V4 Xeon CPUs (Hanswell/Broadwell)
- macOS compatible video card
- Required BIOS Settings: Enable UEFI boot, set SATA/sSATA to AHCI mode.

**Installation:**

- Generate new serials unique for your system
- SYMBIOS iMacPro1,1 or MacPro7,1 supported
- Choose correct CPU Emulation. Modify config.plist->Root->Kernel->Emulate->Cpuid1Data
	- For V3 Xeon's: C3060300 00000000 00000000 00000000 (<- default setting)
	- For V4 Xeon's: D4060300 00000000 00000000 00000000

#

**What Works:**

- Everything, except Sleep/Wake (This is a workstation setup. Disable Sleep from macOS System Preference)


**EFI Folder**

- OpenCore 0.8.5
- Supported SYMBIOS: iMacPro1,1 or MacPro7,1

- ACPI folder:
	- SSDT-EC.aml - Fix Embedded Controller, via OC Guide
	- SSDT-HPET.aml - Fix HPET/IRQ conflict. Created with SDDTTimes, via OC Guide
	- SSDT-PLUG.aml - Enable CPU power management, via OC Guide
	- SDT-UNC.aml - Disable unused Uncore Bridges, via OC Guide
	- SSDT-RTC0-RANGE.aml - Fix RTC range, via OC Guide
	- SSDT-USBX.aml - Fix USB BUS Power properties, via OC Guide.
	
- Kexts folder:
	- Lilu.kext
	- WhateverGreen.kext
	- AppleMCEReporterDisabler.kext
	- VirtualSMC.kext
	- AppleALC.kext - On-board Audio (Layout ID 11)
	- IntelMausi.kext - LAN port #1 driver (Intel i218LM)
	- i210LanInject.kext - LAN port #2 injector (Intel i210AT, Z840 only) 
	- RTCMemoryFixup.kext - For fix RTC memory
	- XHCI-unsupported.kext - C612 USB driver support
	- USBMap-Zx40.kext - Custom USB2/3 port maps
	- NVMeFix.kext - NvMe SSD on PCI-E adapter
	- AstekFusion2Family.kext - SAS controller (Z840 only)
	- AstekFusion2Adapter.kext - SAS controller (Z840 only)

# Others



