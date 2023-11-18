TARGET = kernel.elf
OBJS = main.o

CXXFLAGS += -O2 -Wall -g --target=x86_64-elf -ffreestanding -mno-red-zone \
			-fno-exceptions -fno-rtti -std=c++17
LDFLAGS += --entry KernelMain -z norelro --image-base 0x100000 --static

.PHONY: all
all: $(TARGET)

.PHONY: clean
clean:
	rm -rf *.o

kernel.elf: $(OBJS) Makefile
	sudo ln -sf /usr/bin/ld.lld-7 /etc/alternatives/ld.lld
	ld.lld $(LDFLAGS) -o kernel.elf $(OBJS)
	sudo ln -sf /usr/bin/ld.lld-14 /etc/alternatives/ld.lld

%.o: %.cpp Makefile
	clang++ $(CPPFLAGS) $(CXXFLAGS) -c $<
