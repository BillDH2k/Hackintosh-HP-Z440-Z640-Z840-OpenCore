# Hackintosh-HP-Z440-Z640-Z840-OpenCore

OpenCore 0.9.3 loader. Support macOS Big Sur and Monterey. Ventura also works, but for Z840 the 2nd LAN port (I210-AT) must be disabled for now (until compatible driver issue is resolved).

**Supported Hardware:**

- HP Z440/Z640/Z840 (BIOS V2.59, latest)
- CPUs: E5-1600/2600 V3/V4 Xeon CPUs (Hanswell/Broadwell)
- macOS compatible video card
- Required BIOS Settings: Enable UEFI boot, set SATA/sSATA to AHCI mode.

**Installation:**

- Generate new serials unique for your system
- SYMBIOS iMacPro1,1 (MacPro7,1 also supported)
- Choose correct CPU Emulation. Modify config.plist->Root->Kernel->Emulate->Cpuid1Data
	- For V3 Xeon's: C3060300 00000000 00000000 00000000 (<- default setting)
	- For V4 Xeon's: D4060300 00000000 00000000 00000000

#

**What Works:**

- Everything, except Sleep/Wake for Z840 (no issue with Z440/Z640).

#

**EFI Folder**

- OpenCore 0.9.2
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
	- IntelMausi.kext - LAN port driver (Intel i218LM, all models)
	- i210LanInject.kext - LAN port #2 injector (Intel i210AT, Z840 only) 
	- RTCMemoryFixup.kext - Fix RTC memory
	- XHCI-unsupported.kext - C612 USB driver support
	- USBMap-Zx40.kext - Custom USB port maps
	- NVMeFix.kext - NvMe SSD on PCI-E adapter
	- AstekFusion2Family.kext - SAS controller (Z840 only)
	- AstekFusion2Adapter.kext - SAS controller (Z840 only)

**Others:**

- Custom USB port mapping: All external USB ports are properly mapped and enabled, except one USB2 personality for one of the USB3 connectors (1/4) on the back panel. This is due to the 15 ports limitaiton, so one must be freed in order to enable the internal USB2 conenctor (1 of 2). Enable the internal USB2 connector would be a more useful setting, e.g. when it is required for Wifi addon card.
- RTC exclude range: currently 80-E1. It works on my setup, but could be narrowed down further, based on your hardware.



