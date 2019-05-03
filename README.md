# LinuxMint-t490s
Linux Mint 19 on Lenovo Thinkpad t490s. 
## Background:
This is the `i5/16G/512G/FHD` German Lenovo Campus model for 1995Eur (open-box discount).
In autumn 2018 I've bought a `i7/16G/512G/FHD` X1C6 Campus Model for 1550Eur but I had it returned due to lack of Linux compatibility. Although it is a very new release it seems that the t490s better suited for Linux.

## Build quality compared to X1C6
* the palm top and overall case seems less prone to fingerprints
* very similar in terms of build quality / layout
* worse keyboard than X1C6 but on first impression still good; all keys work okay
* not so smooth clickpad surface, but nicely large area
* display seems similar in brightness/contrast. Expected more nits but I cannot measure it!

## LM 19 compatibility

* [X] Wifi: I've upgraded to kernel 4.18 since I noticed some Wifi reconnects. So far no problems with wifi anymore.
* [X] Touchpad+buttons+knob 
* [X] SSD: > 2G/s reading speed, ~580M/s writing speed. Write speed seems too slow to me.
* [X] Sound
* [X] Suspend: S3 mode is supported
* [X] WebCam throws a [kernel stack trace](issues/camera-stacktrace.md) but shows a picture anyways

## First observations

* idle power consumption - vanilla: 7-8W - with tlp: 5-6W . I am aiming for 10hrs of light usage...let's see!
* upower daemon once went crazy and bogged all CPU+RAM. Cause unknown; had to kill it
* idle CPU temps: 32-34 degrees celsius / after booting: 37-40 degrees celsius
* WLAN transmission speed is 3.5Mb/s on battery / >5Mb/s on AC
```bash

```
## Improvements

* BIOS: Disabled NFC, fingerprint/SC/MC reader, enabled Thunderbolt assist mode -> ~3.5W idle power consumption
* installed `xorg synaptics` driver. I prefer its default settings for the clickpad


## System Info
```
inxi -F
System:    Host: theon Kernel: 4.18.0-18-generic x86_64 bits: 64 Desktop: MATE 1.20.1
           Distro: Linux Mint 19 Tara
Machine:   Device: laptop System: LENOVO product: 20NYS02A00 v: ThinkPad T490s serial: N/A
           Mobo: LENOVO model: 20NYS02A00 serial: N/A UEFI: LENOVO v: N2JET29W (1.07 ) date: 02/19/2019
Battery    BAT0: charge: 51.2 Wh 88.1% condition: 58.1/57.0 Wh (102%)
CPU:       Quad core Intel Core i5-8265U (-MT-MCP-) cache: 6144 KB
           clock speeds: max: 3900 MHz 1: 999 MHz 2: 2543 MHz 3: 2493 MHz 4: 2549 MHz 5: 2321 MHz 6: 1942 MHz
           7: 2485 MHz 8: 2458 MHz
Graphics:  Card: Intel Device 3ea0
           Display Server: x11 (X.Org 1.19.6 ) drivers: modesetting (unloaded: fbdev,vesa)
           Resolution: 1920x1080@60.03hz
           OpenGL: renderer: Mesa DRI Intel HD Graphics (Whiskey Lake 3x8 GT2) version: 4.5 Mesa 18.2.8
Audio:     Card Intel Device 9dc8 driver: snd_hda_intel Sound: ALSA v: k4.18.0-18-generic
Network:   Card-1: Intel Device 9df0 driver: iwlwifi
           IF: wlp0s20f3 state: up speed: N/A duplex: N/A mac: 98:2c:bc:23:fe:47
           Card-2: Intel Ethernet Connection (6) I219-V driver: e1000e
           IF: enp0s31f6 state: down mac: e8:6a:64:b7:66:b0
Drives:    HDD Total Size: 512.1GB (2.0% used)
           ID-1: /dev/nvme0n1 model: INTEL_SSDPEKKF512G8L size: 512.1GB
Partition: ID-1: / size: 468G used: 9.5G (3%) fs: ext4 dev: /dev/nvme0n1p2
RAID:      No RAID devices: /proc/mdstat, md_mod kernel module present
Sensors:   System Temperatures: cpu: 40.0C mobo: N/A
           Fan Speeds (in rpm): cpu: 0
Info:      Processes: 231 Uptime: 47 min Memory: 1032.6/15849.5MB Client: Shell (bash) inxi: 2.3.56 
```

## DMESG output
```
dmesg 
[    0.000000] Linux version 4.18.0-18-generic (buildd@lcy01-amd64-006) (gcc version 7.3.0 (Ubuntu 7.3.0-16ubuntu3)) #19~18.04.1-Ubuntu SMP Fri Apr 5 10:22:13 UTC 2019 (Ubuntu 4.18.0-18.19~18.04.1-generic 4.18.20)
[    0.000000] Command line: BOOT_IMAGE=/boot/vmlinuz-4.18.0-18-generic root=UUID=e67693dd-0b08-4984-9e5e-b84cbe9e8a9f ro quiet splash vt.handoff=1
[    0.000000] KERNEL supported cpus:
[    0.000000]   Intel GenuineIntel
[    0.000000]   AMD AuthenticAMD
[    0.000000]   Centaur CentaurHauls
[    0.000000] x86/fpu: Supporting XSAVE feature 0x001: 'x87 floating point registers'
[    0.000000] x86/fpu: Supporting XSAVE feature 0x002: 'SSE registers'
[    0.000000] x86/fpu: Supporting XSAVE feature 0x004: 'AVX registers'
[    0.000000] x86/fpu: Supporting XSAVE feature 0x008: 'MPX bounds registers'
[    0.000000] x86/fpu: Supporting XSAVE feature 0x010: 'MPX CSR'
[    0.000000] x86/fpu: xstate_offset[2]:  576, xstate_sizes[2]:  256
[    0.000000] x86/fpu: xstate_offset[3]:  832, xstate_sizes[3]:   64
[    0.000000] x86/fpu: xstate_offset[4]:  896, xstate_sizes[4]:   64
[    0.000000] x86/fpu: Enabled xstate features 0x1f, context size is 960 bytes, using 'compacted' format.
[    0.000000] BIOS-provided physical RAM map:
[    0.000000] BIOS-e820: [mem 0x0000000000000000-0x0000000000000fff] reserved
[    0.000000] BIOS-e820: [mem 0x0000000000001000-0x0000000000001fff] usable
[    0.000000] BIOS-e820: [mem 0x0000000000002000-0x000000000000bfff] reserved
[    0.000000] BIOS-e820: [mem 0x000000000000c000-0x000000000005efff] usable
[    0.000000] BIOS-e820: [mem 0x000000000005f000-0x0000000000086fff] reserved
[    0.000000] BIOS-e820: [mem 0x0000000000087000-0x0000000000088fff] usable
[    0.000000] BIOS-e820: [mem 0x0000000000089000-0x000000000008afff] reserved
[    0.000000] BIOS-e820: [mem 0x000000000008b000-0x000000000008bfff] type 20
[    0.000000] BIOS-e820: [mem 0x000000000008c000-0x00000000000fffff] reserved
[    0.000000] BIOS-e820: [mem 0x0000000000100000-0x000000006f998fff] usable
[    0.000000] BIOS-e820: [mem 0x000000006f999000-0x000000006fa5dfff] type 20
[    0.000000] BIOS-e820: [mem 0x000000006fa5e000-0x000000007416dfff] reserved
[    0.000000] BIOS-e820: [mem 0x000000007416e000-0x00000000743a9fff] ACPI NVS
[    0.000000] BIOS-e820: [mem 0x00000000743aa000-0x000000007440efff] ACPI data
[    0.000000] BIOS-e820: [mem 0x000000007440f000-0x000000007440ffff] usable
[    0.000000] BIOS-e820: [mem 0x0000000074410000-0x00000000797fffff] reserved
[    0.000000] BIOS-e820: [mem 0x00000000fe010000-0x00000000fe010fff] reserved
[    0.000000] BIOS-e820: [mem 0x0000000100000000-0x00000004847fffff] usable
[    0.000000] NX (Execute Disable) protection: active
[    0.000000] efi: EFI v2.60 by Lenovo
[    0.000000] efi:  SMBIOS=0x72594000  SMBIOS 3.0=0x72587000  ACPI=0x7440e000  ACPI 2.0=0x7440e014  MPS=0x74142000  MEMATTR=0x6d26c118  ESRT=0x7053e000 
[    0.000000] secureboot: Secure boot could not be determined (mode 0)
[    0.000000] SMBIOS 3.1.1 present.
[    0.000000] DMI: LENOVO 20NYS02A00/20NYS02A00, BIOS N2JET29W (1.07 ) 02/19/2019
[    0.000000] e820: update [mem 0x00000000-0x00000fff] usable ==> reserved
[    0.000000] e820: remove [mem 0x000a0000-0x000fffff] usable
[    0.000000] last_pfn = 0x484800 max_arch_pfn = 0x400000000
[    0.000000] MTRR default type: write-back
[    0.000000] MTRR fixed ranges enabled:
[    0.000000]   00000-9FFFF write-back
[    0.000000]   A0000-BFFFF uncachable
[    0.000000]   C0000-F3FFF write-protect
[    0.000000]   F4000-F7FFF uncachable
[    0.000000]   F8000-FFFFF write-protect
[    0.000000] MTRR variable ranges enabled:
[    0.000000]   0 base 0080000000 mask 7F80000000 uncachable
[    0.000000]   1 base 0078000000 mask 7FF8000000 uncachable
[    0.000000]   2 base 0077000000 mask 7FFF000000 uncachable
[    0.000000]   3 base 2000000000 mask 6000000000 uncachable
[    0.000000]   4 base 1000000000 mask 7000000000 uncachable
[    0.000000]   5 base 0800000000 mask 7800000000 uncachable
[    0.000000]   6 base 4000000000 mask 4000000000 uncachable
[    0.000000]   7 disabled
[    0.000000]   8 disabled
[    0.000000]   9 disabled
[    0.000000] x86/PAT: Configuration [0-7]: WB  WC  UC- UC  WB  WP  UC- WT  
[    0.000000] last_pfn = 0x74410 max_arch_pfn = 0x400000000
[    0.000000] esrt: Reserving ESRT space from 0x000000007053e000 to 0x000000007053e0b0.
[    0.000000] Scanning 2 areas for low memory corruption
[    0.000000] Base memory trampoline at [(____ptrval____)] 55000 size 24576
[    0.000000] Using GB pages for direct mapping
[    0.000000] BRK [0x178963000, 0x178963fff] PGTABLE
[    0.000000] BRK [0x178964000, 0x178964fff] PGTABLE
[    0.000000] BRK [0x178965000, 0x178965fff] PGTABLE
[    0.000000] BRK [0x178966000, 0x178966fff] PGTABLE
[    0.000000] BRK [0x178967000, 0x178967fff] PGTABLE
[    0.000000] BRK [0x178968000, 0x178968fff] PGTABLE
[    0.000000] BRK [0x178969000, 0x178969fff] PGTABLE
[    0.000000] BRK [0x17896a000, 0x17896afff] PGTABLE
[    0.000000] RAMDISK: [mem 0x307af000-0x343cefff]
[    0.000000] ACPI: Early table checksum verification disabled
[    0.000000] ACPI: RSDP 0x000000007440E014 000024 (v02 LENOVO)
[    0.000000] ACPI: XSDT 0x000000007440C188 0000FC (v01 LENOVO TP-N2J   00001070 PTEC 00000002)
[    0.000000] ACPI: FACP 0x0000000071F59000 000114 (v06 LENOVO TP-N2J   00001070 PTEC 00000002)
[    0.000000] ACPI: DSDT 0x0000000071F31000 02396A (v02 LENOVO CFL      20170001 INTL 20160422)
[    0.000000] ACPI: FACS 0x0000000074204000 000040
[    0.000000] ACPI: SSDT 0x0000000072499000 001B1C (v02 LENOVO CpuSsdt  00003000 INTL 20160527)
[    0.000000] ACPI: SSDT 0x0000000072498000 00056D (v02 LENOVO CtdpB    00001000 INTL 20160527)
[    0.000000] ACPI: SSDT 0x000000007245F000 003605 (v02 LENOVO DptfTabl 00001000 INTL 20160527)
[    0.000000] ACPI: SSDT 0x0000000071F5E000 00313D (v02 LENOVO SaSsdt   00003000 INTL 20160527)
[    0.000000] ACPI: SSDT 0x0000000071F5D000 000612 (v02 LENOVO Tpm2Tabl 00001000 INTL 20160527)
[    0.000000] ACPI: TPM2 0x0000000071F5C000 000034 (v04 LENOVO TP-N2J   00001070 PTEC 00000002)
[    0.000000] ACPI: UEFI 0x0000000074223000 000042 (v01 LENOVO TP-N2J   00001070 PTEC 00000002)
[    0.000000] ACPI: SSDT 0x0000000071F5A000 000530 (v02 LENOVO PerfTune 00001000 INTL 20160527)
[    0.000000] ACPI: HPET 0x0000000071F58000 000038 (v01 LENOVO TP-N2J   00001070 PTEC 00000002)
[    0.000000] ACPI: APIC 0x0000000071F57000 00012C (v03 LENOVO TP-N2J   00001070 PTEC 00000002)
[    0.000000] ACPI: MCFG 0x0000000071F56000 00003C (v01 LENOVO TP-N2J   00001070 PTEC 00000002)
[    0.000000] ACPI: ECDT 0x0000000071F55000 000053 (v01 LENOVO TP-N2J   00001070 PTEC 00000002)
[    0.000000] ACPI: SSDT 0x0000000071F2F000 0015EF (v02 LENOVO WHL_Tbt_ 00001000 INTL 20160527)
[    0.000000] ACPI: SSDT 0x0000000071F2C000 002242 (v02 LENOVO ProjSsdt 00000010 INTL 20160527)
[    0.000000] ACPI: BOOT 0x0000000071F2B000 000028 (v01 LENOVO TP-N2J   00001070 PTEC 00000002)
[    0.000000] ACPI: SSDT 0x0000000071F2A000 000CE3 (v02 LENOVO UsbCTabl 00001000 INTL 20160527)
[    0.000000] ACPI: LPIT 0x0000000071F29000 000094 (v01 LENOVO TP-N2J   00001070 PTEC 00000002)
[    0.000000] ACPI: WSMT 0x0000000071F28000 000028 (v01 LENOVO TP-N2J   00001070 PTEC 00000002)
[    0.000000] ACPI: SSDT 0x0000000071F26000 001667 (v02 LENOVO TbtTypeC 00000000 INTL 20160527)
[    0.000000] ACPI: DBGP 0x0000000071F25000 000034 (v01 LENOVO TP-N2J   00001070 PTEC 00000002)
[    0.000000] ACPI: DBG2 0x0000000071F24000 000054 (v00 LENOVO TP-N2J   00001070 PTEC 00000002)
[    0.000000] ACPI: POAT 0x0000000071F23000 000055 (v03 LENOVO TP-N2J   00001070 PTEC 00000002)
[    0.000000] ACPI: BATB 0x0000000071D46000 00004A (v02 LENOVO TP-N2J   00001070 PTEC 00000002)
[    0.000000] ACPI: NHLT 0x000000007053F000 00002D (v00 LENOVO TP-N2J   00001070 PTEC 00000002)
[    0.000000] ACPI: FPDT 0x000000007053D000 000044 (v01 LENOVO TP-N2J   00001070 PTEC 00000002)
[    0.000000] ACPI: UEFI 0x00000000741B8000 00012A (v01 LENOVO TP-N2J   00001070 PTEC 00000002)
[    0.000000] ACPI: Local APIC address 0xfee00000
[    0.000000] No NUMA configuration found
[    0.000000] Faking a node at [mem 0x0000000000000000-0x00000004847fffff]
[    0.000000] NODE_DATA(0) allocated [mem 0x4847d5000-0x4847fffff]
[    0.000000] Zone ranges:
[    0.000000]   DMA      [mem 0x0000000000001000-0x0000000000ffffff]
[    0.000000]   DMA32    [mem 0x0000000001000000-0x00000000ffffffff]
[    0.000000]   Normal   [mem 0x0000000100000000-0x00000004847fffff]
[    0.000000]   Device   empty
[    0.000000] Movable zone start for each node
[    0.000000] Early memory node ranges
[    0.000000]   node   0: [mem 0x0000000000001000-0x0000000000001fff]
[    0.000000]   node   0: [mem 0x000000000000c000-0x000000000005efff]
[    0.000000]   node   0: [mem 0x0000000000087000-0x0000000000088fff]
[    0.000000]   node   0: [mem 0x0000000000100000-0x000000006f998fff]
[    0.000000]   node   0: [mem 0x000000007440f000-0x000000007440ffff]
[    0.000000]   node   0: [mem 0x0000000100000000-0x00000004847fffff]
[    0.000000] Reserved but unavailable: 34576 pages
[    0.000000] Initmem setup node 0 [mem 0x0000000000001000-0x00000004847fffff]
[    0.000000] On node 0 totalpages: 4145392
[    0.000000]   DMA zone: 64 pages used for memmap
[    0.000000]   DMA zone: 12 pages reserved
[    0.000000]   DMA zone: 3926 pages, LIFO batch:0
[    0.000000]   DMA32 zone: 7079 pages used for memmap
[    0.000000]   DMA32 zone: 453018 pages, LIFO batch:31
[    0.000000]   Normal zone: 57632 pages used for memmap
[    0.000000]   Normal zone: 3688448 pages, LIFO batch:31
[    0.000000] Reserving Intel graphics memory at [mem 0x77800000-0x797fffff]
[    0.000000] ACPI: PM-Timer IO Port: 0x1808
[    0.000000] ACPI: Local APIC address 0xfee00000
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x01] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x02] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x03] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x04] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x05] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x06] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x07] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x08] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x09] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x0a] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x0b] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x0c] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x0d] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x0e] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x0f] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x10] high edge lint[0x1])
[    0.000000] IOAPIC[0]: apic_id 2, version 32, address 0xfec00000, GSI 0-119
[    0.000000] ACPI: INT_SRC_OVR (bus 0 bus_irq 0 global_irq 2 dfl dfl)
[    0.000000] ACPI: INT_SRC_OVR (bus 0 bus_irq 9 global_irq 9 high level)
[    0.000000] ACPI: IRQ0 used by override.
[    0.000000] ACPI: IRQ9 used by override.
[    0.000000] Using ACPI (MADT) for SMP configuration information
[    0.000000] ACPI: HPET id: 0x8086a201 base: 0xfed00000
[    0.000000] smpboot: Allowing 8 CPUs, 0 hotplug CPUs
[    0.000000] PM: Registered nosave memory: [mem 0x00000000-0x00000fff]
[    0.000000] PM: Registered nosave memory: [mem 0x00002000-0x0000bfff]
[    0.000000] PM: Registered nosave memory: [mem 0x0005f000-0x00086fff]
[    0.000000] PM: Registered nosave memory: [mem 0x00089000-0x0008afff]
[    0.000000] PM: Registered nosave memory: [mem 0x0008b000-0x0008bfff]
[    0.000000] PM: Registered nosave memory: [mem 0x0008c000-0x000fffff]
[    0.000000] PM: Registered nosave memory: [mem 0x6f999000-0x6fa5dfff]
[    0.000000] PM: Registered nosave memory: [mem 0x6fa5e000-0x7416dfff]
[    0.000000] PM: Registered nosave memory: [mem 0x7416e000-0x743a9fff]
[    0.000000] PM: Registered nosave memory: [mem 0x743aa000-0x7440efff]
[    0.000000] PM: Registered nosave memory: [mem 0x74410000-0x797fffff]
[    0.000000] PM: Registered nosave memory: [mem 0x79800000-0xfe00ffff]
[    0.000000] PM: Registered nosave memory: [mem 0xfe010000-0xfe010fff]
[    0.000000] PM: Registered nosave memory: [mem 0xfe011000-0xffffffff]
[    0.000000] [mem 0x79800000-0xfe00ffff] available for PCI devices
[    0.000000] Booting paravirtualized kernel on bare hardware
[    0.000000] clocksource: refined-jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 7645519600211568 ns
[    0.000000] random: get_random_bytes called from start_kernel+0x99/0x55a with crng_init=0
[    0.000000] setup_percpu: NR_CPUS:8192 nr_cpumask_bits:8 nr_cpu_ids:8 nr_node_ids:1
[    0.000000] percpu: Embedded 46 pages/cpu @(____ptrval____) s151552 r8192 d28672 u262144
[    0.000000] pcpu-alloc: s151552 r8192 d28672 u262144 alloc=1*2097152
[    0.000000] pcpu-alloc: [0] 0 1 2 3 4 5 6 7 
[    0.000000] Built 1 zonelists, mobility grouping on.  Total pages: 4080605
[    0.000000] Policy zone: Normal
[    0.000000] Kernel command line: BOOT_IMAGE=/boot/vmlinuz-4.18.0-18-generic root=UUID=e67693dd-0b08-4984-9e5e-b84cbe9e8a9f ro quiet splash vt.handoff=1
[    0.000000] Calgary: detecting Calgary via BIOS EBDA area
[    0.000000] Calgary: Unable to locate Rio Grande table in EBDA - bailing!
[    0.000000] Memory: 16123764K/16581568K available (12300K kernel code, 2634K rwdata, 4384K rodata, 2464K init, 2340K bss, 457804K reserved, 0K cma-reserved)
[    0.000000] SLUB: HWalign=64, Order=0-3, MinObjects=0, CPUs=8, Nodes=1
[    0.000000] ftrace: allocating 40843 entries in 160 pages
[    0.000000] Hierarchical RCU implementation.
[    0.000000] 	RCU restricting CPUs from NR_CPUS=8192 to nr_cpu_ids=8.
[    0.000000] 	Tasks RCU enabled.
[    0.000000] RCU: Adjusting geometry for rcu_fanout_leaf=16, nr_cpu_ids=8
[    0.000000] NR_IRQS: 524544, nr_irqs: 2048, preallocated irqs: 16
[    0.000000] vt handoff: transparent VT on vt#1
[    0.000000] Console: colour dummy device 80x25
[    0.000000] console [tty0] enabled
[    0.000000] ACPI: Core revision 20180531
[    0.000000] clocksource: hpet: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 79635855245 ns
[    0.000000] hpet clockevent registered
[    0.004000] APIC: Switch to symmetric I/O mode setup
[    0.004000] x2apic: IRQ remapping doesn't support X2APIC mode
[    0.012000] ..TIMER: vector=0x30 apic1=0 pin1=2 apic2=-1 pin2=-1
[    0.032000] tsc: Detected 1800.000 MHz processor
[    0.032000] clocksource: tsc-early: mask: 0xffffffffffffffff max_cycles: 0x19f2297dd97, max_idle_ns: 440795236593 ns
[    0.032000] Calibrating delay loop (skipped), value calculated using timer frequency.. 3600.00 BogoMIPS (lpj=7200000)
[    0.032000] pid_max: default: 32768 minimum: 301
[    0.032000] efi: memattr: Entry attributes invalid: RO and XP bits both cleared
[    0.032000] efi: memattr: ! 0x00000008b000-0x00000008bfff [Runtime Code       |RUN|  |  |  |  |  |  |   |  |  |  |  ]
[    0.032000] Security Framework initialized
[    0.032000] Yama: becoming mindful.
[    0.032000] AppArmor: AppArmor initialized
[    0.032000] Dentry cache hash table entries: 2097152 (order: 12, 16777216 bytes)
[    0.036514] Inode-cache hash table entries: 1048576 (order: 11, 8388608 bytes)
[    0.036562] Mount-cache hash table entries: 32768 (order: 6, 262144 bytes)
[    0.036601] Mountpoint-cache hash table entries: 32768 (order: 6, 262144 bytes)
[    0.036859] ENERGY_PERF_BIAS: Set to 'normal', was 'performance'
[    0.036859] ENERGY_PERF_BIAS: View and update with x86_energy_perf_policy(8)
[    0.036867] mce: CPU supports 10 MCE banks
[    0.036880] CPU0: Thermal monitoring enabled (TM1)
[    0.036907] process: using mwait in idle threads
[    0.036910] Last level iTLB entries: 4KB 64, 2MB 8, 4MB 8
[    0.036911] Last level dTLB entries: 4KB 64, 2MB 0, 4MB 0, 1GB 4
[    0.036913] Spectre V2 : Mitigation: Full generic retpoline
[    0.036914] Spectre V2 : Spectre v2 / SpectreRSB mitigation: Filling RSB on context switch
[    0.036914] Spectre V2 : Enabling Restricted Speculation for firmware calls
[    0.036922] Spectre V2 : mitigation: Enabling conditional Indirect Branch Prediction Barrier
[    0.036922] Spectre V2 : User space: Mitigation: STIBP via seccomp and prctl
[    0.036924] Speculative Store Bypass: Mitigation: Speculative Store Bypass disabled via prctl and seccomp
[    0.044981] Freeing SMP alternatives memory: 36K
[    0.049133] TSC deadline timer enabled
[    0.049144] smpboot: CPU0: Intel(R) Core(TM) i5-8265U CPU @ 1.60GHz (family: 0x6, model: 0x8e, stepping: 0xb)
[    0.049247] Performance Events: PEBS fmt3+, Skylake events, 32-deep LBR, full-width counters, Intel PMU driver.
[    0.049289] ... version:                4
[    0.049290] ... bit width:              48
[    0.049291] ... generic registers:      4
[    0.049292] ... value mask:             0000ffffffffffff
[    0.049293] ... max period:             00007fffffffffff
[    0.049293] ... fixed-purpose events:   3
[    0.049294] ... event mask:             000000070000000f
[    0.049343] Hierarchical SRCU implementation.
[    0.050771] NMI watchdog: Enabled. Permanently consumes one hw-PMU counter.
[    0.050795] smp: Bringing up secondary CPUs ...
[    0.050882] x86: Booting SMP configuration:
[    0.050884] .... node  #0, CPUs:      #1 #2 #3 #4 #5 #6 #7
[    0.056993] smp: Brought up 1 node, 8 CPUs
[    0.056993] smpboot: Max logical packages: 1
[    0.056993] smpboot: Total of 8 processors activated (28800.00 BogoMIPS)
[    0.060548] devtmpfs: initialized
[    0.060548] x86/mm: Memory block size: 128MB
[    0.061874] PM: Registering ACPI NVS region [mem 0x7416e000-0x743a9fff] (2342912 bytes)
[    0.061874] clocksource: jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 7645041785100000 ns
[    0.061874] futex hash table entries: 2048 (order: 5, 131072 bytes)
[    0.061874] pinctrl core: initialized pinctrl subsystem
[    0.061874] RTC time:  9:16:44, date: 05/03/19
[    0.064424] NET: Registered protocol family 16
[    0.064567] audit: initializing netlink subsys (disabled)
[    0.064575] audit: type=2000 audit(1556875004.064:1): state=initialized audit_enabled=0 res=1
[    0.064575] cpuidle: using governor ladder
[    0.064575] cpuidle: using governor menu
[    0.064575] Simple Boot Flag at 0x47 set to 0x1
[    0.064575] ACPI FADT declares the system doesn't support PCIe ASPM, so disable it
[    0.064575] ACPI: bus type PCI registered
[    0.064575] acpiphp: ACPI Hot Plug PCI Controller Driver version: 0.5
[    0.064575] PCI: MMCONFIG for domain 0000 [bus 00-ff] at [mem 0xe0000000-0xefffffff] (base 0xe0000000)
[    0.064575] PCI: not using MMCONFIG
[    0.064575] PCI: Using configuration type 1 for base access
[    0.066075] HugeTLB registered 1.00 GiB page size, pre-allocated 0 pages
[    0.066075] HugeTLB registered 2.00 MiB page size, pre-allocated 0 pages
[    0.068008] ACPI: Added _OSI(Module Device)
[    0.068008] ACPI: Added _OSI(Processor Device)
[    0.068008] ACPI: Added _OSI(3.0 _SCP Extensions)
[    0.068008] ACPI: Added _OSI(Processor Aggregator Device)
[    0.068008] ACPI: Added _OSI(Linux-Dell-Video)
[    0.068008] ACPI: Added _OSI(Linux-Lenovo-NV-HDMI-Audio)
[    0.068008] ACPI: EC: EC started
[    0.068008] ACPI: EC: interrupt blocked
[    0.068008] ACPI: \: Used as first EC
[    0.068008] ACPI: \: GPE=0x16, EC_CMD/EC_SC=0x66, EC_DATA=0x62
[    0.068008] ACPI: \: Used as boot ECDT EC to handle transactions
[    0.160061] ACPI: 11 ACPI AML tables successfully acquired and loaded
[    0.171072] ACPI: [Firmware Bug]: BIOS _OSI(Linux) query ignored
[    0.252391] ACPI: Dynamic OEM Table Load:
[    0.252411] ACPI: SSDT 0xFFFF9AC371557300 0000F4 (v02 PmRef  Cpu0Psd  00003000 INTL 20160527)
[    0.252696] ACPI: \_SB_.PR00: _OSC native thermal LVT Acked
[    0.253631] ACPI: Dynamic OEM Table Load:
[    0.253642] ACPI: SSDT 0xFFFF9AC371534800 000400 (v02 PmRef  Cpu0Cst  00003001 INTL 20160527)
[    0.254544] ACPI: Dynamic OEM Table Load:
[    0.254554] ACPI: SSDT 0xFFFF9AC371882000 000596 (v02 PmRef  Cpu0Ist  00003000 INTL 20160527)
[    0.256845] ACPI: Dynamic OEM Table Load:
[    0.256853] ACPI: SSDT 0xFFFF9AC37152FC00 00011B (v02 PmRef  Cpu0Hwp  00003000 INTL 20160527)
[    0.257568] ACPI: Dynamic OEM Table Load:
[    0.257579] ACPI: SSDT 0xFFFF9AC371883000 000724 (v02 PmRef  HwpLvt   00003000 INTL 20160527)
[    0.258132] ACPI: Dynamic OEM Table Load:
[    0.258132] ACPI: SSDT 0xFFFF9AC371821000 0005FC (v02 PmRef  ApIst    00003000 INTL 20160527)
[    0.258132] ACPI: Dynamic OEM Table Load:
[    0.258132] ACPI: SSDT 0xFFFF9AC371536400 000317 (v02 PmRef  ApHwp    00003000 INTL 20160527)
[    0.260526] ACPI: Dynamic OEM Table Load:
[    0.260538] ACPI: SSDT 0xFFFF9AC371454000 000AB0 (v02 PmRef  ApPsd    00003000 INTL 20160527)
[    0.262199] ACPI: Dynamic OEM Table Load:
[    0.262199] ACPI: SSDT 0xFFFF9AC371533000 00030A (v02 PmRef  ApCst    00003000 INTL 20160527)
[    0.268546] ACPI: Interpreter enabled
[    0.268619] ACPI: (supports S0 S3 S4 S5)
[    0.268621] ACPI: Using IOAPIC for interrupt routing
[    0.268681] PCI: MMCONFIG for domain 0000 [bus 00-ff] at [mem 0xe0000000-0xefffffff] (base 0xe0000000)
[    0.270677] PCI: MMCONFIG at [mem 0xe0000000-0xefffffff] reserved in ACPI motherboard resources
[    0.270694] PCI: Using host bridge windows from ACPI; if necessary, use "pci=nocrs" and report a bug
[    0.271540] ACPI: Enabled 7 GPEs in block 00 to 7F
[    0.279226] ACPI: Power Resource [PUBS] (on)
[    0.282219] ACPI: Power Resource [USBC] (on)
[    0.285033] ACPI: Power Resource [PXP] (on)
[    0.297108] ACPI: Power Resource [V0PR] (on)
[    0.297448] ACPI: Power Resource [V1PR] (on)
[    0.297779] ACPI: Power Resource [V2PR] (on)
[    0.304773] ACPI: Power Resource [WRST] (on)
[    0.309665] ACPI: Power Resource [PIN] (off)
[    0.310729] ACPI: PCI Root Bridge [PCI0] (domain 0000 [bus 00-fe])
[    0.310737] acpi PNP0A08:00: _OSC: OS supports [ExtendedConfig ASPM ClockPM Segments MSI]
[    0.312727] acpi PNP0A08:00: _OSC: platform does not support [AER]
[    0.316341] acpi PNP0A08:00: _OSC: OS now controls [PCIeHotplug SHPCHotplug PME PCIeCapability LTR]
[    0.316343] acpi PNP0A08:00: FADT indicates ASPM is unsupported, using BIOS configuration
[    0.320123] PCI host bridge to bus 0000:00
[    0.320126] pci_bus 0000:00: root bus resource [io  0x0000-0x0cf7 window]
[    0.320128] pci_bus 0000:00: root bus resource [io  0x0d00-0xffff window]
[    0.320130] pci_bus 0000:00: root bus resource [mem 0x000a0000-0x000bffff window]
[    0.320132] pci_bus 0000:00: root bus resource [mem 0x79800000-0xdfffffff window]
[    0.320133] pci_bus 0000:00: root bus resource [mem 0xfc800000-0xfe7fffff window]
[    0.320135] pci_bus 0000:00: root bus resource [bus 00-fe]
[    0.320146] pci 0000:00:00.0: [8086:3e34] type 00 class 0x060000
[    0.321520] pci 0000:00:02.0: [8086:3ea0] type 00 class 0x030000
[    0.321536] pci 0000:00:02.0: reg 0x10: [mem 0xcb000000-0xcbffffff 64bit]
[    0.321545] pci 0000:00:02.0: reg 0x18: [mem 0x80000000-0x8fffffff 64bit pref]
[    0.321551] pci 0000:00:02.0: reg 0x20: [io  0x3000-0x303f]
[    0.321572] pci 0000:00:02.0: BAR 2: assigned to efifb
[    0.322950] pci 0000:00:04.0: [8086:1903] type 00 class 0x118000
[    0.322967] pci 0000:00:04.0: reg 0x10: [mem 0xcd730000-0xcd737fff 64bit]
[    0.324400] pci 0000:00:08.0: [8086:1911] type 00 class 0x088000
[    0.324418] pci 0000:00:08.0: reg 0x10: [mem 0xcd742000-0xcd742fff 64bit]
[    0.325815] pci 0000:00:12.0: [8086:9df9] type 00 class 0x118000
[    0.325844] pci 0000:00:12.0: reg 0x10: [mem 0xcd743000-0xcd743fff 64bit]
[    0.327277] pci 0000:00:14.0: [8086:9ded] type 00 class 0x0c0330
[    0.327301] pci 0000:00:14.0: reg 0x10: [mem 0xcd720000-0xcd72ffff 64bit]
[    0.327378] pci 0000:00:14.0: PME# supported from D3hot D3cold
[    0.328810] pci 0000:00:14.2: [8086:9def] type 00 class 0x050000
[    0.328834] pci 0000:00:14.2: reg 0x10: [mem 0xcd740000-0xcd741fff 64bit]
[    0.328847] pci 0000:00:14.2: reg 0x18: [mem 0xcd744000-0xcd744fff 64bit]
[    0.330281] pci 0000:00:14.3: [8086:9df0] type 00 class 0x028000
[    0.330416] pci 0000:00:14.3: reg 0x10: [mem 0xcd738000-0xcd73bfff 64bit]
[    0.330934] pci 0000:00:14.3: PME# supported from D0 D3hot D3cold
[    0.332402] pci 0000:00:15.0: [8086:9de8] type 00 class 0x0c8000
[    0.332461] pci 0000:00:15.0: reg 0x10: [mem 0xcd745000-0xcd745fff 64bit]
[    0.334060] pci 0000:00:16.0: [8086:9de0] type 00 class 0x078000
[    0.334090] pci 0000:00:16.0: reg 0x10: [mem 0xcd746000-0xcd746fff 64bit]
[    0.334179] pci 0000:00:16.0: PME# supported from D3hot
[    0.335657] pci 0000:00:1c.0: [8086:9db8] type 01 class 0x060400
[    0.335757] pci 0000:00:1c.0: PME# supported from D0 D3hot D3cold
[    0.335777] pci 0000:00:1c.0: PTM enabled (root), 4dns granularity
[    0.337259] pci 0000:00:1c.4: [8086:9dbc] type 01 class 0x060400
[    0.337348] pci 0000:00:1c.4: PME# supported from D0 D3hot D3cold
[    0.337365] pci 0000:00:1c.4: PTM enabled (root), 4dns granularity
[    0.338826] pci 0000:00:1d.0: [8086:9db0] type 01 class 0x060400
[    0.338918] pci 0000:00:1d.0: PME# supported from D0 D3hot D3cold
[    0.340387] pci 0000:00:1d.4: [8086:9db4] type 01 class 0x060400
[    0.340479] pci 0000:00:1d.4: PME# supported from D0 D3hot D3cold
[    0.340497] pci 0000:00:1d.4: PTM enabled (root), 4dns granularity
[    0.341977] pci 0000:00:1f.0: [8086:9d84] type 00 class 0x060100
[    0.343616] pci 0000:00:1f.3: [8086:9dc8] type 00 class 0x040380
[    0.343690] pci 0000:00:1f.3: reg 0x10: [mem 0xcd73c000-0xcd73ffff 64bit]
[    0.343774] pci 0000:00:1f.3: reg 0x20: [mem 0xcca00000-0xccafffff 64bit]
[    0.343914] pci 0000:00:1f.3: PME# supported from D3hot D3cold
[    0.345460] pci 0000:00:1f.4: [8086:9da3] type 00 class 0x0c0500
[    0.345488] pci 0000:00:1f.4: reg 0x10: [mem 0xcd747000-0xcd7470ff 64bit]
[    0.345514] pci 0000:00:1f.4: reg 0x20: [io  0xefa0-0xefbf]
[    0.346926] pci 0000:00:1f.5: [8086:9da4] type 00 class 0x0c8000
[    0.346946] pci 0000:00:1f.5: reg 0x10: [mem 0xfe010000-0xfe010fff]
[    0.348347] pci 0000:00:1f.6: [8086:15be] type 00 class 0x020000
[    0.348404] pci 0000:00:1f.6: reg 0x10: [mem 0xcd700000-0xcd71ffff]
[    0.348644] pci 0000:00:1f.6: PME# supported from D0 D3hot D3cold
[    0.350140] pci 0000:01:00.0: [10ec:522a] type 00 class 0xff0000
[    0.350178] pci 0000:01:00.0: reg 0x10: [mem 0xcd600000-0xcd600fff]
[    0.350401] pci 0000:01:00.0: supports D1 D2
[    0.350403] pci 0000:01:00.0: PME# supported from D1 D2 D3hot D3cold
[    0.350760] pci 0000:00:1c.0: PCI bridge to [bus 01]
[    0.350766] pci 0000:00:1c.0:   bridge window [mem 0xcd600000-0xcd6fffff]
[    0.350847] pci 0000:02:00.0: [8086:15c0] type 01 class 0x060400
[    0.350909] pci 0000:02:00.0: enabling Extended Tags
[    0.350994] pci 0000:02:00.0: supports D1 D2
[    0.350996] pci 0000:02:00.0: PME# supported from D0 D1 D2 D3hot D3cold
[    0.351117] pci 0000:00:1c.4: PCI bridge to [bus 02-3a]
[    0.351122] pci 0000:00:1c.4:   bridge window [mem 0xb4000000-0xca0fffff]
[    0.351128] pci 0000:00:1c.4:   bridge window [mem 0x90000000-0xb1ffffff 64bit pref]
[    0.351205] pci 0000:03:00.0: [8086:15c0] type 01 class 0x060400
[    0.351272] pci 0000:03:00.0: enabling Extended Tags
[    0.351360] pci 0000:03:00.0: supports D1 D2
[    0.351362] pci 0000:03:00.0: PME# supported from D0 D1 D2 D3hot D3cold
[    0.351461] pci 0000:03:01.0: [8086:15c0] type 01 class 0x060400
[    0.351528] pci 0000:03:01.0: enabling Extended Tags
[    0.351616] pci 0000:03:01.0: supports D1 D2
[    0.351618] pci 0000:03:01.0: PME# supported from D0 D1 D2 D3hot D3cold
[    0.351717] pci 0000:03:02.0: [8086:15c0] type 01 class 0x060400
[    0.351783] pci 0000:03:02.0: enabling Extended Tags
[    0.351872] pci 0000:03:02.0: supports D1 D2
[    0.351874] pci 0000:03:02.0: PME# supported from D0 D1 D2 D3hot D3cold
[    0.352006] pci 0000:02:00.0: PCI bridge to [bus 03-3a]
[    0.352015] pci 0000:02:00.0:   bridge window [mem 0xb4000000-0xca0fffff]
[    0.352022] pci 0000:02:00.0:   bridge window [mem 0x90000000-0xb1ffffff 64bit pref]
[    0.352090] pci 0000:04:00.0: [8086:15bf] type 00 class 0x088000
[    0.352126] pci 0000:04:00.0: reg 0x10: [mem 0xca000000-0xca03ffff]
[    0.352139] pci 0000:04:00.0: reg 0x14: [mem 0xca040000-0xca040fff]
[    0.352207] pci 0000:04:00.0: enabling Extended Tags
[    0.352314] pci 0000:04:00.0: supports D1 D2
[    0.352316] pci 0000:04:00.0: PME# supported from D0 D1 D2 D3hot D3cold
[    0.352460] pci 0000:03:00.0: PCI bridge to [bus 04]
[    0.352470] pci 0000:03:00.0:   bridge window [mem 0xca000000-0xca0fffff]
[    0.352527] pci 0000:03:01.0: PCI bridge to [bus 05-39]
[    0.352537] pci 0000:03:01.0:   bridge window [mem 0xb4000000-0xc9efffff]
[    0.352545] pci 0000:03:01.0:   bridge window [mem 0x90000000-0xb1ffffff 64bit pref]
[    0.352626] pci 0000:3a:00.0: [8086:15c1] type 00 class 0x0c0330
[    0.352665] pci 0000:3a:00.0: reg 0x10: [mem 0xc9f00000-0xc9f0ffff]
[    0.352751] pci 0000:3a:00.0: enabling Extended Tags
[    0.352860] pci 0000:3a:00.0: supports D1 D2
[    0.352862] pci 0000:3a:00.0: PME# supported from D0 D1 D2 D3hot D3cold
[    0.353027] pci 0000:03:02.0: PCI bridge to [bus 3a]
[    0.353037] pci 0000:03:02.0:   bridge window [mem 0xc9f00000-0xc9ffffff]
[    0.353127] pci 0000:00:1d.0: PCI bridge to [bus 3c]
[    0.353131] pci 0000:00:1d.0:   bridge window [io  0x2000-0x2fff]
[    0.353135] pci 0000:00:1d.0:   bridge window [mem 0xccc00000-0xcd5fffff]
[    0.353141] pci 0000:00:1d.0:   bridge window [mem 0xcc000000-0xcc9fffff 64bit pref]
[    0.353210] pci 0000:3d:00.0: [8086:f1a6] type 00 class 0x010802
[    0.353248] pci 0000:3d:00.0: reg 0x10: [mem 0xccb00000-0xccb03fff 64bit]
[    0.353552] pci 0000:00:1d.4: PCI bridge to [bus 3d]
[    0.353557] pci 0000:00:1d.4:   bridge window [mem 0xccb00000-0xccbfffff]
[    0.358993] ACPI: EC: interrupt unblocked
[    0.359044] ACPI: EC: event unblocked
[    0.359068] ACPI: \_SB_.PCI0.LPCB.EC__: GPE=0x16, EC_CMD/EC_SC=0x66, EC_DATA=0x62
[    0.359070] ACPI: \_SB_.PCI0.LPCB.EC__: Used as boot DSDT EC to handle transactions and events
[    0.360108] SCSI subsystem initialized
[    0.360126] libata version 3.00 loaded.
[    0.360126] pci 0000:00:02.0: vgaarb: setting as boot VGA device
[    0.360126] pci 0000:00:02.0: vgaarb: VGA device added: decodes=io+mem,owns=io+mem,locks=none
[    0.360126] pci 0000:00:02.0: vgaarb: bridge control possible
[    0.360126] vgaarb: loaded
[    0.360126] ACPI: bus type USB registered
[    0.360126] usbcore: registered new interface driver usbfs
[    0.360126] usbcore: registered new interface driver hub
[    0.360126] usbcore: registered new device driver usb
[    0.360126] pps_core: LinuxPPS API ver. 1 registered
[    0.360126] pps_core: Software ver. 5.3.6 - Copyright 2005-2007 Rodolfo Giometti <giometti@linux.it>
[    0.360126] PTP clock support registered
[    0.360136] EDAC MC: Ver: 3.0.0
[    0.360277] Registered efivars operations
[    0.378304] PCI: Using ACPI for IRQ routing
[    0.414700] PCI: pci_cache_line_size set to 64 bytes
[    0.414977] e820: reserve RAM buffer [mem 0x00002000-0x0000ffff]
[    0.414979] e820: reserve RAM buffer [mem 0x0005f000-0x0005ffff]
[    0.414980] e820: reserve RAM buffer [mem 0x00089000-0x0008ffff]
[    0.414981] e820: reserve RAM buffer [mem 0x6f999000-0x6fffffff]
[    0.414982] e820: reserve RAM buffer [mem 0x74410000-0x77ffffff]
[    0.414984] e820: reserve RAM buffer [mem 0x484800000-0x487ffffff]
[    0.415089] NetLabel: Initializing
[    0.415090] NetLabel:  domain hash size = 128
[    0.415090] NetLabel:  protocols = UNLABELED CIPSOv4 CALIPSO
[    0.415107] NetLabel:  unlabeled traffic allowed by default
[    0.415122] hpet0: at MMIO 0xfed00000, IRQs 2, 8, 0, 0, 0, 0, 0, 0
[    0.415122] hpet0: 8 comparators, 64-bit 24.000000 MHz counter
[    0.417056] clocksource: Switched to clocksource tsc-early
[    0.430144] VFS: Disk quotas dquot_6.6.0
[    0.430165] VFS: Dquot-cache hash table entries: 512 (order 0, 4096 bytes)
[    0.430304] AppArmor: AppArmor Filesystem Enabled
[    0.430334] pnp: PnP ACPI init
[    0.430453] system 00:00: [mem 0x40000000-0x403fffff] could not be reserved
[    0.430460] system 00:00: Plug and Play ACPI device, IDs PNP0c02 (active)
[    0.430972] system 00:01: [io  0x1800-0x18fe] has been reserved
[    0.430974] system 00:01: [mem 0xfd000000-0xfd69ffff] has been reserved
[    0.430977] system 00:01: [mem 0xfd6b0000-0xfd6cffff] has been reserved
[    0.430979] system 00:01: [mem 0xfd6f0000-0xfdffffff] has been reserved
[    0.430981] system 00:01: [mem 0xfe000000-0xfe01ffff] could not be reserved
[    0.430983] system 00:01: [mem 0xfe200000-0xfe7fffff] has been reserved
[    0.430985] system 00:01: [mem 0xff000000-0xffffffff] has been reserved
[    0.430991] system 00:01: Plug and Play ACPI device, IDs PNP0c02 (active)
[    0.431499] system 00:02: [io  0xff00-0xfffe] has been reserved
[    0.431504] system 00:02: Plug and Play ACPI device, IDs PNP0c02 (active)
[    0.434573] system 00:03: [io  0x0680-0x069f] has been reserved
[    0.434575] system 00:03: [io  0x164e-0x164f] has been reserved
[    0.434580] system 00:03: Plug and Play ACPI device, IDs PNP0c02 (active)
[    0.434655] pnp 00:04: Plug and Play ACPI device, IDs PNP0b00 (active)
[    0.434807] system 00:05: [io  0x1854-0x1857] has been reserved
[    0.434812] system 00:05: Plug and Play ACPI device, IDs INT3f0d PNP0c02 (active)
[    0.434841] pnp 00:06: Plug and Play ACPI device, IDs LEN0071 PNP0303 (active)
[    0.434865] pnp 00:07: Plug and Play ACPI device, IDs LEN0400 PNP0f13 (active)
[    0.434980] system 00:08: [io  0x1800-0x189f] could not be reserved
[    0.434983] system 00:08: [io  0x0800-0x087f] has been reserved
[    0.434985] system 00:08: [io  0x0880-0x08ff] has been reserved
[    0.434987] system 00:08: [io  0x0900-0x097f] has been reserved
[    0.434989] system 00:08: [io  0x0980-0x09ff] has been reserved
[    0.434991] system 00:08: [io  0x0a00-0x0a7f] has been reserved
[    0.434993] system 00:08: [io  0x0a80-0x0aff] has been reserved
[    0.434995] system 00:08: [io  0x0b00-0x0b7f] has been reserved
[    0.434997] system 00:08: [io  0x0b80-0x0bff] has been reserved
[    0.434999] system 00:08: [io  0x15e0-0x15ef] has been reserved
[    0.435001] system 00:08: [io  0x1600-0x167f] could not be reserved
[    0.435003] system 00:08: [io  0x1640-0x165f] could not be reserved
[    0.435006] system 00:08: [mem 0xe0000000-0xefffffff] has been reserved
[    0.435008] system 00:08: [mem 0xfed10000-0xfed13fff] has been reserved
[    0.435010] system 00:08: [mem 0xfed18000-0xfed18fff] has been reserved
[    0.435012] system 00:08: [mem 0xfed19000-0xfed19fff] has been reserved
[    0.435014] system 00:08: [mem 0xfeb00000-0xfebfffff] has been reserved
[    0.435016] system 00:08: [mem 0xfed20000-0xfed3ffff] has been reserved
[    0.435019] system 00:08: [mem 0xfed90000-0xfed93fff] has been reserved
[    0.435023] system 00:08: Plug and Play ACPI device, IDs PNP0c02 (active)
[    0.436960] system 00:09: Plug and Play ACPI device, IDs PNP0c02 (active)
[    0.438351] system 00:0a: [mem 0xfed10000-0xfed17fff] could not be reserved
[    0.438354] system 00:0a: [mem 0xfed18000-0xfed18fff] has been reserved
[    0.438356] system 00:0a: [mem 0xfed19000-0xfed19fff] has been reserved
[    0.438358] system 00:0a: [mem 0xe0000000-0xefffffff] has been reserved
[    0.438360] system 00:0a: [mem 0xfed20000-0xfed3ffff] has been reserved
[    0.438362] system 00:0a: [mem 0xfed90000-0xfed93fff] has been reserved
[    0.438364] system 00:0a: [mem 0xfed45000-0xfed8ffff] has been reserved
[    0.438366] system 00:0a: [mem 0xfee00000-0xfeefffff] has been reserved
[    0.438373] system 00:0a: Plug and Play ACPI device, IDs PNP0c02 (active)
[    0.438815] system 00:0b: [mem 0x00000000-0x0009ffff] could not be reserved
[    0.438818] system 00:0b: [mem 0x000c0000-0x000c3fff] could not be reserved
[    0.438820] system 00:0b: [mem 0x000c8000-0x000cbfff] could not be reserved
[    0.438821] system 00:0b: [mem 0x000d0000-0x000d3fff] could not be reserved
[    0.438823] system 00:0b: [mem 0x000d8000-0x000dbfff] could not be reserved
[    0.438825] system 00:0b: [mem 0x000e0000-0x000e3fff] could not be reserved
[    0.438827] system 00:0b: [mem 0x000e8000-0x000ebfff] could not be reserved
[    0.438829] system 00:0b: [mem 0x000f0000-0x000fffff] could not be reserved
[    0.438831] system 00:0b: [mem 0x00100000-0x797fffff] could not be reserved
[    0.438834] system 00:0b: [mem 0xfec00000-0xfed3ffff] could not be reserved
[    0.438836] system 00:0b: [mem 0xfed4c000-0xffffffff] could not be reserved
[    0.438841] system 00:0b: Plug and Play ACPI device, IDs PNP0c01 (active)
[    0.439022] pnp: PnP ACPI: found 12 devices
[    0.445042] clocksource: acpi_pm: mask: 0xffffff max_cycles: 0xffffff, max_idle_ns: 2085701024 ns
[    0.445091] pci 0000:03:01.0: bridge window [io  0x1000-0x0fff] to [bus 05-39] add_size 1000
[    0.445111] pci 0000:02:00.0: bridge window [io  0x1000-0x0fff] to [bus 03-3a] add_size 1000
[    0.445119] pci 0000:00:1c.4: bridge window [io  0x1000-0x0fff] to [bus 02-3a] add_size 1000
[    0.445140] pci 0000:00:1c.4: BAR 13: assigned [io  0x4000-0x4fff]
[    0.445143] pci 0000:00:1c.0: PCI bridge to [bus 01]
[    0.445149] pci 0000:00:1c.0:   bridge window [mem 0xcd600000-0xcd6fffff]
[    0.445158] pci 0000:02:00.0: BAR 13: assigned [io  0x4000-0x4fff]
[    0.445160] pci 0000:03:01.0: BAR 13: assigned [io  0x4000-0x4fff]
[    0.445162] pci 0000:03:00.0: PCI bridge to [bus 04]
[    0.445168] pci 0000:03:00.0:   bridge window [mem 0xca000000-0xca0fffff]
[    0.445179] pci 0000:03:01.0: PCI bridge to [bus 05-39]
[    0.445182] pci 0000:03:01.0:   bridge window [io  0x4000-0x4fff]
[    0.445187] pci 0000:03:01.0:   bridge window [mem 0xb4000000-0xc9efffff]
[    0.445192] pci 0000:03:01.0:   bridge window [mem 0x90000000-0xb1ffffff 64bit pref]
[    0.445199] pci 0000:03:02.0: PCI bridge to [bus 3a]
[    0.445205] pci 0000:03:02.0:   bridge window [mem 0xc9f00000-0xc9ffffff]
[    0.445215] pci 0000:02:00.0: PCI bridge to [bus 03-3a]
[    0.445218] pci 0000:02:00.0:   bridge window [io  0x4000-0x4fff]
[    0.445223] pci 0000:02:00.0:   bridge window [mem 0xb4000000-0xca0fffff]
[    0.445228] pci 0000:02:00.0:   bridge window [mem 0x90000000-0xb1ffffff 64bit pref]
[    0.445235] pci 0000:00:1c.4: PCI bridge to [bus 02-3a]
[    0.445237] pci 0000:00:1c.4:   bridge window [io  0x4000-0x4fff]
[    0.445241] pci 0000:00:1c.4:   bridge window [mem 0xb4000000-0xca0fffff]
[    0.445245] pci 0000:00:1c.4:   bridge window [mem 0x90000000-0xb1ffffff 64bit pref]
[    0.445250] pci 0000:00:1d.0: PCI bridge to [bus 3c]
[    0.445254] pci 0000:00:1d.0:   bridge window [io  0x2000-0x2fff]
[    0.445258] pci 0000:00:1d.0:   bridge window [mem 0xccc00000-0xcd5fffff]
[    0.445262] pci 0000:00:1d.0:   bridge window [mem 0xcc000000-0xcc9fffff 64bit pref]
[    0.445267] pci 0000:00:1d.4: PCI bridge to [bus 3d]
[    0.445272] pci 0000:00:1d.4:   bridge window [mem 0xccb00000-0xccbfffff]
[    0.445280] pci_bus 0000:00: resource 4 [io  0x0000-0x0cf7 window]
[    0.445282] pci_bus 0000:00: resource 5 [io  0x0d00-0xffff window]
[    0.445284] pci_bus 0000:00: resource 6 [mem 0x000a0000-0x000bffff window]
[    0.445286] pci_bus 0000:00: resource 7 [mem 0x79800000-0xdfffffff window]
[    0.445287] pci_bus 0000:00: resource 8 [mem 0xfc800000-0xfe7fffff window]
[    0.445289] pci_bus 0000:01: resource 1 [mem 0xcd600000-0xcd6fffff]
[    0.445291] pci_bus 0000:02: resource 0 [io  0x4000-0x4fff]
[    0.445293] pci_bus 0000:02: resource 1 [mem 0xb4000000-0xca0fffff]
[    0.445295] pci_bus 0000:02: resource 2 [mem 0x90000000-0xb1ffffff 64bit pref]
[    0.445297] pci_bus 0000:03: resource 0 [io  0x4000-0x4fff]
[    0.445298] pci_bus 0000:03: resource 1 [mem 0xb4000000-0xca0fffff]
[    0.445300] pci_bus 0000:03: resource 2 [mem 0x90000000-0xb1ffffff 64bit pref]
[    0.445302] pci_bus 0000:04: resource 1 [mem 0xca000000-0xca0fffff]
[    0.445303] pci_bus 0000:05: resource 0 [io  0x4000-0x4fff]
[    0.445305] pci_bus 0000:05: resource 1 [mem 0xb4000000-0xc9efffff]
[    0.445307] pci_bus 0000:05: resource 2 [mem 0x90000000-0xb1ffffff 64bit pref]
[    0.445309] pci_bus 0000:3a: resource 1 [mem 0xc9f00000-0xc9ffffff]
[    0.445310] pci_bus 0000:3c: resource 0 [io  0x2000-0x2fff]
[    0.445312] pci_bus 0000:3c: resource 1 [mem 0xccc00000-0xcd5fffff]
[    0.445314] pci_bus 0000:3c: resource 2 [mem 0xcc000000-0xcc9fffff 64bit pref]
[    0.445316] pci_bus 0000:3d: resource 1 [mem 0xccb00000-0xccbfffff]
[    0.445560] NET: Registered protocol family 2
[    0.445752] tcp_listen_portaddr_hash hash table entries: 8192 (order: 5, 131072 bytes)
[    0.445811] TCP established hash table entries: 131072 (order: 8, 1048576 bytes)
[    0.446043] TCP bind hash table entries: 65536 (order: 8, 1048576 bytes)
[    0.446160] TCP: Hash tables configured (established 131072 bind 65536)
[    0.446200] UDP hash table entries: 8192 (order: 6, 262144 bytes)
[    0.446247] UDP-Lite hash table entries: 8192 (order: 6, 262144 bytes)
[    0.446332] NET: Registered protocol family 1
[    0.446364] NET: Registered protocol family 44
[    0.446375] pci 0000:00:02.0: Video device with shadowed ROM at [mem 0x000c0000-0x000dffff]
[    0.447542] PCI: CLS 128 bytes, default 64
[    0.447582] Unpacking initramfs...
[    1.620546] Freeing initrd memory: 61568K
[    1.620599] PCI-DMA: Using software bounce buffering for IO (SWIOTLB)
[    1.620602] software IO TLB [mem 0x62ff6000-0x66ff6000] (64MB) mapped at [(____ptrval____)-(____ptrval____)]
[    1.620770] clocksource: tsc: mask: 0xffffffffffffffff max_cycles: 0x19f2297dd97, max_idle_ns: 440795236593 ns
[    1.620787] clocksource: Switched to clocksource tsc
[    1.620916] Scanning for low memory corruption every 60 seconds
[    1.621806] Initialise system trusted keyrings
[    1.621819] Key type blacklist registered
[    1.621852] workingset: timestamp_bits=36 max_order=22 bucket_order=0
[    1.623366] zbud: loaded
[    1.624042] squashfs: version 4.0 (2009/01/31) Phillip Lougher
[    1.624270] fuse init (API version 7.27)
[    1.624340] pstore: using deflate compression
[    1.625642] Key type asymmetric registered
[    1.625644] Asymmetric key parser 'x509' registered
[    1.625675] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 244)
[    1.625714] io scheduler noop registered
[    1.625715] io scheduler deadline registered
[    1.625745] io scheduler cfq registered (default)
[    1.627362] pcieport 0000:00:1c.0: Signaling PME with IRQ 120
[    1.627385] pcieport 0000:00:1c.4: Signaling PME with IRQ 121
[    1.627406] pcieport 0000:00:1d.0: Signaling PME with IRQ 122
[    1.627431] pcieport 0000:00:1d.4: Signaling PME with IRQ 123
[    1.627453] pciehp 0000:00:1c.4:pcie004: Slot #4 AttnBtn- PwrCtrl- MRL- AttnInd- PwrInd- HotPlug+ Surprise+ Interlock- NoCompl+ LLActRep+
[    1.627487] pciehp 0000:00:1d.0:pcie004: Slot #0 AttnBtn- PwrCtrl- MRL- AttnInd- PwrInd- HotPlug+ Surprise+ Interlock- NoCompl+ LLActRep+
[    1.627513] pciehp 0000:03:01.0:pcie204: Slot #1 AttnBtn- PwrCtrl- MRL- AttnInd- PwrInd- HotPlug+ Surprise+ Interlock- NoCompl+ LLActRep+
[    1.627570] shpchp: Standard Hot Plug PCI Controller Driver version: 0.4
[    1.627637] efifb: probing for efifb
[    1.627652] efifb: framebuffer at 0x80000000, using 8128k, total 8128k
[    1.627653] efifb: mode is 1920x1080x32, linelength=7680, pages=1
[    1.627654] efifb: scrolling: redraw
[    1.627656] efifb: Truecolor: size=8:8:8:8, shift=24:16:8:0
[    1.627757] Console: switching to colour frame buffer device 240x67
[    1.627790] fb0: EFI VGA frame buffer device
[    1.627799] intel_idle: MWAIT substates: 0x11142120
[    1.627800] intel_idle: v0.4.1 model 0x8E
[    1.628297] intel_idle: lapic_timer_reliable_states 0xffffffff
[    1.629979] ACPI: AC Adapter [AC] (off-line)
[    1.631299] input: Sleep Button as /devices/LNXSYSTM:00/LNXSYBUS:00/PNP0C0E:00/input/input0
[    1.631312] ACPI: Sleep Button [SLPB]
[    1.631356] input: Lid Switch as /devices/LNXSYSTM:00/LNXSYBUS:00/PNP0C0D:00/input/input1
[    1.631363] ACPI: Lid Switch [LID]
[    1.631400] input: Power Button as /devices/LNXSYSTM:00/LNXPWRBN:00/input/input2
[    1.631407] ACPI: Power Button [PWRF]
[    1.666835] thermal LNXTHERM:00: registered as thermal_zone0
[    1.666837] ACPI: Thermal Zone [THM0] (50 C)
[    1.667096] Serial: 8250/16550 driver, 32 ports, IRQ sharing enabled
[    1.669501] Linux agpgart interface v0.103
[    1.671273] tpm_tis STM7308:00: 2.0 TPM (device-id 0x0, rev-id 78)
[    1.689482] loop: module loaded
[    1.689704] libphy: Fixed MDIO Bus: probed
[    1.689705] tun: Universal TUN/TAP device driver, 1.6
[    1.689742] PPP generic driver version 2.4.2
[    1.689789] ehci_hcd: USB 2.0 'Enhanced' Host Controller (EHCI) Driver
[    1.689792] ehci-pci: EHCI PCI platform driver
[    1.689805] ehci-platform: EHCI generic platform driver
[    1.689818] ohci_hcd: USB 1.1 'Open' Host Controller (OHCI) Driver
[    1.689820] ohci-pci: OHCI PCI platform driver
[    1.689831] ohci-platform: OHCI generic platform driver
[    1.689840] uhci_hcd: USB Universal Host Controller Interface driver
[    1.690762] xhci_hcd 0000:00:14.0: xHCI Host Controller
[    1.690774] xhci_hcd 0000:00:14.0: new USB bus registered, assigned bus number 1
[    1.691867] xhci_hcd 0000:00:14.0: hcc params 0x200077c1 hci version 0x110 quirks 0x0000000000009810
[    1.691872] xhci_hcd 0000:00:14.0: cache line size of 128 is not supported
[    1.692207] usb usb1: New USB device found, idVendor=1d6b, idProduct=0002, bcdDevice= 4.18
[    1.692210] usb usb1: New USB device strings: Mfr=3, Product=2, SerialNumber=1
[    1.692212] usb usb1: Product: xHCI Host Controller
[    1.692213] usb usb1: Manufacturer: Linux 4.18.0-18-generic xhci-hcd
[    1.692215] usb usb1: SerialNumber: 0000:00:14.0
[    1.692829] hub 1-0:1.0: USB hub found
[    1.692846] hub 1-0:1.0: 12 ports detected
[    1.703351] xhci_hcd 0000:00:14.0: xHCI Host Controller
[    1.703356] xhci_hcd 0000:00:14.0: new USB bus registered, assigned bus number 2
[    1.703360] xhci_hcd 0000:00:14.0: Host supports USB 3.1 Enhanced SuperSpeed
[    1.703411] usb usb2: New USB device found, idVendor=1d6b, idProduct=0003, bcdDevice= 4.18
[    1.703413] usb usb2: New USB device strings: Mfr=3, Product=2, SerialNumber=1
[    1.703415] usb usb2: Product: xHCI Host Controller
[    1.703417] usb usb2: Manufacturer: Linux 4.18.0-18-generic xhci-hcd
[    1.703419] usb usb2: SerialNumber: 0000:00:14.0
[    1.703777] hub 2-0:1.0: USB hub found
[    1.703789] hub 2-0:1.0: 6 ports detected
[    1.708240] usb: port power management may be unreliable
[    1.710097] xhci_hcd 0000:3a:00.0: xHCI Host Controller
[    1.710104] xhci_hcd 0000:3a:00.0: new USB bus registered, assigned bus number 3
[    1.711255] xhci_hcd 0000:3a:00.0: hcc params 0x200077c1 hci version 0x110 quirks 0x0000000000009810
[    1.711587] usb usb3: New USB device found, idVendor=1d6b, idProduct=0002, bcdDevice= 4.18
[    1.711589] usb usb3: New USB device strings: Mfr=3, Product=2, SerialNumber=1
[    1.711591] usb usb3: Product: xHCI Host Controller
[    1.711593] usb usb3: Manufacturer: Linux 4.18.0-18-generic xhci-hcd
[    1.711594] usb usb3: SerialNumber: 0000:3a:00.0
[    1.711713] hub 3-0:1.0: USB hub found
[    1.711722] hub 3-0:1.0: 2 ports detected
[    1.718479] xhci_hcd 0000:3a:00.0: xHCI Host Controller
[    1.718483] xhci_hcd 0000:3a:00.0: new USB bus registered, assigned bus number 4
[    1.718487] xhci_hcd 0000:3a:00.0: Host supports USB 3.1 Enhanced SuperSpeed
[    1.718525] usb usb4: New USB device found, idVendor=1d6b, idProduct=0003, bcdDevice= 4.18
[    1.718527] usb usb4: New USB device strings: Mfr=3, Product=2, SerialNumber=1
[    1.718529] usb usb4: Product: xHCI Host Controller
[    1.718531] usb usb4: Manufacturer: Linux 4.18.0-18-generic xhci-hcd
[    1.718532] usb usb4: SerialNumber: 0000:3a:00.0
[    1.719022] hub 4-0:1.0: USB hub found
[    1.719033] hub 4-0:1.0: 2 ports detected
[    1.724060] i8042: PNP: PS/2 Controller [PNP0303:KBD,PNP0f13:MOU] at 0x60,0x64 irq 1,12
[    1.726185] serio: i8042 KBD port at 0x60,0x64 irq 1
[    1.726190] serio: i8042 AUX port at 0x60,0x64 irq 12
[    1.726317] mousedev: PS/2 mouse device common for all mice
[    1.726503] rtc_cmos 00:04: RTC can wake from S4
[    1.727472] rtc_cmos 00:04: registered as rtc0
[    1.727491] rtc_cmos 00:04: alarms up to one month, y3k, 242 bytes nvram, hpet irqs
[    1.727499] i2c /dev entries driver
[    1.727504] pcie_mp2_amd: AMD(R) PCI-E MP2 Communication Driver Version: 1.0
[    1.727591] device-mapper: uevent: version 1.0.3
[    1.727740] device-mapper: ioctl: 4.39.0-ioctl (2018-04-03) initialised: dm-devel@redhat.com
[    1.727744] intel_pstate: Intel P-state driver initializing
[    1.728189] input: AT Translated Set 2 keyboard as /devices/platform/i8042/serio0/input/input3
[    1.728493] intel_pstate: HWP enabled
[    1.728567] ledtrig-cpu: registered to indicate activity on CPUs
[    1.728569] EFI Variables Facility v0.08 2004-May-17
[    1.744915] intel_pmc_core:  initialized
[    1.745064] NET: Registered protocol family 10
[    1.747454] Segment Routing with IPv6
[    1.747465] NET: Registered protocol family 17
[    1.747494] Key type dns_resolver registered
[    1.747757] RAS: Correctable Errors collector initialized.
[    1.747779] microcode: sig=0x806eb, pf=0x80, revision=0xa4
[    1.747816] microcode: Microcode Update Driver: v2.2.
[    1.747822] sched_clock: Marking stable (1747814182, 0)->(1728313522, 19500660)
[    1.748009] registered taskstats version 1
[    1.748015] Loading compiled-in X.509 certificates
[    1.749594] Loaded X.509 cert 'Build time autogenerated kernel key: f8e50bb784a026944d779efa6a4082ac5a8d006f'
[    1.749945] Loaded UEFI:db cert 'Lenovo Ltd.: ThinkPad Product CA 2012: 838b1f54c1550463f45f98700640f11069265949' linked to secondary sys keyring
[    1.749954] Loaded UEFI:db cert 'Lenovo UEFI CA 2014: 4b91a68732eaefdd2c8ffffc6b027ec3449e9c8f' linked to secondary sys keyring
[    1.749968] Loaded UEFI:db cert 'Microsoft Corporation UEFI CA 2011: 13adbf4309bd82709c8cd54f316ed522988a1bd4' linked to secondary sys keyring
[    1.749982] Loaded UEFI:db cert 'Microsoft Windows Production PCA 2011: a92902398e16c49778cd90f99e4f9ae17c55af53' linked to secondary sys keyring
[    1.750530] zswap: loaded using pool lzo/zbud
[    1.752987] Key type big_key registered
[    1.752989] Key type trusted registered
[    1.754241] Key type encrypted registered
[    1.754243] AppArmor: AppArmor sha1 policy hashing enabled
[    1.755869] ima: Allocated hash algorithm: sha1
[    1.772191] evm: Initialising EVM extended attributes:
[    1.772192] evm: security.selinux
[    1.772193] evm: security.SMACK64
[    1.772193] evm: security.SMACK64EXEC
[    1.772193] evm: security.SMACK64TRANSMUTE
[    1.772194] evm: security.SMACK64MMAP
[    1.772194] evm: security.apparmor
[    1.772194] evm: security.ima
[    1.772195] evm: security.capability
[    1.772195] evm: HMAC attrs: 0x1
[    1.776145]   Magic number: 3:889:271
[    1.776188] acpi INT34B9:00: hash matches
[    1.776430] rtc_cmos 00:04: setting system clock to 2019-05-03 09:16:45 UTC (1556875005)
[    1.863220] ACPI: Battery Slot [BAT0] (battery present)
[    2.036045] usb 1-1: new full-speed USB device number 2 using xhci_hcd
[    2.115539] Freeing unused kernel image memory: 2464K
[    2.120346] Write protecting the kernel read-only data: 20480k
[    2.121445] Freeing unused kernel image memory: 2008K
[    2.121632] Freeing unused kernel image memory: 1760K
[    2.126770] x86/mm: Checked W+X mappings: passed, no W+X pages found.
[    2.179108] acpi PNP0C14:02: duplicate WMI GUID 05901221-D566-11D1-B2F0-00A0C9062910 (first instance was on PNP0C14:01)
[    2.179162] acpi PNP0C14:03: duplicate WMI GUID 05901221-D566-11D1-B2F0-00A0C9062910 (first instance was on PNP0C14:01)
[    2.179267] acpi PNP0C14:04: duplicate WMI GUID 05901221-D566-11D1-B2F0-00A0C9062910 (first instance was on PNP0C14:01)
[    2.179376] acpi PNP0C14:05: duplicate WMI GUID 05901221-D566-11D1-B2F0-00A0C9062910 (first instance was on PNP0C14:01)
[    2.181392] rtsx_pci 0000:01:00.0: enabling device (0000 -> 0002)
[    2.182714] thunderbolt 0000:04:00.0: NHI initialized, starting thunderbolt
[    2.182717] thunderbolt 0000:04:00.0: allocating TX ring 0 of size 10
[    2.182730] thunderbolt 0000:04:00.0: allocating RX ring 0 of size 10
[    2.182743] thunderbolt 0000:04:00.0: control channel created
[    2.182744] thunderbolt 0000:04:00.0: control channel starting...
[    2.182747] thunderbolt 0000:04:00.0: starting TX ring 0
[    2.182754] thunderbolt 0000:04:00.0: enabling interrupt at register 0x38200 bit 0 (0x0 -> 0x1)
[    2.182756] thunderbolt 0000:04:00.0: starting RX ring 0
[    2.182762] thunderbolt 0000:04:00.0: enabling interrupt at register 0x38200 bit 12 (0x1 -> 0x1001)
[    2.186516] e1000e: Intel(R) PRO/1000 Network Driver - 3.2.6-k
[    2.186517] e1000e: Copyright(c) 1999 - 2015 Intel Corporation.
[    2.186791] e1000e 0000:00:1f.6: Interrupt Throttling Rate (ints/sec) set to dynamic conservative mode
[    2.187606] nvme nvme0: pci function 0000:3d:00.0
[    2.195527] usb 1-1: New USB device found, idVendor=058f, idProduct=9540, bcdDevice= 1.20
[    2.195529] usb 1-1: New USB device strings: Mfr=1, Product=2, SerialNumber=0
[    2.195530] usb 1-1: Product: EMV Smartcard Reader
[    2.195531] usb 1-1: Manufacturer: Generic
[    2.207851] checking generic (80000000 7f0000) vs hw (80000000 10000000)
[    2.207852] fb: switching to inteldrmfb from EFI VGA
[    2.207866] Console: switching to colour dummy device 80x25
[    2.207916] [drm] Replacing VGA console driver
[    2.208718] [drm] Supports vblank timestamp caching Rev 2 (21.10.2013).
[    2.208718] [drm] Driver supports precise vblank timestamp query.
[    2.209195] i915 0000:00:02.0: vgaarb: changed VGA decodes: olddecodes=io+mem,decodes=io+mem:owns=io+mem
[    2.209834] [drm] Finished loading DMC firmware i915/kbl_dmc_ver1_04.bin (v1.4)
[    2.215125] random: fast init done
[    2.218346] random: systemd-udevd: uninitialized urandom read (16 bytes read)
[    2.218352] random: systemd-udevd: uninitialized urandom read (16 bytes read)
[    2.218355] random: systemd-udevd: uninitialized urandom read (16 bytes read)
[    2.218688] [drm] Initialized i915 1.6.0 20180514 for 0000:00:02.0 on minor 0
[    2.220375] ACPI: Video Device [GFX0] (multi-head: yes  rom: no  post: no)
[    2.220663] input: Video Bus as /devices/LNXSYSTM:00/LNXSYBUS:00/PNP0A08:00/LNXVIDEO:00/input/input6
[    2.228292] fbcon: inteldrmfb (fb0) is primary device
[    2.228369] Console: switching to colour frame buffer device 240x67
[    2.228386] i915 0000:00:02.0: fb0: inteldrmfb frame buffer device
[    2.312853] thunderbolt 0000:04:00.0: current switch config:
[    2.312855] thunderbolt 0000:04:00.0:  Switch: 8086:15c0 (Revision: 1, TB Version: 2)
[    2.312855] thunderbolt 0000:04:00.0:   Max Port Number: 5
[    2.312856] thunderbolt 0000:04:00.0:   Config:
[    2.312857] thunderbolt 0000:04:00.0:    Upstream Port Number: 3 Depth: 0 Route String: 0x0 Enabled: 1, PlugEventsDelay: 254ms
[    2.312858] thunderbolt 0000:04:00.0:    unknown1: 0x0 unknown4: 0x0
[    2.324009] usb 1-8: new high-speed USB device number 3 using xhci_hcd
[    2.355566] thunderbolt 0000:04:00.0: 0: uid: 0x109cfb72c882300
[    2.356907] thunderbolt 0000:04:00.0:  Port 0: 8086:15c0 (Revision: 1, TB Version: 1, Type: Port (0x1))
[    2.356908] thunderbolt 0000:04:00.0:   Max hop id (in/out): 7/7
[    2.356909] thunderbolt 0000:04:00.0:   Max counters: 8
[    2.356909] thunderbolt 0000:04:00.0:   NFC Credits: 0x800000
[    2.357390] thunderbolt 0000:04:00.0:  Port 1: 8086:15c0 (Revision: 1, TB Version: 1, Type: Port (0x1))
[    2.357390] thunderbolt 0000:04:00.0:   Max hop id (in/out): 15/15
[    2.357391] thunderbolt 0000:04:00.0:   Max counters: 16
[    2.357392] thunderbolt 0000:04:00.0:   NFC Credits: 0x3c00000
[    2.357933] thunderbolt 0000:04:00.0:  Port 2: 8086:15c0 (Revision: 1, TB Version: 1, Type: Port (0x1))
[    2.357934] thunderbolt 0000:04:00.0:   Max hop id (in/out): 15/15
[    2.357935] thunderbolt 0000:04:00.0:   Max counters: 16
[    2.357936] thunderbolt 0000:04:00.0:   NFC Credits: 0x3c00000
[    2.358030] thunderbolt 0000:04:00.0:  Port 3: 8086:15c0 (Revision: 1, TB Version: 1, Type: NHI (0x2))
[    2.358030] thunderbolt 0000:04:00.0:   Max hop id (in/out): 11/11
[    2.358031] thunderbolt 0000:04:00.0:   Max counters: 16
[    2.358032] thunderbolt 0000:04:00.0:   NFC Credits: 0x1000000
[    2.358157] thunderbolt 0000:04:00.0:  Port 4: 8086:15c0 (Revision: 1, TB Version: 1, Type: PCIe (0x100101))
[    2.358158] thunderbolt 0000:04:00.0:   Max hop id (in/out): 8/8
[    2.358158] thunderbolt 0000:04:00.0:   Max counters: 2
[    2.358159] thunderbolt 0000:04:00.0:   NFC Credits: 0x800000
[    2.358310] thunderbolt 0000:04:00.0:  Port 5: 8086:15c0 (Revision: 1, TB Version: 1, Type: DP/HDMI (0xe0101))
[    2.358310] thunderbolt 0000:04:00.0:   Max hop id (in/out): 9/9
[    2.358311] thunderbolt 0000:04:00.0:   Max counters: 2
[    2.358312] thunderbolt 0000:04:00.0:   NFC Credits: 0x1000000
[    2.430675] e1000e 0000:00:1f.6 0000:00:1f.6 (uninitialized): registered PHC clock
[    2.485940]  nvme0n1: p1 p2
[    2.500454] e1000e 0000:00:1f.6 eth0: (PCI Express:2.5GT/s:Width x1) e8:6a:64:b7:66:b0
[    2.500456] e1000e 0000:00:1f.6 eth0: Intel(R) PRO/1000 Network Connection
[    2.500520] e1000e 0000:00:1f.6 eth0: MAC: 13, PHY: 12, PBA No: FFFFFF-0FF
[    2.501159] e1000e 0000:00:1f.6 enp0s31f6: renamed from eth0
[    2.530126] usb 1-8: New USB device found, idVendor=04f2, idProduct=b67c, bcdDevice=67.23
[    2.530127] usb 1-8: New USB device strings: Mfr=3, Product=1, SerialNumber=2
[    2.530147] usb 1-8: Product: Integrated Camera
[    2.530148] usb 1-8: Manufacturer: Chicony Electronics Co.,Ltd.
[    2.530148] usb 1-8: SerialNumber: 0001
[    2.660187] usb 1-9: new full-speed USB device number 4 using xhci_hcd
[    2.727927] psmouse serio1: elantech: assuming hardware version 4 (with firmware version 0x5f3001)
[    2.738777] psmouse serio1: elantech: Synaptics capabilities query result 0x90, 0x18, 0x0f.
[    2.749689] psmouse serio1: elantech: Elan sample query result 00, 31, b7
[    2.760585] psmouse serio1: elantech: Trying to set up SMBus access
[    2.760589] psmouse serio1: elantech: SMbus companion is not ready yet
[    2.793963] input: ETPS/2 Elantech TrackPoint as /devices/platform/i8042/serio1/input/input7
[    2.806819] input: ETPS/2 Elantech Touchpad as /devices/platform/i8042/serio1/input/input5
[    2.809637] usb 1-9: New USB device found, idVendor=06cb, idProduct=00bd, bcdDevice= 0.00
[    2.809638] usb 1-9: New USB device strings: Mfr=0, Product=0, SerialNumber=1
[    2.809640] usb 1-9: SerialNumber: 9fef321d90a4
[    2.936183] usb 1-10: new full-speed USB device number 5 using xhci_hcd
[    3.086874] usb 1-10: New USB device found, idVendor=8087, idProduct=0aaa, bcdDevice= 0.02
[    3.086876] usb 1-10: New USB device strings: Mfr=0, Product=0, SerialNumber=0
[    4.796047] raid6: sse2x1   gen() 13229 MB/s
[    4.844047] raid6: sse2x1   xor()  9734 MB/s
[    4.892070] raid6: sse2x2   gen() 16336 MB/s
[    4.940046] raid6: sse2x2   xor() 11089 MB/s
[    4.988071] raid6: sse2x4   gen() 17295 MB/s
[    5.036037] raid6: sse2x4   xor() 11780 MB/s
[    5.084068] raid6: avx2x1   gen() 26571 MB/s
[    5.132068] raid6: avx2x1   xor() 18512 MB/s
[    5.180068] raid6: avx2x2   gen() 31930 MB/s
[    5.228044] raid6: avx2x2   xor() 20263 MB/s
[    5.276043] raid6: avx2x4   gen() 33718 MB/s
[    5.324038] raid6: avx2x4   xor() 23221 MB/s
[    5.324038] raid6: using algorithm avx2x4 gen() 33718 MB/s
[    5.324039] raid6: .... xor() 23221 MB/s, rmw enabled
[    5.324039] raid6: using avx2x2 recovery algorithm
[    5.325922] xor: automatically using best checksumming function   avx       
[    5.336443] Btrfs loaded, crc32c=crc32c-intel
[    5.440985] EXT4-fs (nvme0n1p2): mounted filesystem with ordered data mode. Opts: (null)
[    6.110901] systemd[1]: systemd 237 running in system mode. (+PAM +AUDIT +SELINUX +IMA +APPARMOR +SMACK +SYSVINIT +UTMP +LIBCRYPTSETUP +GCRYPT +GNUTLS +ACL +XZ +LZ4 +SECCOMP +BLKID +ELFUTILS +KMOD -IDN2 +IDN -PCRE2 default-hierarchy=hybrid)
[    6.128832] systemd[1]: Detected architecture x86-64.
[    6.131522] systemd[1]: Set hostname to <theon>.
[    6.175160] systemd[1]: Reached target System Time Synchronized.
[    6.175291] systemd[1]: Created slice System Slice.
[    6.175361] systemd[1]: Created slice system-systemd\x2dfsck.slice.
[    6.175396] systemd[1]: Listening on Journal Socket (/dev/log).
[    6.175423] systemd[1]: Listening on /dev/initctl Compatibility Named Pipe.
[    6.175442] systemd[1]: Listening on udev Kernel Socket.
[    6.175496] systemd[1]: Listening on Journal Audit Socket.
[    6.185582] EXT4-fs (nvme0n1p2): re-mounted. Opts: errors=remount-ro
[    6.205868] lp: driver loaded but no devices found
[    6.217883] ppdev: user-space parallel port driver
[    6.236359] systemd-journald[391]: Received request to flush runtime journal from PID 1
[    6.252018] Adding 2097148k swap on /swapfile.  Priority:-2 extents:6 across:2260988k SSFS
[    6.351952] proc_thermal 0000:00:04.0: enabling device (0000 -> 0002)
[    6.352571] intel-lpss 0000:00:15.0: enabling device (0000 -> 0002)
[    6.356736] cfg80211: Loading compiled-in X.509 certificates for regulatory database
[    6.356797] Non-volatile memory driver v1.3
[    6.357224] mei_me 0000:00:16.0: enabling device (0000 -> 0002)
[    6.362436] cfg80211: Loaded X.509 cert 'sforshee: 00b28ddf47aef9cea7'
[    6.371281] Intel(R) Wireless WiFi driver for Linux
[    6.371282] Copyright(c) 2003- 2015 Intel Corporation
[    6.371333] iwlwifi 0000:00:14.3: enabling device (0000 -> 0002)
[    6.376382] idma64 idma64.0: Found Intel integrated DMA 64-bit
[    6.377645] snd_hda_intel 0000:00:1f.3: bound 0000:00:02.0 (ops i915_audio_component_bind_ops [i915])
[    6.382029] RAPL PMU: API unit is 2^-32 Joules, 5 fixed counters, 655360 ms ovfl timer
[    6.382030] RAPL PMU: hw unit of domain pp0-core 2^-14 Joules
[    6.382030] RAPL PMU: hw unit of domain package 2^-14 Joules
[    6.382031] RAPL PMU: hw unit of domain dram 2^-14 Joules
[    6.382031] RAPL PMU: hw unit of domain pp1-gpu 2^-14 Joules
[    6.382032] RAPL PMU: hw unit of domain psys 2^-14 Joules
[    6.393226] thinkpad_acpi: ThinkPad ACPI Extras v0.26
[    6.393227] thinkpad_acpi: http://ibm-acpi.sf.net/
[    6.393228] thinkpad_acpi: ThinkPad BIOS N2JET29W (1.07 ), EC unknown
[    6.393229] thinkpad_acpi: Lenovo ThinkPad T490s, model 20NYS02A00
[    6.395349] cryptd: max_cpu_qlen set to 1000
[    6.403386] AVX2 version of gcm_enc/dec engaged.
[    6.403388] AES CTR mode by8 optimization enabled
[    6.409071] random: crng init done
[    6.409073] random: 7 urandom warning(s) missed due to ratelimiting
[    6.411611] thinkpad_acpi: radio switch found; radios are enabled
[    6.411624] thinkpad_acpi: This ThinkPad has standard ACPI backlight brightness control, supported by the ACPI video driver
[    6.411624] thinkpad_acpi: Disabling thinkpad-acpi brightness events by default...
[    6.411767] snd_hda_codec_realtek hdaudioC0D0: autoconfig for ALC257: line_outs=1 (0x14/0x0/0x0/0x0/0x0) type:speaker
[    6.411769] snd_hda_codec_realtek hdaudioC0D0:    speaker_outs=0 (0x0/0x0/0x0/0x0/0x0)
[    6.411770] snd_hda_codec_realtek hdaudioC0D0:    hp_outs=1 (0x21/0x0/0x0/0x0/0x0)
[    6.411771] snd_hda_codec_realtek hdaudioC0D0:    mono: mono_out=0x0
[    6.411772] snd_hda_codec_realtek hdaudioC0D0:    inputs:
[    6.411774] snd_hda_codec_realtek hdaudioC0D0:      Mic=0x19
[    6.411775] snd_hda_codec_realtek hdaudioC0D0:      Internal Mic=0x12
[    6.412491] iwlwifi 0000:00:14.3: loaded firmware version 38.c0e03d94.0 op_mode iwlmvm
[    6.446347] iwlwifi 0000:00:14.3: Detected Intel(R) Dual Band Wireless AC 9560, REV=0x318
[    6.478219] kvm: disabled by bios
[    6.493941] thinkpad_acpi: rfkill switch tpacpi_bluetooth_sw: radio is unblocked
[    6.495014] intel_rapl: Found RAPL domain package
[    6.495015] intel_rapl: Found RAPL domain core
[    6.495016] intel_rapl: Found RAPL domain uncore
[    6.495016] intel_rapl: Found RAPL domain dram
[    6.495276] iwlwifi 0000:00:14.3: base HW address: 98:2c:bc:23:fe:47
[    6.505064] thinkpad_acpi: Standard ACPI backlight interface available, not loading native one
[    6.517045] kvm: disabled by bios
[    6.565378] ieee80211 phy0: Selected rate control algorithm 'iwl-mvm-rs'
[    6.565645] thermal thermal_zone6: failed to read out thermal zone (-61)
[    6.567736] iwlwifi 0000:00:14.3 wlp0s20f3: renamed from wlan0
[    6.576988] thinkpad_acpi: battery 1 registered (start 0, stop 100)
[    6.576991] battery: new extension: ThinkPad Battery Extension
[    6.577022] input: ThinkPad Extra Buttons as /devices/platform/thinkpad_acpi/input/input8
[    6.629896] input: HDA Intel PCH Mic as /devices/pci0000:00/0000:00:1f.3/sound/card0/input9
[    6.630108] input: HDA Intel PCH Headphone as /devices/pci0000:00/0000:00:1f.3/sound/card0/input10
[    6.630154] input: HDA Intel PCH HDMI/DP,pcm=3 as /devices/pci0000:00/0000:00:1f.3/sound/card0/input11
[    6.630197] input: HDA Intel PCH HDMI/DP,pcm=7 as /devices/pci0000:00/0000:00:1f.3/sound/card0/input12
[    6.630236] input: HDA Intel PCH HDMI/DP,pcm=8 as /devices/pci0000:00/0000:00:1f.3/sound/card0/input13
[    6.630274] input: HDA Intel PCH HDMI/DP,pcm=9 as /devices/pci0000:00/0000:00:1f.3/sound/card0/input14
[    6.630319] input: HDA Intel PCH HDMI/DP,pcm=10 as /devices/pci0000:00/0000:00:1f.3/sound/card0/input15
[    6.729700] audit: type=1400 audit(1556875010.448:2): apparmor="STATUS" operation="profile_load" profile="unconfined" name="libreoffice-xpdfimport" pid=755 comm="apparmor_parser"
[    6.734100] audit: type=1400 audit(1556875010.452:3): apparmor="STATUS" operation="profile_load" profile="unconfined" name="libreoffice-senddoc" pid=757 comm="apparmor_parser"
[    6.759094] audit: type=1400 audit(1556875010.476:4): apparmor="STATUS" operation="profile_load" profile="unconfined" name="libreoffice-oopslash" pid=752 comm="apparmor_parser"
[    6.771247] audit: type=1400 audit(1556875010.488:5): apparmor="STATUS" operation="profile_load" profile="unconfined" name="/usr/sbin/ippusbxd" pid=770 comm="apparmor_parser"
[    6.786039] audit: type=1400 audit(1556875010.504:6): apparmor="STATUS" operation="profile_load" profile="unconfined" name="/usr/bin/man" pid=754 comm="apparmor_parser"
[    6.786514] audit: type=1400 audit(1556875010.504:7): apparmor="STATUS" operation="profile_load" profile="unconfined" name="man_filter" pid=754 comm="apparmor_parser"
[    6.786958] audit: type=1400 audit(1556875010.504:8): apparmor="STATUS" operation="profile_load" profile="unconfined" name="man_groff" pid=754 comm="apparmor_parser"
[    6.806056] audit: type=1400 audit(1556875010.524:9): apparmor="STATUS" operation="profile_load" profile="unconfined" name="/usr/sbin/cups-browsed" pid=761 comm="apparmor_parser"
[    6.840951] audit: type=1400 audit(1556875010.560:10): apparmor="STATUS" operation="profile_load" profile="unconfined" name="/usr/sbin/ntpd" pid=772 comm="apparmor_parser"
[    6.910083] audit: type=1400 audit(1556875010.628:11): apparmor="STATUS" operation="profile_load" profile="unconfined" name="/usr/sbin/tcpdump" pid=776 comm="apparmor_parser"
[    7.408016] Bluetooth: Core ver 2.22
[    7.408036] NET: Registered protocol family 31
[    7.408037] Bluetooth: HCI device and connection manager initialized
[    7.408679] Bluetooth: HCI socket layer initialized
[    7.408681] Bluetooth: L2CAP socket layer initialized
[    7.408688] Bluetooth: SCO socket layer initialized
[    7.426794] media: Linux media interface: v0.10
[    7.434892] videodev: Linux video capture interface: v2.00
[    7.548385] usbcore: registered new interface driver btusb
[    7.548806] Bluetooth: hci0: Bootloader revision 0.1 build 42 week 52 2015
[    7.549842] Bluetooth: hci0: Device revision is 2
[    7.549843] Bluetooth: hci0: Secure boot is enabled
[    7.549843] Bluetooth: hci0: OTP lock is enabled
[    7.549844] Bluetooth: hci0: API lock is enabled
[    7.549844] Bluetooth: hci0: Debug lock is disabled
[    7.549845] Bluetooth: hci0: Minimum firmware build 1 week 10 2014
[    7.550564] Bluetooth: hci0: Found device firmware: intel/ibt-17-16-1.sfi
[    7.559502] Bluetooth: BNEP (Ethernet Emulation) ver 1.3
[    7.559503] Bluetooth: BNEP filters: protocol multicast
[    7.559505] Bluetooth: BNEP socket layer initialized
[    7.581278] uvcvideo: Found UVC 1.50 device Integrated Camera (04f2:b67c)
[    7.588478] uvcvideo 1-8:1.0: Entity type for entity Realtek Extended Controls Unit was not initialized!
[    7.588480] uvcvideo 1-8:1.0: Entity type for entity Extension 4 was not initialized!
[    7.588481] uvcvideo 1-8:1.0: Entity type for entity Processing 2 was not initialized!
[    7.588481] uvcvideo 1-8:1.0: Entity type for entity Camera 1 was not initialized!
[    7.588525] input: Integrated Camera: Integrated C as /devices/pci0000:00/0000:00:14.0/usb1/1-8/1-8:1.0/input/input16
[    7.589037] uvcvideo: Unknown video format 00000032-0002-0010-8000-00aa00389b71
[    7.590146] uvcvideo: Found UVC 1.50 device Integrated Camera (04f2:b67c)
[    7.591630] uvcvideo: Unable to create debugfs 1-3 directory.
[    7.591689] uvcvideo 1-8:1.2: Entity type for entity Realtek Extended Controls Unit was not initialized!
[    7.591690] uvcvideo 1-8:1.2: Entity type for entity Microsoft Extended Controls Uni was not initialized!
[    7.591691] uvcvideo 1-8:1.2: Entity type for entity Extension 9 was not initialized!
[    7.591692] uvcvideo 1-8:1.2: Entity type for entity Extension 11 was not initialized!
[    7.591693] uvcvideo 1-8:1.2: Entity type for entity Processing 15 was not initialized!
[    7.591694] uvcvideo 1-8:1.2: Entity type for entity Camera 8 was not initialized!
[    7.591734] input: Integrated Camera: Integrated I as /devices/pci0000:00/0000:00:14.0/usb1/1-8/1-8:1.2/input/input17
[    7.591776] usbcore: registered new interface driver uvcvideo
[    7.591777] USB Video Class driver (1.1.1)
[    7.606538] IPv6: ADDRCONF(NETDEV_UP): enp0s31f6: link is not ready
[    7.800738] IPv6: ADDRCONF(NETDEV_UP): enp0s31f6: link is not ready
[    7.803105] IPv6: ADDRCONF(NETDEV_UP): wlp0s20f3: link is not ready
[    7.992971] IPv6: ADDRCONF(NETDEV_UP): wlp0s20f3: link is not ready
[    8.050117] IPv6: ADDRCONF(NETDEV_UP): wlp0s20f3: link is not ready
[    8.986407] Bluetooth: hci0: Waiting for firmware download to complete
[    8.986833] Bluetooth: hci0: Firmware loaded in 1404737 usecs
[    8.986987] Bluetooth: hci0: Waiting for device to boot
[    8.999897] Bluetooth: hci0: Device booted in 12697 usecs
[    9.000218] Bluetooth: hci0: Found Intel DDC parameters: intel/ibt-17-16-1.ddc
[    9.002913] Bluetooth: hci0: Applying Intel DDC parameters completed
[   11.351835] wlp0s20f3: authenticate with f4:ec:38:eb:d5:46
[   11.358590] wlp0s20f3: send auth to f4:ec:38:eb:d5:46 (try 1/3)
[   11.396814] wlp0s20f3: authenticated
[   11.400057] wlp0s20f3: associate with f4:ec:38:eb:d5:46 (try 1/3)
[   11.404042] wlp0s20f3: RX AssocResp from f4:ec:38:eb:d5:46 (capab=0x31 status=0 aid=3)
[   11.406452] wlp0s20f3: associated
[   11.433433] IPv6: ADDRCONF(NETDEV_CHANGE): wlp0s20f3: link becomes ready
[   11.756441] Bluetooth: RFCOMM TTY layer initialized
[   11.756447] Bluetooth: RFCOMM socket layer initialized
[   11.756453] Bluetooth: RFCOMM ver 1.11
[   17.890025] thunderbolt 0000:04:00.0: stopping RX ring 0
[   17.890032] thunderbolt 0000:04:00.0: disabling interrupt at register 0x38200 bit 12 (0x1001 -> 0x1)
[   17.890039] thunderbolt 0000:04:00.0: stopping TX ring 0
[   17.890044] thunderbolt 0000:04:00.0: disabling interrupt at register 0x38200 bit 0 (0x1 -> 0x0)
[   17.890048] thunderbolt 0000:04:00.0: control channel stopped
[   39.148730] thunderbolt 0000:04:00.0: control channel starting...
[   39.148734] thunderbolt 0000:04:00.0: starting TX ring 0
[   39.148743] thunderbolt 0000:04:00.0: enabling interrupt at register 0x38200 bit 0 (0x0 -> 0x1)
[   39.148746] thunderbolt 0000:04:00.0: starting RX ring 0
[   39.148755] thunderbolt 0000:04:00.0: enabling interrupt at register 0x38200 bit 12 (0x1 -> 0x1001)
[   49.223496] usb 1-10: USB disconnect, device number 5
[   50.668468] usb 1-10: new full-speed USB device number 6 using xhci_hcd
[   50.817701] usb 1-10: New USB device found, idVendor=8087, idProduct=0aaa, bcdDevice= 0.02
[   50.817708] usb 1-10: New USB device strings: Mfr=0, Product=0, SerialNumber=0
[   50.820546] Bluetooth: hci0: Bootloader revision 0.1 build 42 week 52 2015
[   50.821588] Bluetooth: hci0: Device revision is 2
[   50.821592] Bluetooth: hci0: Secure boot is enabled
[   50.821595] Bluetooth: hci0: OTP lock is enabled
[   50.821597] Bluetooth: hci0: API lock is enabled
[   50.821600] Bluetooth: hci0: Debug lock is disabled
[   50.821604] Bluetooth: hci0: Minimum firmware build 1 week 10 2014
[   50.822242] Bluetooth: hci0: Found device firmware: intel/ibt-17-16-1.sfi
[   51.127550] usb usb1-port10: disabled by hub (EMI?), re-enabling...
[   51.127575] usb 1-10: USB disconnect, device number 6
[   51.127724] xhci_hcd 0000:00:14.0: WARN Event TRB for slot 5 ep 4 with no TDs queued?
[   51.127725] xhci_hcd 0000:00:14.0: WARN Set TR Deq Ptr cmd failed due to incorrect slot or ep state.
[   53.152465] Bluetooth: hci0: command 0xfc09 tx timeout
[   61.152422] Bluetooth: hci0: Failed to send firmware data (-110)
[  781.625606] thunderbolt 0000:04:00.0: stopping RX ring 0
[  781.625618] thunderbolt 0000:04:00.0: disabling interrupt at register 0x38200 bit 12 (0x1001 -> 0x1)
[  781.625637] thunderbolt 0000:04:00.0: stopping TX ring 0
[  781.625645] thunderbolt 0000:04:00.0: disabling interrupt at register 0x38200 bit 0 (0x1 -> 0x0)
[  781.625655] thunderbolt 0000:04:00.0: control channel stopped
[  807.187356] e1000e: enp0s31f6 NIC Link is Down
[  807.232322] wlp0s20f3: deauthenticating from f4:ec:38:eb:d5:46 by local choice (Reason: 3=DEAUTH_LEAVING)
[  807.681169] thunderbolt 0000:04:00.0: control channel starting...
[  807.681176] thunderbolt 0000:04:00.0: starting TX ring 0
[  807.681189] thunderbolt 0000:04:00.0: enabling interrupt at register 0x38200 bit 0 (0x0 -> 0x1)
[  807.681193] thunderbolt 0000:04:00.0: starting RX ring 0
[  807.681205] thunderbolt 0000:04:00.0: enabling interrupt at register 0x38200 bit 12 (0x1 -> 0x1001)
[  807.740519] PM: suspend entry (deep)
[  807.740523] PM: Syncing filesystems ... done.
[  808.059021] Freezing user space processes ... (elapsed 0.003 seconds) done.
[  808.062224] OOM killer disabled.
[  808.062226] Freezing remaining freezable tasks ... (elapsed 0.001 seconds) done.
[  808.063740] Suspending console(s) (use no_console_suspend to debug)
[  808.170039] e1000e: EEE TX LPI TIMER: 00000011
[  808.529561] thunderbolt 0000:04:00.0: stopping RX ring 0
[  808.529780] thunderbolt 0000:04:00.0: disabling interrupt at register 0x38200 bit 12 (0x1001 -> 0x1)
[  808.529797] thunderbolt 0000:04:00.0: stopping TX ring 0
[  808.529807] thunderbolt 0000:04:00.0: disabling interrupt at register 0x38200 bit 0 (0x1 -> 0x0)
[  808.529815] thunderbolt 0000:04:00.0: control channel stopped
[  808.529972] ACPI: EC: interrupt blocked
[  808.569555] ACPI: Preparing to enter system sleep state S3
[  808.576660] ACPI: EC: event blocked
[  808.576660] ACPI: EC: EC stopped
[  808.576660] PM: Saving platform NVS memory
[  808.576677] Disabling non-boot CPUs ...
[  808.593910] smpboot: CPU 1 is now offline
[  808.618158] smpboot: CPU 2 is now offline
[  808.643181] smpboot: CPU 3 is now offline
[  808.665422] IRQ 146: no longer affine to CPU4
[  808.666453] smpboot: CPU 4 is now offline
[  808.689164] IRQ 120: no longer affine to CPU5
[  808.689200] IRQ 158: no longer affine to CPU5
[  808.689221] IRQ 162: no longer affine to CPU5
[  808.690244] smpboot: CPU 5 is now offline
[  808.713220] IRQ 121: no longer affine to CPU6
[  808.713226] IRQ 123: no longer affine to CPU6
[  808.713233] IRQ 125: no longer affine to CPU6
[  808.714290] smpboot: CPU 6 is now offline
[  808.737219] IRQ 124: no longer affine to CPU7
[  808.737251] IRQ 156: no longer affine to CPU7
[  808.737272] IRQ 157: no longer affine to CPU7
[  808.738442] smpboot: CPU 7 is now offline
[  808.743456] ACPI: Low-level resume complete
[  808.743557] ACPI: EC: EC started
[  808.743558] PM: Restoring platform NVS memory
[  808.744441] Enabling non-boot CPUs ...
[  808.744485] x86: Booting SMP configuration:
[  808.744487] smpboot: Booting Node 0 Processor 1 APIC 0x2
[  808.745123]  cache: parent cpu1 should not be sleeping
[  808.745338] CPU1 is up
[  808.745360] smpboot: Booting Node 0 Processor 2 APIC 0x4
[  808.745717]  cache: parent cpu2 should not be sleeping
[  808.745867] CPU2 is up
[  808.745889] smpboot: Booting Node 0 Processor 3 APIC 0x6
[  808.746247]  cache: parent cpu3 should not be sleeping
[  808.746390] CPU3 is up
[  808.746408] smpboot: Booting Node 0 Processor 4 APIC 0x1
[  808.746837]  cache: parent cpu4 should not be sleeping
[  808.747117] CPU4 is up
[  808.747139] smpboot: Booting Node 0 Processor 5 APIC 0x3
[  808.747508]  cache: parent cpu5 should not be sleeping
[  808.747665] CPU5 is up
[  808.747684] smpboot: Booting Node 0 Processor 6 APIC 0x5
[  808.748065]  cache: parent cpu6 should not be sleeping
[  808.748231] CPU6 is up
[  808.748249] smpboot: Booting Node 0 Processor 7 APIC 0x7
[  808.748619]  cache: parent cpu7 should not be sleeping
[  808.748794] CPU7 is up
[  808.754280] ACPI: Waking up from system sleep state S3
[  808.838570] ACPI: EC: interrupt unblocked
[  808.878471] thunderbolt 0000:04:00.0: control channel starting...
[  808.878474] thunderbolt 0000:04:00.0: starting TX ring 0
[  808.878484] thunderbolt 0000:04:00.0: enabling interrupt at register 0x38200 bit 0 (0x0 -> 0x1)
[  808.878491] thunderbolt 0000:04:00.0: starting RX ring 0
[  808.878501] thunderbolt 0000:04:00.0: enabling interrupt at register 0x38200 bit 12 (0x1 -> 0x1001)
[  808.878534] pciehp 0000:00:1c.4:pcie004: Slot(4): Link Up
[  808.884211] ACPI: EC: event unblocked
[  808.886150] iwlwifi 0000:00:14.3: RF_KILL bit toggled to enable radio.
[  808.894069] ACPI: button: The lid device is not compliant to SW_LID.
[  809.122152] usb 1-8: reset high-speed USB device number 3 using xhci_hcd
[  809.398745] usb 1-1: reset full-speed USB device number 2 using xhci_hcd
[  809.674801] usb 1-9: reset full-speed USB device number 4 using xhci_hcd
[  809.834264] acpi LNXPOWER:06: Turning OFF
[  809.838700] OOM killer enabled.
[  809.838702] Restarting tasks ... done.
[  809.844954] pcieport 0000:00:1c.4: PCI bridge to [bus 02-3a]
[  809.844956] pcieport 0000:00:1c.4:   bridge window [io  0x4000-0x4fff]
[  809.844959] pcieport 0000:00:1c.4:   bridge window [mem 0xb4000000-0xca0fffff]
[  809.844962] pcieport 0000:00:1c.4:   bridge window [mem 0x90000000-0xb1ffffff 64bit pref]
[  809.858733] thermal thermal_zone6: failed to read out thermal zone (-61)
[  809.982684] PM: suspend exit
[  809.988926] IPv6: ADDRCONF(NETDEV_UP): enp0s31f6: link is not ready
[  810.178506] IPv6: ADDRCONF(NETDEV_UP): enp0s31f6: link is not ready
[  810.180516] IPv6: ADDRCONF(NETDEV_UP): wlp0s20f3: link is not ready
[  810.378637] IPv6: ADDRCONF(NETDEV_UP): wlp0s20f3: link is not ready
[  810.432819] IPv6: ADDRCONF(NETDEV_UP): wlp0s20f3: link is not ready
[  813.735242] wlp0s20f3: authenticate with f4:ec:38:eb:d5:46
[  813.737990] wlp0s20f3: send auth to f4:ec:38:eb:d5:46 (try 1/3)
[  813.779813] wlp0s20f3: authenticated
[  813.781782] wlp0s20f3: associate with f4:ec:38:eb:d5:46 (try 1/3)
[  813.785777] wlp0s20f3: RX AssocResp from f4:ec:38:eb:d5:46 (capab=0x31 status=0 aid=3)
[  813.800836] wlp0s20f3: associated
[  813.809804] IPv6: ADDRCONF(NETDEV_CHANGE): wlp0s20f3: link becomes ready
[  818.426759] psmouse serio1: Touchpad at isa0060/serio1/input0 lost sync at byte 6
[  818.481203] psmouse serio1: Touchpad at isa0060/serio1/input0 lost sync at byte 6
[  818.495962] psmouse serio1: Touchpad at isa0060/serio1/input0 lost sync at byte 6
[  818.510539] psmouse serio1: Touchpad at isa0060/serio1/input0 lost sync at byte 6
[  818.524291] psmouse serio1: Touchpad at isa0060/serio1/input0 lost sync at byte 6
[  818.524299] psmouse serio1: issuing reconnect request
[  822.755705] thunderbolt 0000:04:00.0: stopping RX ring 0
[  822.755720] thunderbolt 0000:04:00.0: disabling interrupt at register 0x38200 bit 12 (0x1001 -> 0x1)
[  822.755741] thunderbolt 0000:04:00.0: stopping TX ring 0
[  822.755754] thunderbolt 0000:04:00.0: disabling interrupt at register 0x38200 bit 0 (0x1 -> 0x0)
[  822.755766] thunderbolt 0000:04:00.0: control channel stopped
[  837.145938] thunderbolt 0000:04:00.0: control channel starting...
[  837.145945] thunderbolt 0000:04:00.0: starting TX ring 0
[  837.145959] thunderbolt 0000:04:00.0: enabling interrupt at register 0x38200 bit 0 (0x0 -> 0x1)
[  837.145963] thunderbolt 0000:04:00.0: starting RX ring 0
[  837.145975] thunderbolt 0000:04:00.0: enabling interrupt at register 0x38200 bit 12 (0x1 -> 0x1001)
[  837.791296] e1000e: enp0s31f6 NIC Link is Down
[  837.896794] wlp0s20f3: deauthenticating from f4:ec:38:eb:d5:46 by local choice (Reason: 3=DEAUTH_LEAVING)
[  837.974187] PM: suspend entry (deep)
[  837.974188] PM: Syncing filesystems ... done.
[  837.989062] Freezing user space processes ... (elapsed 0.005 seconds) done.
[  837.994106] OOM killer disabled.
[  837.994107] Freezing remaining freezable tasks ... (elapsed 0.001 seconds) done.
[  837.995687] Suspending console(s) (use no_console_suspend to debug)
[  838.101807] e1000e: EEE TX LPI TIMER: 00000011
[  838.446906] thunderbolt 0000:04:00.0: stopping RX ring 0
[  838.447106] ACPI: EC: interrupt blocked
[  838.447117] thunderbolt 0000:04:00.0: disabling interrupt at register 0x38200 bit 12 (0x1001 -> 0x1)
[  838.447151] thunderbolt 0000:04:00.0: stopping TX ring 0
[  838.447167] thunderbolt 0000:04:00.0: disabling interrupt at register 0x38200 bit 0 (0x1 -> 0x0)
[  838.447228] thunderbolt 0000:04:00.0: control channel stopped
[  838.486362] ACPI: Preparing to enter system sleep state S3
[  838.493513] ACPI: EC: event blocked
[  838.493513] ACPI: EC: EC stopped
[  838.493514] PM: Saving platform NVS memory
[  838.493531] Disabling non-boot CPUs ...
[  838.511189] smpboot: CPU 1 is now offline
[  838.534290] irq_migrate_all_off_this_cpu: 5 callbacks suppressed
[  838.534293] IRQ 157: no longer affine to CPU2
[  838.535339] smpboot: CPU 2 is now offline
[  838.558252] IRQ 163: no longer affine to CPU3
[  838.559281] smpboot: CPU 3 is now offline
[  838.582307] IRQ 146: no longer affine to CPU4
[  838.582333] IRQ 161: no longer affine to CPU4
[  838.584219] smpboot: CPU 4 is now offline
[  838.605992] IRQ 156: no longer affine to CPU5
[  838.606017] IRQ 162: no longer affine to CPU5
[  838.607038] smpboot: CPU 5 is now offline
[  838.630028] IRQ 158: no longer affine to CPU6
[  838.630093] IRQ 164: no longer affine to CPU6
[  838.631115] smpboot: CPU 6 is now offline
[  838.654057] IRQ 160: no longer affine to CPU7
[  838.655149] smpboot: CPU 7 is now offline
[  838.659858] ACPI: Low-level resume complete
[  838.659959] ACPI: EC: EC started
[  838.659960] PM: Restoring platform NVS memory
[  838.660834] Enabling non-boot CPUs ...
[  838.660879] x86: Booting SMP configuration:
[  838.660880] smpboot: Booting Node 0 Processor 1 APIC 0x2
[  838.661524]  cache: parent cpu1 should not be sleeping
[  838.661738] CPU1 is up
[  838.661774] smpboot: Booting Node 0 Processor 2 APIC 0x4
[  838.662145]  cache: parent cpu2 should not be sleeping
[  838.662279] CPU2 is up
[  838.662310] smpboot: Booting Node 0 Processor 3 APIC 0x6
[  838.662784]  cache: parent cpu3 should not be sleeping
[  838.662928] CPU3 is up
[  838.662948] smpboot: Booting Node 0 Processor 4 APIC 0x1
[  838.663378]  cache: parent cpu4 should not be sleeping
[  838.663657] CPU4 is up
[  838.663678] smpboot: Booting Node 0 Processor 5 APIC 0x3
[  838.664061]  cache: parent cpu5 should not be sleeping
[  838.664216] CPU5 is up
[  838.664235] smpboot: Booting Node 0 Processor 6 APIC 0x5
[  838.664615]  cache: parent cpu6 should not be sleeping
[  838.664782] CPU6 is up
[  838.664800] smpboot: Booting Node 0 Processor 7 APIC 0x7
[  838.665185]  cache: parent cpu7 should not be sleeping
[  838.665361] CPU7 is up
[  838.670830] ACPI: Waking up from system sleep state S3
[  838.755194] ACPI: EC: interrupt unblocked
[  838.795141] thunderbolt 0000:04:00.0: control channel starting...
[  838.795145] thunderbolt 0000:04:00.0: starting TX ring 0
[  838.795155] thunderbolt 0000:04:00.0: enabling interrupt at register 0x38200 bit 0 (0x0 -> 0x1)
[  838.795158] thunderbolt 0000:04:00.0: starting RX ring 0
[  838.795168] thunderbolt 0000:04:00.0: enabling interrupt at register 0x38200 bit 12 (0x1 -> 0x1001)
[  838.795193] pciehp 0000:00:1c.4:pcie004: Slot(4): Link Up
[  838.800875] ACPI: EC: event unblocked
[  838.802696] iwlwifi 0000:00:14.3: RF_KILL bit toggled to enable radio.
[  839.042763] usb 1-8: reset high-speed USB device number 3 using xhci_hcd
[  839.318837] usb 1-9: reset full-speed USB device number 4 using xhci_hcd
[  839.594825] usb 1-1: reset full-speed USB device number 2 using xhci_hcd
[  839.762556] acpi LNXPOWER:06: Turning OFF
[  839.766770] OOM killer enabled.
[  839.766772] Restarting tasks ... done.
[  839.777368] pcieport 0000:00:1c.4: PCI bridge to [bus 02-3a]
[  839.777373] pcieport 0000:00:1c.4:   bridge window [io  0x4000-0x4fff]
[  839.777377] pcieport 0000:00:1c.4:   bridge window [mem 0xb4000000-0xca0fffff]
[  839.777379] pcieport 0000:00:1c.4:   bridge window [mem 0x90000000-0xb1ffffff 64bit pref]
[  839.788610] thermal thermal_zone6: failed to read out thermal zone (-61)
[  839.916610] PM: suspend exit
[  839.922186] IPv6: ADDRCONF(NETDEV_UP): enp0s31f6: link is not ready
[  840.111089] IPv6: ADDRCONF(NETDEV_UP): enp0s31f6: link is not ready
[  840.112955] IPv6: ADDRCONF(NETDEV_UP): wlp0s20f3: link is not ready
[  840.309970] IPv6: ADDRCONF(NETDEV_UP): wlp0s20f3: link is not ready
[  840.384560] IPv6: ADDRCONF(NETDEV_UP): wlp0s20f3: link is not ready
[  841.170422] psmouse serio1: Touchpad at isa0060/serio1/input0 lost sync at byte 6
[  841.204414] psmouse serio1: Touchpad at isa0060/serio1/input0 lost sync at byte 6
[  843.683681] wlp0s20f3: authenticate with f4:ec:38:eb:d5:46
[  843.689533] wlp0s20f3: send auth to f4:ec:38:eb:d5:46 (try 1/3)
[  843.734537] wlp0s20f3: authenticated
[  843.738587] wlp0s20f3: associate with f4:ec:38:eb:d5:46 (try 1/3)
[  843.742652] wlp0s20f3: RX AssocResp from f4:ec:38:eb:d5:46 (capab=0x31 status=0 aid=3)
[  843.748083] wlp0s20f3: associated
[  843.757642] iwlwifi 0000:00:14.3: Unhandled alg: 0x707
[  843.774367] IPv6: ADDRCONF(NETDEV_CHANGE): wlp0s20f3: link becomes ready
[  845.934130] psmouse serio1: Touchpad at isa0060/serio1/input0 lost sync at byte 6
[  845.995956] psmouse serio1: Touchpad at isa0060/serio1/input0 lost sync at byte 6
[  846.022454] psmouse serio1: Touchpad at isa0060/serio1/input0 lost sync at byte 6
[  846.022462] psmouse serio1: issuing reconnect request
```
