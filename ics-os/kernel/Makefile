CC=gcc
CFLAGS=-fno-stack-protector -fgnu89-inline -m32 -w -nostdlib -fno-builtin -ffreestanding -c -g -Wno-incompatible-pointer-types -Wno-implicit-function-declaration -Wno-int-conversion -Wno-return-mismatch -Wno-implicit-int
ASM=nasm
ASMFLAGS=-f elf32
OBJDIR=obj-i386
BIN_KERNEL=$(OBJDIR)/kernel32.bin

bzImage: all
	objcopy --only-keep-debug $(BIN_KERNEL) $(OBJDIR)/kernel32.sym
	objcopy --strip-debug $(BIN_KERNEL)
	gzip -c -9 $(BIN_KERNEL) > $(OBJDIR)/vmdex
	cp $(OBJDIR)/vmdex ..

all: obj kernel32.bin

objdir:
	mkdir $(OBJDIR)

obj: objdir scheduler.o fat.o iso9660.o devfs.o iomgr.o devmgr_error.o kernel32.o \
		startup.o asmlib.o irqwrap.o
	#strip --strip-debug *.o

kernel32.o: kernel32.c build.h
	$(CC) $(CFLAGS) -o $(OBJDIR)/kernel32.o kernel32.c

scheduler.o:
	$(CC) $(CFLAGS) -o $(OBJDIR)/scheduler.o process/scheduler.c

fat.o:
	$(CC) $(CFLAGS) -o $(OBJDIR)/fat.o filesystem/fat12.c

iso9660.o:
	$(CC) $(CFLAGS) -o $(OBJDIR)/iso9660.o filesystem/iso9660.c

devfs.o:
	$(CC) $(CFLAGS) -o $(OBJDIR)/devfs.o filesystem/devfs.c

iomgr.o:
	$(CC) $(CFLAGS) -o $(OBJDIR)/iomgr.o iomgr/iosched.c

devmgr_error.o:
	$(CC) $(CFLAGS) -o $(OBJDIR)/devmgr_error.o devmgr/devmgr_error.c

startup.o:
	$(ASM) $(ASMFLAGS) -o $(OBJDIR)/startup.o startup/startup.asm

asmlib.o:
	$(ASM) $(ASMFLAGS) -o $(OBJDIR)/asmlib.o startup/asmlib.asm

irqwrap.o:
	$(ASM) $(ASMFLAGS) -o $(OBJDIR)/irqwrap.o irqwrap.asm

kernel32.bin:
	ld -melf_i386 -L=$(OBJDIR) -T lscript.ld -o $(BIN_KERNEL) -Map $(OBJDIR)/mapfile.txt

clean:
	rm -rf $(OBJDIR)
