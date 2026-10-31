# Peb

Fork of FreeBSD 15 kernel

Nothing to say for now.

## Compiling on Linux

Install the prerequisites:

**Fedora/RHEL/CentOS based (bzip requires CRB repo enabled on RHEL/CentOS)**

```shell
sudo dnf install git python3 gcc gcc-c++ libarchive-devel bzip2 xz clang lld
```

**Ubuntu/Debian based**

```shell
sudo apt install git python3 build-essential libarchive-dev libbz2-dev liblzma-dev clang lld
```

**Arch based**

```shell
sudo pacman -Syu git python gcc libarchive bzip2 xz clang lld
```

Then compile the toolchain:

```shell
MAKEOBJDIRPREFIX=/tmp/obj python3 tools/build/make.py -j$(nproc) kernel-toolchain TARGET=amd64 TARGET_ARCH=amd64 --bootstrap-toolchain
```

If the compilation fails because of OOM killer, change -j$(nproc) to eg. -j4:

```shell
MAKEOBJDIRPREFIX=/tmp/obj python3 tools/build/make.py -j4 kernel-toolchain TARGET=amd64 TARGET_ARCH=amd64 --bootstrap-toolchain
```

A successful toolchain compilation will return:

```
--------------------------------------------------------------
>>> Kernel toolchain for amd64 completed on Fri Oct 30 21:30:15 CET 2026
--------------------------------------------------------------
>>> Kernel toolchain built in 1342 seconds, ncpu: 4, make -j4
--------------------------------------------------------------
```

You can change amd64 for i386 too.

And then compile the kernel (if you copied the compiled toolchain from /tmp/obj, make sure to put the correct directory after MAKEOBJDIRPREFIX)  (if the OOM killer stops the compilation, change -j$(nproc) to eg. -j4):

```shell
MAKEOBJDIRPREFIX=/tmp/obj python3 tools/build/make.py -j$(nproc) buildkernel KERNCONF=PEBKERNEL TARGET=amd64 TARGET_ARCH=amd64 --bootstrap-toolchain
```

After the compilation, you should see something like this:

```
--------------------------------------------------------------
>>> Kernel build for PEBKERNEL completed on Fri Oct 30 21:36:51 CET 2026
--------------------------------------------------------------
>>> Kernel(s) PEBKERNEL built in 337 seconds, ncpu: 12, make -j12
--------------------------------------------------------------
```

## Compiling on FreeBSD

Open the source code tree in terminal and type:

```bash
make buildkernel KERNCONF=PEBKERNEL
```

Optionally you can install the kernel too after it compiles:

```bash
make installkernel KERNCONF=PEBKERNEL
```

## People that contributed to Peb

| Name                         | Role                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| Antoni Kundera (@pikus69420) | Main maintainer of the Peb kernel, founder of the Peb kernel |
