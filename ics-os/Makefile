# ics-os Makefile
#
# written by Joseph Anthony C. Hermocilla
#

SND_BACKEND = pa
SND_DEVID = snd0
IMG_FDA = ics-os-floppy.img

vmdex:
	make -C kernel/

.PHONY: clean
clean:
	rm -f vmdex
	rm -f ics-os-livecd.iso
	rm -fr tmp/*
	make -C kernel/ clean

update_kernel_only: vmdex
	sudo rm -fr mnt
	sudo mkdir mnt
	sudo mount $(IMG_FDA) mnt -tmsdos -oloop
	sudo cp -r vmdex mnt
	sudo umount mnt
	sudo chmod 666 $(IMG_FDA)

prep_image: vmdex
	rm -fr tmp
	mkdir tmp
	cp -r vmdex tmp
	scripts/gen-help.sh
	cp  base/* tmp
	mkdir -p tmp/apps
	mkdir -p tmp/tcc1
	mkdir -p tmp/lib1
	cp apps/* tmp/apps/
	cp sdk/* tmp/tcc1/
	cp lib/* tmp/lib1/

floppy: prep_image
	cp grub.img $(IMG_FDA)                #copy an image with grub
	sudo rm -fr mnt
	sudo mkdir mnt
	sudo mount $(IMG_FDA) mnt -tmsdos -oloop
	sudo cp -r tmp/* mnt/
	sudo umount mnt
	sudo chmod 666 $(IMG_FDA)
	rm -fr tmp/

livecd: prep_image
	mkdir -p tmp/boot/grub
	cp boot/grub/grub.cfg tmp/boot/grub/.
	grub-mkrescue -o ics-os-livecd.iso tmp/
	rm -fr tmp/

boot-floppy:
	qemu-system-i386 -net nic,model=rtl8139 \
			-audiodev $(SND_BACKEND),id=$(SND_DEVID) \
			-machine pcspk-audiodev=$(SND_DEVID) \
			-drive format=raw,file=$(IMG_FDA),index=0,if=floppy \
			-boot a -m 64M

boot-floppy-gdb:
	qemu-system-i386 -net nic,model=rtl8139 \
			-audiodev $(SND_BACKEND),id=$(SND_DEVID) \
			-machine pcspk-audiodev=$(SND_DEVID) \
			-drive format=raw,file=$(IMG_FDA),index=0,if=floppy \
			-boot a -m 64M -s -S

boot-floppy-vnc:
	qemu-system-i386 -net nic,model=rtl8139 \
			-audiodev $(SND_BACKEND),id=$(SND_DEVID) \
			-machine pcspk-audiodev=$(SND_DEVID) \
			-drive format=raw,file=$(IMG_FDA),index=0,if=floppy \
			-boot a -m 64M -vnc :1

boot-debug:
	qemu-system-i386 -s -S -kernel "kernel/obj-i386/kernel32.bin" \
			-drive format=raw,file=$(IMG_FDA),index=0,if=floppy \
			-m 64M -append "root (hdp0p0)"

boot-livecd:
	qemu-system-i386 -cdrom ics-os-livecd.iso -boot cd -m 64M

all: clean floppy

run: boot-floppy
