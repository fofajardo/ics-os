![Alt Text](./ics-os.gif)

## About

Modern real-world operating systems are too complex to be taught to undergraduates and other instructional operating systems are not complete and usable and do not work on real hardware. By providing students with a _not so complex_ working operating system to play with, they will be able to appreciate and understand deeper the concepts underlying an operating system.

Thus, this project aims to develop a simple yet operational instructional operating system for teaching undergraduate operating systems courses. ICS-OS is a fork of <a href='http://sourceforge.net/projects/dex-os'>DEX-OS</a> by Joseph Dayo.

## Downloads

Latest floppy image: [![CI badge](https://github.com/fofajardo/ics-os/actions/workflows/main.yml/badge.svg)](https://nightly.link/?url=https://github.com/fofajardo/ics-os/blob/master/.github/workflows/main.yml)

Test the floppy image in qemu.
```console
$ qemu-system-i386 -fda ics-os-floppy.img
```

## Prerequisites

### Docker

ICS-OS is a 32-bit operating system and requires a 32-bit build environment. You need to install
[docker](https://docs.docker.com/engine/install/ubuntu/) and [docker-compose](https://docs.docker.com/compose/install/)
to build the ICS-OS kernel and user applications.

Run the following command to enter the build environment:

`$docker-compose run ics-os-build`

or if you are using the docker-compose plugin:

`$docker compose run ics-os-build`

You will be dropped to a shell where you can perform the build. The ics-os folder is mapped inside the container. Thus,
you can perform the edits outside the container(in another terminal) and the changes will be reflected inside the build environment.

Alternatively, you can boot the floppy image directly using qemu.
```console
$ qemu-system-i386 -fda ics-os-floppy.img
```

See [Lab 01](https://github.com/srg-ics-uplb/ics-os/blob/master/labs/lab01/ICSOS_Lab01.pdf) for a more complete discussion of how to set up the build environment.

### Ubuntu 22.04 and above
```console
$ sudo apt-get update
$ sudo apt-get install -y build-essential nasm qemu-kvm tcc git gcc-multilib
```

### Arch Linux
```console
$ sudo pacman -Syu base-devel nasm qemu-full git
```

### Windows (WSL)
1. Install [WSL](https://learn.microsoft.com/en-us/windows/wsl/install).
2. Open a Linux/Ubuntu shell and run:
```console
$ sudo apt-get update
$ sudo apt-get install -y build-essential nasm qemu-kvm tcc git gcc-multilib
```

## Build instructions
Make the floppy image then boot.
```console
$ sudo make all
$ make run
```

## Development and Support
This project is used at the <a href='http://www.ics.uplb.edu.ph'>Institute of Computer Science</a>, <a href='http://www.uplb.edu.ph'>University of the Philippines Los Banos</a> for <a href='http://ics.uplb.edu.ph/courses/ugrad/cmsc/125'>CMSC 125</a>. It is maintained by the <a href='https://sites.google.com/up.edu.ph/systems-research'>Systems Research Group</a>.

Get started by reading the <a href="https://github.com/srg-ics-uplb/ics-os/wiki/Kernel-Developer's-Guide">Kernel Developer's Guide</a>.

Don't forget to check the <a href="http://github.com/srg-ics-uplb/ics-os/wiki">Wiki</a>.

You can ask questions by submitting an issue.

## Citation

If you find his resource useful in your research or teaching, please cite our [paper](https://jachermocilla.org/publications/hermocilla-pitj2009-ics-os.pdf).

---

J. A. C. Hermocilla. Ics-os: A kernel programming approach to teaching operating system concepts. Philippine Information Technology Journal, 2(2):25--30, 2009.

---

You can also use the following bibtex entry.

```
@article{hermocilla-ics-os-pitj2009,
  author = {Hermocilla, J. A. C.},
  title = {ICS-OS: A Kernel Programming Approach to Teaching Operating System Concepts},
  journal = {Philippine Information Technology Journal},
  volume = {2},
  number = {2},
  year = {2009},
  issn = {2012-0761},
  pages = {25--30},
  publisher = {Philippine Society of Information Technology Educators and Computing Society of the Philippines },
  address = {Philippines},
  pdf = {https://jachermocilla.org/publications/hermocilla-pitj2009-ics-os.pdf}
}
```
