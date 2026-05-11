# acMesure — STM32G030F6Px Firmware

Firmware for the M5Stack UNIT_ACMEASURE module (AC sensor HLW8032 + STM32G030F6Px).

This fork fix the issue that stopped the mesurements if the current was 0.
---

## Requirements

- **STM32CubeIDE 2.1.1**
- **ST-Link V2**
---

## Build

### 1. Open the project in CubeIDE

`File → Open Projects from File System` → select the `acMesure/` folder

### 2. Project configuration (if not already done)

**Preprocessor defines** (`Properties → C/C++ Build → Settings → MCU GCC Compiler → Preprocessor`):
```
STM32G030xx
USE_HAL_DRIVER
STM32G030F6Px
STM32
STM32G0
```

**Include paths**:
```
../Inc
../Drivers/STM32G0xx_HAL_Driver/Inc
../Drivers/STM32G0xx_HAL_Driver/Inc/Legacy
../Drivers/CMSIS/Device/ST/STM32G0xx/Include
../Drivers/CMSIS/Include
```

**Optimization**: `-Os` (Optimize for size)

### 3. Files to exclude from build

Right-click → Properties → C/C++ Build → check "Exclude resource from build" for:
- `HAL_Src/stm32g0xx_hal_timebase_rtc_alarm_template.c`
- `HAL_Src/stm32g0xx_hal_timebase_rtc_wakeup_template.c`
- `HAL_Src/stm32g0xx_hal_timebase_tim_template.c`
- `HAL_Src/stm32g0xx_hal_msp_template.c`
- All `HAL_Src/stm32g0xx_ll_*.c` files

### 4. Compile

`Ctrl+B` 
---

### Flash from CubeIDE

1. Wire yout stlink
2. `Run → Run Configurations → STM32 C/C++ Application → acMesure Debug`
3. Check: Project = `acMesure`, .elf = `acMesure.elf`
4. Click **Run**

---

## Important notes

- **`IAP_Set()` must be commented out** in `main()` — this function is intended for a bootloader and will crash the firmware when flashed directly at `0x08000000`.