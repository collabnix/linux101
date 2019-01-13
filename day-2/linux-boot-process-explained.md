# Understanding Linux Boot Process


## BIOS (Basic Input-Output System)

BIOS is a pre-installed firmware on a system/server’s Mother board. BIOS controls the computer hardware. BIOS is used to perform hardware initialization during the booting process. The main job assigned to BIOS is POST (Power On Self Test). It’s a hardware self test. POST tests are simple read/write tests of a few location.

### Main responsibilities of BIOS during POST are listed below:

- Verify CPU registers.
- Verify the integrity of the BIOS code itself.
- Verify some basic components like DMA, timer, interrupt controller.
- Find, size, and verify system main memory.
- Initialize BIOS
- Identify, organize, and select which devices are available for booting.

The beep sound after the POST indicate its result. A short beep while restart/start means normal POST – system is OK. Two short beeps means POST error – error code shown on screen and so on. Check POST manual for more details.

BIOS act as an intermediary between computer CPU and Input/Output devices. This eliminates the need for the operating system and software on the system/server are always aware about the details of hardware and other I/O devices. If any harddisks or I/O devices changed, only the BIOS needs to be updated.

BIOS is stored in EEPROM (Electrically Erasable Programmable ROM) / Flash memory. BIOS can not stored on a  hard disk or other devices, because it manages those devices. BIOS is written in assembly language

Remember, POST, that is the main thing happen at BIOS stage of booting. Next we can move to 1st boot loader stage, MBR stage

## Master Boot Record - 1st Stage bootloader

Master Boot Record, is the first place where boot loaders begins to start. MBR is a 512 byte sector located in the first sector of hard disk. MBR contains both program code and partition table details. Please see the image added below:

When allocating disk space for a partition, the first sector or data unit for each partition is always reserved for programmable code used in booting process. The very first sector of the hard disk is reserved for same purpose and it’s called the Master Boot Record. In case of a mechanical spinning disk, sector 1 of cylinder 0, head 0.

## 2nd Stage BootLoader (GRUB)

It is called the kernel loader. The main task at this stage is to load the Linux kernel.
This bootloader is intelligent to boot up your desired kernel.

If you have Red Hat OS and Windows installed, GRUB provides you choice to boot your desired OS via loading the kernel.

## Kernel Stage

Kernel is the interface between Shell and Hardware. kernel talk to Hardware via Device driver.

Kernel is in compressed format. We can select the kernel from the GRUB menu. If not selected, the GRUB automatically load the default one in its configuration. We can change the default kernel details from the GRUB configuration.

Every OS distribution pick up kernel software via kernel.org website

## Init Phase

Init is the first process which gets started after kernel loading finishes.

The kernel, once it is loaded in step 4, it finds init in sbin (/sbin/init) and executes it. [In RHEL/CentOS 7 /sbin/init is linked to ../lib/systemd/systemd]. When init starts, it become the first or parent process on your Linux machine/server.

The first thing init does is reading the initialization file, /etc/inittab. This instructs init to read an initial configuration script for the environment, which sets the path, starts swapping, checks the file systems, and so on. From the /etc/inittab system will find the run level selected and start services by looking in the appropriate rc directory for that run level.

## Login Page

Under init, the login process entry is present and hence you see login windows






