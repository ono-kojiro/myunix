
#BOOTBLOCK = /home/kojiro/devel/xv6-x64/out/bootblock
BOOTBLOCK = ../bootblock/bootblock

# kernel : NG
KERNEL    = ../kernel/kernel.elf
#KERNEL    = /home/kojiro/devel/xv6-x64/out/kernel.elf

FS        = ../usr/fs.img
#FS        = /home/kojiro/devel/xv6-x64/fs.img

IMAGE = xv6.img
QEMU = /usr/bin/qemu-system-i386

all : image

image : $(IMAGE)

$(IMAGE) :
	rm -f $(IMAGE)
	dd if=/dev/zero    of=$(IMAGE) count=10000
	dd if=$(BOOTBLOCK) of=$(IMAGE) conv=notrunc
	dd if=$(KERNEL)    of=$(IMAGE) seek=1 conv=notrunc

qemu :
	$(QEMU) -nographic -serial mon:stdio \
		-drive file=$(FS),index=1,media=disk,format=raw \
		-drive file=$(IMAGE),index=0,media=disk,format=raw \
		-smp 2 -m 512

clean :
	rm -f $(IMAGE)

