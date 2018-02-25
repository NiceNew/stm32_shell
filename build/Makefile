CC:=arm-none-eabi-gcc
ASM:=arm-none-eabi-as
LD:=arm-none-eabi-ld
OBJCOPY:=arm-none-eabi-objcopy

INCLUDES:=-I. -I../src/includes
CFLAG:=--specs=nosys.specs -mcpu=cortex-m3
ASFLAG:=-mcpu=cortex-m3

DIR_SRC:=../src
DIR_OBJ:=.

SRC_C:=$(wildcard $(DIR_SRC)/*.c)
SRC_C+=$(wildcard $(DIR_SRC)/boot/*.c)
SRC_C+=$(wildcard $(DIR_SRC)/sys/*.c)
SRC_C+=$(wildcard $(DIR_SRC)/prph/*.c)
SRC_S:=$(wildcard $(DIR_SRC)/boot/*.s)

OBJ_O:=$(patsubst %.c,%.o,$(SRC_C))
OBJ_O+=$(patsubst %.s,%.o,$(SRC_S))

.PHONY:all clean
all:$(OBJ_O)
	$(LD) -T stm32f10x_flash.ld -o start.elf ./*.o
	$(OBJCOPY) start.elf -Oihex start.hex
%.o:%.c
	$(CC) $(INCLUDES) $(CFLAG) -c $< -o $(DIR_OBJ)/$(notdir $@)
%.o:%.s
	$(ASM) $(ASFLAG) -c $< -o $(DIR_OBJ)/$(notdir $@)
clean:
	rm *.o
	rm *.elf
	rm *.hex