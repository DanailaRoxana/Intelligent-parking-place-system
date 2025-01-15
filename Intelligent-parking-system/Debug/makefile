################################################################################
# Automatically-generated file. Do not edit!
################################################################################

-include ../makefile.init

RM := rm -rf

# All of the sources participating in the build are defined here
-include sources.mk
-include Startup/subdir.mk
-include Libraries/XMCLib/src/subdir.mk
-include Libraries/Newlib/subdir.mk
-include Dave/Generated/UART/subdir.mk
-include Dave/Generated/TIMER/subdir.mk
-include Dave/Generated/PWM/subdir.mk
-include Dave/Generated/INTERRUPT/subdir.mk
-include Dave/Generated/GLOBAL_CCU4/subdir.mk
-include Dave/Generated/FREERTOS/portable/Keil/subdir.mk
-include Dave/Generated/FREERTOS/portable/IAR/subdir.mk
-include Dave/Generated/FREERTOS/portable/GCC/subdir.mk
-include Dave/Generated/FREERTOS/subdir.mk
-include Dave/Generated/DIGITAL_IO/subdir.mk
-include Dave/Generated/CPU_CTRL_XMC1/subdir.mk
-include Dave/Generated/CLOCK_XMC1/subdir.mk
-include Dave/Generated/subdir.mk
-include subdir.mk
-include objects.mk

ifneq ($(MAKECMDGOALS),clean)
ifneq ($(strip $(S_DEPS)),)
-include $(S_DEPS)
endif
ifneq ($(strip $(S_UPPER_DEPS)),)
-include $(S_UPPER_DEPS)
endif
ifneq ($(strip $(C_DEPS)),)
-include $(C_DEPS)
endif
endif

-include ../makefile.defs

# Add inputs and outputs from these tool invocations to the build variables 
SECONDARY_FLASH += \
Intelligent-parking-system.hex \

SECONDARY_LIST += \
Intelligent-parking-system.lst \

SECONDARY_SIZE += \
Intelligent-parking-system.siz \


LIST_FILES = $(addsuffix .o.lst, $(basename $(OBJS))) 
MAP_FILE = "Intelligent-parking-system.map"

TOOLCHAIN_ROOT=C:/Infineon/Tools/DAVE IDE/4.5.0.202105191637/eclipse/ARM-GCC-49
PROJECT_LOC=C:/Users/danai/FisiereleMele/de mutat/uni/master/an1/sem1/sdtr/proiect/Intelligent-parking-place-system/Intelligent-parking-system

# All Target
all: Intelligent-parking-system.elf secondary-outputs

# Tool invocations
Intelligent-parking-system.elf: $(OBJS) ../linker_script.ld $(USER_OBJS)
	@echo 'Building target: $@'
	@echo 'Invoking: ARM-GCC C Linker'
	$(file >objects.rsp,$(OBJS))
	"$(TOOLCHAIN_ROOT)/bin/arm-none-eabi-gcc" -T"../linker_script.ld" -nostartfiles -Xlinker --gc-sections -specs=nano.specs -specs=nosys.specs -u _printf_float -Wl,-Map,$(MAP_FILE) -specs=rdimon.specs -mcpu=cortex-m0 -mthumb -g -gdwarf-2 -o "Intelligent-parking-system.elf" "@objects.rsp" $(USER_OBJS) $(LIBS)
	@echo 'Finished building target: $@'
	@echo.
Intelligent-parking-system.hex: Intelligent-parking-system.elf
	@echo 'Invoking: ARM-GCC Create Flash Image'
	"$(TOOLCHAIN_ROOT)/bin/arm-none-eabi-objcopy" -O ihex "Intelligent-parking-system.elf" "Intelligent-parking-system.hex"
	@echo 'Finished building: $@'
	@echo.
Intelligent-parking-system.lst: Intelligent-parking-system.elf
	@echo 'Invoking: ARM-GCC Create Listing'
	"$(TOOLCHAIN_ROOT)/bin/arm-none-eabi-objdump" -h -S "Intelligent-parking-system.elf" > "Intelligent-parking-system.lst"
	@echo 'Finished building: $@'
	@echo.
Intelligent-parking-system.siz: Intelligent-parking-system.elf
	@echo 'Invoking: ARM-GCC Print Size'
	"$(TOOLCHAIN_ROOT)/bin/arm-none-eabi-size" --format=berkeley "Intelligent-parking-system.elf"
	@echo 'Finished building: $@'
	@echo.
# Other Targets
clean:
	-$(RM) $(SECONDARY_FLASH)$(SECONDARY_LIST)$(SECONDARY_SIZE)$(ARM_GCC_FOR_XMC_LINKER_OUTPUT_TYPE_OUTPUTS)$(S_DEPS)$(S_UPPER_DEPS)$(C_DEPS)
	-$(RM) Dave/Generated/CLOCK_XMC1/clock_xmc1.o Dave/Generated/CLOCK_XMC1/clock_xmc1_conf.o Dave/Generated/CPU_CTRL_XMC1/cpu_ctrl_xmc1.o Dave/Generated/CPU_CTRL_XMC1/cpu_ctrl_xmc1_conf.o Dave/Generated/DAVE.o Dave/Generated/DIGITAL_IO/digital_io.o Dave/Generated/DIGITAL_IO/digital_io_conf.o Dave/Generated/FREERTOS/croutine.o Dave/Generated/FREERTOS/event_groups.o Dave/Generated/FREERTOS/freertos.o Dave/Generated/FREERTOS/heap.o Dave/Generated/FREERTOS/list.o Dave/Generated/FREERTOS/mpu_wrappers.o Dave/Generated/FREERTOS/queue.o Dave/Generated/FREERTOS/stream_buffer.o Dave/Generated/FREERTOS/tasks.o Dave/Generated/FREERTOS/timers.o Dave/Generated/FREERTOS/portable/GCC/port.o Dave/Generated/FREERTOS/portable/IAR/port.o Dave/Generated/FREERTOS/portable/IAR/portasm.o Dave/Generated/FREERTOS/portable/Keil/port.o Dave/Generated/GLOBAL_CCU4/global_ccu4.o Dave/Generated/GLOBAL_CCU4/global_ccu4_conf.o Dave/Generated/INTERRUPT/interrupt.o Dave/Generated/INTERRUPT/interrupt_conf.o Dave/Generated/PWM/pwm.o Dave/Generated/PWM/pwm_conf.o Dave/Generated/TIMER/timer.o Dave/Generated/TIMER/timer_conf.o Dave/Generated/UART/uart.o Dave/Generated/UART/uart_conf.o Libraries/Newlib/syscalls.o Libraries/XMCLib/src/xmc1_eru.o Libraries/XMCLib/src/xmc1_flash.o Libraries/XMCLib/src/xmc1_gpio.o Libraries/XMCLib/src/xmc1_rtc.o Libraries/XMCLib/src/xmc1_scu.o Libraries/XMCLib/src/xmc_acmp.o Libraries/XMCLib/src/xmc_bccu.o Libraries/XMCLib/src/xmc_can.o Libraries/XMCLib/src/xmc_ccu4.o Libraries/XMCLib/src/xmc_ccu8.o Libraries/XMCLib/src/xmc_common.o Libraries/XMCLib/src/xmc_eru.o Libraries/XMCLib/src/xmc_gpio.o Libraries/XMCLib/src/xmc_i2c.o Libraries/XMCLib/src/xmc_i2s.o Libraries/XMCLib/src/xmc_ledts.o Libraries/XMCLib/src/xmc_math.o Libraries/XMCLib/src/xmc_pau.o Libraries/XMCLib/src/xmc_posif.o Libraries/XMCLib/src/xmc_prng.o Libraries/XMCLib/src/xmc_rtc.o Libraries/XMCLib/src/xmc_spi.o Libraries/XMCLib/src/xmc_uart.o 
	-$(RM) Libraries/XMCLib/src/xmc_usic.o Libraries/XMCLib/src/xmc_vadc.o Libraries/XMCLib/src/xmc_wdt.o Startup/startup_XMC1100.o Startup/system_XMC1100.o main.o  Intelligent-parking-system.elf $(LIST_FILES) $(MAP_FILE) objects.rsp
	-@echo.
secondary-outputs: $(SECONDARY_FLASH) $(SECONDARY_LIST) $(SECONDARY_SIZE)

.PHONY: all clean dependents
.SECONDARY:

-include ../makefile.targets
