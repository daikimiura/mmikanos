SHELL=/bin/bash

TARGET = kernel.elf
OBJS = main.o

CXXFLAGS += -O2 -Wall -g --target=x86_64-elf -ffreestanding -mno-red-zone \
			-fno-exceptions -fno-rtti -std=c++17
LDFLAGS += --entry KernelMain -z norelro --image-base 0x100000 --static

.PHONY: run
run: $(TARGET)
	cd $(HOME)/edk2 && source edksetup.sh \
	&& $(HOME)/osbook/devenv/run_qemu.sh $(HOME)/edk2/Build/MikanLoaderX64/DEBUG_CLANG38/X64/Loader.efi /workspaces/mikanos-devcontainer/mmikanos/kernel/kernel.elf

.PHONY: all
all: $(TARGET)

.PHONY: clean
clean:
	rm -rf *.o

kernel.elf: $(OBJS) Makefile
	ld.lld $(LDFLAGS) -o kernel.elf $(OBJS)

%.o: %.cpp Makefile
	source $(HOME)/osbook/devenv/buildenv.sh && clang++ $(CPPFLAGS) $(CXXFLAGS) -c $<