# Optimization

    Good programs
7zip
https://www.7-zip.org/a/7z1900-x64.exe

Firefox or Brave is a good privacy browser option

VLC
https://www.mediafire.com/file/6nu3it9ihpvn35s/VLC.rar/file

Visual C++ All-In-One
https://www.mediafire.com/file/vs72423ov28j44s/Visual_C++_v56.exe/file

    BEFORE FORMATTING

**Backup & Unplug Internet Before formatting**, make sure you backup important files

- [ ] Music

- [ ] Pictures

- [ ] Videos

- [ ] Documents

- [ ] Any kind of Configs

Once you’ve backed up everything you can think of, you can unplug your internet cable and begin the install

    FRESH INSTALL
- [ ] Turn off UAC

- [ ] Change Mouse Settings (6/11, EPP off, cursor)

- [ ] Disable Indexing

Right click Local Disk (C:)

Untick "Allow files on this drive to have contents indexed in addition to file properties"

- [ ] DDU
Run DDU, reboot to safe mode - clean uninstall all drivers. Audio & GPU

- [ ] Disable Windows Updates

Go to gpedit.msc

Computer Configuration\Administrative Templates\Windows Components\Windows Update

Configure automatic updates - disabled

Specify intranet microsoft update service location - enabled

Enter this link into all three boxes on the left
http:\\neverupdatewindows10.com

Remove access to use all windows update features - enabled

Do not connect to any windows update internet locations - enabled

Do not include drivers with windows updates - enabled

Restart Computer, it’s now safe to plug in your internet cable/connect to wifi

- [ ] Install DirectX

- [ ] Install .NET Framework 3.5 (required for some things to work)

Insert your USB stick with Win10 on it

Run CMD as administrator

Dism /online /enable-feature /featurename:NetFx3 /All /Source:E:\sources\sxs /LimitAccess

Change “/Source:E” to match your USB letter


    GPEDIT

- [ ] gpedit.msc

Computer Configuration\Administrative Templates\System\Group Policy\

Continue experiences on this device - disable

Computer Configuration\Administrative Templates\Start Menu and Taskbar\Notifications\

Turn off notifications network usage - enabled

Computer Configuration\Administrative Templates\Windows Components\Windows Error Reporting

Disable windows error reporting - enabled

Computer Configuration\Administrative Templates\Windows Components\Data Collection

Allow telemetry - disabled

User Configuration\Administrative Templates\Windows Components\Data Collection

Allow telemetry - disabled

User Configuration\Administrative Templates\Start Menu And Taskbar\Notifications

Turn off notifications network usage - enabled

    DRIVERS

- [ ] Get a stripped nvidia driver

- [ ] Snappy Driver Installer

Download Snappy Driver Installer Origin

Download indexes only

Do not install chipset drivers

Update SATA/USB/PCI drivers

    WINAERO TWEAKER
- [ ] Download WinAero Tweaker

Install the Portable version, extract to your desktop. Import this XML file

    FEATURES & SERVICES
- [ ] Windows Features

Turn all Windows features off except for

.NET 3.5

.NET 4.7

- [ ] Disable Services

Run the Disable Services.bat file with Nsudo - TrustedInstaller & All Privileges

It’s technically better to do services manually, so if you have the patience for that it’s better. But I find the script works just fine.

    My Personal Services (1809)

With these, your task scheduler won’t work. Put shortcuts of your programs you want starting up with your computer into this folder
Run - shell:startup

![Services](https://i.imgur.com/qkZJpD4.png)

Services Info

**Windows Event Log** - fast taskbar right click menus

**Capability Access Manager Service** - needed in 1803 or higher or microphone won’t work in Discord/ts

**State Repository Service** - needed or my taskbar breaks personally, you can test it for yourself

**Device Setup Service** - needed for when you switch mice/keyboards/webcams, etc.

**WLAN AutoConfig** - WIFI

**Network List Service** - WIFI

**Network Location Awareness** - WIFI

**Windows Event Log** - WIFI

    GPU

- [ ] Nvidia Inspector
Run Nvidia Inspector as administrator and import the preset that’s included

- [ ] GPU Overclock
Install & Run MSI Afterburner
Overclock your GPU
You can also use KBoost, but personally it raised my temperatures too much. Definitely do use if you have good cooling

- [ ] PowerMizer

Download and run NVPMManager

Create PowerMizer settings

Enable PowerMizer feature

Fixed Performance Level - “Max. Perf/Min PowerSave” on both boxes

![What it should look like](https://i.imgur.com/YHeKiaR.png)

    DEVICE MANAGER

- [ ] Device Manager

**Turn off power saving features for**:

Human Interface Devices

USB Input Device (all)

Keyboards

HID Keyboard Device (all)

Universal Serial Bus controllers

USB Root Hubs

**Disable the following**:

Audio inputs and outputs
- Speakers (Realtek HD Audio) - Your headphones should still work, mine do

Human Interface Devices
- HID-compliant consumer control device (all)
- HID-compliant system controller
- HID-compliant vendor-defined device (all)
- Unused USB ports (USB Input Device)

Keyboards
- Standard PS/2 Keyboard

Mice
- Microsoft PS/2 Mouse

Monitors
- Generic PnP Monitor - This is safe to turn off, nothing will happen

Ports
- Communications Port (COM1)
- Printer Port (LPT1)

Software Devices
- Microsoft GS Wavetable Synth
Network adapters
- All WAN miniports

Other devices
- PCI Simple Communications Controller
Sound, video games, and controllers
- Unused audio devices

System devices
- Composite Bus Enumerator
- HD Audio Controller (one is real, one is nvidia, test audio to see if you disabled the correct one)
- High precision event timer
- Microsoft System Management BIOS Driver
- Microsoft Virtual Driver Enumerator
- NDIS Virtual Network ADapter Enumerator
- Numeric data processor
- Unused PCI-to-PCI Bridge - use “Devices > View by Connection” to see which PCI bridges aren’t used
- Programmable interrupt controller
- Remote Desktop Device Redirector Bus
- System Timer
- UMBus Root Bus Enumerator

Show Hidden Devices
Uninstall every transparent device

- [ ] Hard Drive Tweaks

Open device manager

Disk drives

Select all drives individually

Right click -> Properties -> Policies

Enable write caching on this device - on

Turn off windows write-cache buffer flushing on the device - on

    CPU
- [ ] Windows Timer Resolution

Download Intelligent standby list cleaner, extract it and run the exe

Set “Wanted Timer Resolution” to 0.50

Set “The list size is at least:” to 1024mb

Set “Free memory is lower than:” to half your RAM in mb (4096 if you have 8gb, 8192 if you have 16gb)

To achieve the “0.50” you must disable windows’ synthetic HPET and enable HPET in BIOS

Cmd as administrator (these are also included in the scripts file below)

bcdedit /set useplatformclock no

bcdedit /set useplatformtick yes

- [ ] Processor Scheduling

![](https://i.imgur.com/avxxh16.png)

Long/Short Quantum:
How long the CPU will spend on that specific task.

Short Quantum = More responsive inputs at the expense of smoothness.

Long Quantum = Smoother games at the expense of input response.

Fixed/Variable Quantum

If you select variable, you can select a boost. The higher the boost, the smoother the game, but less responsive inputs. If you select fixed, you can’t select a boost.

Testing to see which is best:

There is no restart required so you can leave regedit open and keep trying different values while having your game open.

Open regedit and go to:
HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\PriorityControl

Add together the decimal values you want and enter that as a decimal to the Win32PrioritySeparation key.

Example: 32 (Short) + 4 (Variable) + 2 (High) = 38

Decimal 40 theoretically provides the most responsive input.

Decimal 22 theoretically provides the smoothest gameplay.

Possible options: decimal 21, 22, 24, 37, 38, 40

decimal 38 works best for most people, including me.

- [ ] Power

powercfg -import C:\optimizedpower.pow

You can set “Process idle disable” to disabled for slightly lower latency, but this will stress your CPU so it isn’t worth using unless you have good cooling. For me it raised my idle temps from 35-40c to 50-55c

Delete all other power plans in powershell

powercfg /list

powercfg -delete Power Scheme GUID

- [ ] Unpark Cores
Download UnparkCpu.exe and run it, unpark your cores

- [ ] Affinity

Install Interrupt Affinity Tool

Open it at "C:\Program Files (x86)\Microsoft Corporation\Interrupt Affinity Policy Tool"

Run "intPolicy_x64" as administrator

Here is a list of things that are safe:

**GPU** - Set the PCIe controller that the GPU is connected to onto the same core

Use a benchmarkable program with very high FPS to test which core is best for the GPU

**USB controllers and USB hubs** - Use MouseTester to see which core is best

**PCIe Controllers** - you should set the PCIe controller onto the same cores that you set its devices as

PCI Standard ISA Bridge

LPC Controller

Make sure the PCI bridge that is connected to the device that was moved is also moved to the same core as the device

Device Manager > View (Devices by Connection)

Scroll down to PCI bridges

Right click the PCI bridge that's connected to a usb hub or the gpu
Copy it's location

Under the affinity tool, search the PCI bridges until the one with the same location comes up

Personal best results: USB Hubs/PCI Core #4

    SCRIPTS
- [ ] Run scripts

CMD Files (as administrator) 

Reg Files

- [ ] ESEA fix

Run CMD as admin - bcdedit /deletevalue nx (turns DEP back on)

    MSI MODE & IRQ SHARING

- [ ] Run MSI_Mode.exe (as administrator)

Do not enable MSI mode for USB2 or SATA controller driver. You’ll brick your windows

If you put a device into MSI mode, also put the connected PCI-to-PCI bridge

NVIDIA GeForce GTX 970 - Enabled, High

PCI standard ISA bridge - Enabled, High

PCIe/PCI-to-PCI bridge - Enabled, High

Intel Ethernet I219-V - Enabled, High

USB 3.1 Host Controller - Enabled, High

HD Audio Controller - Enabled, Undefined

- [ ] IRQ Sharing

If devices are sharing IRQs (interrupt request lines), they will interfere with each other and increase latency.

To see which devices are sharing IRQs, go to device manager > resources by connection > IRQs

MSI_Mode.exe also shows shared IRQs on the [IRQ] column.

How to solve shared IRQs

IRQ 16 is repeated five times, or five devices share one IRQ. This will have a profound effect on latency, and as a result, smoothness. Let’s take a look at how to fix this. 

The Intel Management Driver should be disabled as it is meant for corporate computers, not home computers. Next, the GTX 680 should be put in MSI mode, as well as the PCI standard PCI-to-PCI bridges. That’s all this user has to do.

![](https://i.imgur.com/jmxhsy0.png)

    AUTO RUNS
- [ ] Autoruns

Run Autoruns as administrator

Scheduled Tasks - untick all auto updates

KnownDLLs - delete all, untick the ones you can't delete

Services - take off auto updates

Useful program to see if something newly installed has an autorun or not

    NETWORKING

- [ ] Internet Tweaks

Device manager

Network adapter

Power management

Allow the computer to turn off this device to save power - off

Allow this device to wake the computer - off

    Network Adapter Tweaks (recommended)

Energy Efficient Ethernet - OFF

Interrupt Moderation/Rate - OFF

Receive/Transmit Buffers - MAX

TCP Offloads - OFF

Ultra-Low Power Mode - OFF

Advanced Internet Tweaks (not recommended for now, neither is TCPOptimizer)

    STEAM
- [ ] No Browser

Add “-no-browser” to the Steam shortcut’s target

- [ ] Old Library

Download Old Steam Library UI

Exit steam completely

Go to “C:\Program Files (x86)\Steam”, drag in the files from the download & replace

    CSGO SPECIFICS
- [ ] Launch Options (anything other than these are placebo or will hurt your game instead of help)

-novid -nojoy -no-browser -d3d9ex -tickrate 128 -console

- [ ] Disable Fullscreen Optimizations
Make sure you change settings for all users!
