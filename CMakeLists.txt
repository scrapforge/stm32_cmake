cmake_minimum_required(VERSION 3.15.3)
include(FetchContent)

set(CMAKE_TOOLCHAIN_FILE "${CMAKE_CURRENT_LIST_DIR}/arm-none-eabi-gcc.cmake")

project(nucleo-h743zi C CXX ASM)

enable_language(C ASM)
set(MC h7)
set(MC_TYPE 43)
set(MC_MEMORY zit)

set(MC_LC ${MC})
set(MC_TYPE_LC ${MC_TYPE})
set(MC_MEMORY_LC ${MC_MEMORY})
string(TOUPPER ${MC_LC} MC_UC)
string(TOUPPER ${MC_TYPE_LC} MC_TYPE_UC)
string(TOUPPER ${MC_MEMORY_LC} MC_MEMORY_UC)

set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS OFF)
set(USE_FULL_LL_DRIVER TRUE)

FetchContent_Declare(
  stm32_cmsis_device
  GIT_REPOSITORY https://github.com/STMicroelectronics/cmsis_device_${MC_LC}.git
  # GIT_TAG        v1.10.3
)

FetchContent_Declare(
  stm32_cmsis_core
  GIT_REPOSITORY https://github.com/STMicroelectronics/cmsis_core.git
  # GIT_TAG        v1.10.3
)

FetchContent_Declare(
  stm32_hal
  GIT_REPOSITORY https://github.com/STMicroelectronics/stm32${MC_LC}xx_hal_driver.git
  # GIT_TAG        v1.10.3
)

FetchContent_Declare(
  stm32_bsp
  GIT_REPOSITORY https://github.com/STMicroelectronics/stm32${MC_LC}xx-nucleo-bsp.git
  GIT_TAG        main #v1.10.3
)

FetchContent_MakeAvailable(stm32_cmsis_device stm32_cmsis_core stm32_hal stm32_bsp)

set(STM32_HAL_SOURCE_FILES
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_adc.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_adc_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_cec.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_comp.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_cordic.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_cortex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_crc.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_crc_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_cryp.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_cryp_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_dac.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_dac_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_dcmi.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_dfsdm.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_dfsdm_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_dma2d.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_dma.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_dma_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_dsi.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_dts.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_eth.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_eth_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_exti.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_fdcan.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_flash.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_flash_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_fmac.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_gfxmmu.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_gpio.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_hash.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_hash_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_hcd.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_hrtim.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_hsem.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_i2c.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_i2c_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_i2s.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_i2s_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_irda.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_iwdg.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_jpeg.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_lptim.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_ltdc.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_ltdc_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_mdios.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_mdma.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_mmc.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_mmc_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_nand.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_nor.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_opamp.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_opamp_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_ospi.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_otfdec.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_pcd.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_pcd_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_pssi.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_pwr.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_pwr_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_qspi.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_ramecc.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_rcc.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_rcc_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_rng.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_rng_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_rtc.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_rtc_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_sai.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_sai_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_sd.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_sd_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_sdram.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_smartcard.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_smartcard_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_smbus.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_smbus_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_spdifrx.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_spi.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_spi_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_sram.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_swpmi.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_tim.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_tim_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_uart.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_uart_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_usart.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_usart_ex.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_hal_wwdg.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_adc.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_bdma.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_comp.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_cordic.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_crc.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_crs.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_dac.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_delayblock.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_dma2d.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_dma.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_exti.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_fmac.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_fmc.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_gpio.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_hrtim.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_i2c.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_lptim.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_lpuart.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_mdma.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_opamp.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_pwr.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_rcc.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_rng.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_rtc.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_sdmmc.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_spi.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_swpmi.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_tim.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_usart.c
    ${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_usb.c
    #${stm32_hal_SOURCE_DIR}/Src/stm32${MC_LC}xx_ll_utils.c
    ${stm32_bsp_SOURCE_DIR}/stm32${MC_LC}xx_nucleo.c)


set(SOURCE_FILES
   # Inc/main.h
    # Inc/stm32${MC_LC}xx_hal_conf.h
    # Inc/stm32${MC_LC}xx_it.h
    Src/main.c
    Src/stm32${MC_LC}xx_hal_msp.c
    Src/stm32${MC_LC}xx_it.c
    Src/system_stm32${MC_LC}xx.c

    startup_stm32${MC_LC}${MC_TYPE_LC}xx.s)

set(EXECUTABLE ${PROJECT_NAME}.out)

add_executable(${EXECUTABLE} ${STM32_HAL_SOURCE_FILES} ${SOURCE_FILES})

target_compile_definitions(${EXECUTABLE} PRIVATE
        -DUSE_HAL_DRIVER
        -DSTM32${MC_UC}${MC_TYPE_UC}xx
        )

target_include_directories(${EXECUTABLE} PRIVATE
        ${stm32_hal_SOURCE_DIR}/Inc
        ${stm32_bsp_SOURCE_DIR}
        ${stm32_cmsis_device_SOURCE_DIR}/Include
        ${stm32_cmsis_core_SOURCE_DIR}/Include
        Inc
        )

target_compile_options(${EXECUTABLE} PRIVATE
        -mcpu=cortex-m7
        -mthumb
        -mfpu=fpv4-sp-d16
        -mfloat-abi=hard
        -fdata-sections
        -ffunction-sections
        -Wall

        $<$<CONFIG:Debug>:-Og>
        )

target_link_options(${EXECUTABLE} PRIVATE
        -T${CMAKE_SOURCE_DIR}/STM32${MC_UC}${MC_TYPE_UC}${MC_MEMORY_UC}X_FLASH.ld
        -mcpu=cortex-m7
        -mthumb
        -mfpu=fpv4-sp-d16
        -mfloat-abi=hard
        -specs=nano.specs
        -lc
        -lm
        -lnosys
        -Wl,-Map=${PROJECT_NAME}.map,--cref
        -Wl,--gc-sections
        )

# Print executable size
add_custom_command(TARGET ${EXECUTABLE}
        POST_BUILD
        COMMAND arm-none-eabi-size ${EXECUTABLE})

# Create hex file
add_custom_command(TARGET ${EXECUTABLE}
        POST_BUILD
        COMMAND arm-none-eabi-objcopy -O ihex ${EXECUTABLE} ${PROJECT_NAME}.hex
        # COMMAND arm-none-eabi-objcopy -O elf ${EXECUTABLE} ${PROJECT_NAME}.elf
        COMMAND arm-none-eabi-objcopy -O binary ${EXECUTABLE} ${PROJECT_NAME}.bin)

