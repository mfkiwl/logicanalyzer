# Generated Cmake Pico project file

cmake_minimum_required(VERSION 3.13)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# Initialise pico_sdk from installed location
# (note this can come from environment, CMake cache etc)
set(PICO_SDK_PATH "F:/PicoSDK/Pico/pico-sdk")

# Pull in Raspberry Pi Pico SDK (must be before project)
include(pico_sdk_import.cmake)

project(LogicAnalyzer C CXX ASM)

# Initialise the Raspberry Pi Pico SDK
pico_sdk_init()

# Add executable. Default name is the project name, version 0.1

# add_executable(LogicAnalyzer LogicAnalyzer.c )

FILE(GLOB CSources *.c)
ADD_EXECUTABLE(LogicAnalyzer ${CSources})

# Create C header file with the name <pio program>.pio.h
pico_generate_pio_header(${PROJECT_NAME}  
        ${CMAKE_CURRENT_LIST_DIR}/LogicAnalyzer.pio
)

pico_set_program_name(LogicAnalyzer "LogicAnalyzer")
pico_set_program_version(LogicAnalyzer "4.5")


pico_enable_stdio_uart(LogicAnalyzer 0)
pico_enable_stdio_usb(LogicAnalyzer 1)

# Configure the correct cyw library based on what this is built for
# Regular pico: empty
# Pico W without WiFi support: pico_cyw43_arch_none
# Pico W with WiFi support: pico_cyw43_arch_lwip_poll
# set (CYW_LIB pico_cyw43_arch_lwip_poll)
# set (CYW_LIB pico_cyw43_arch_none)

# Add any user requested libraries
target_link_libraries(LogicAnalyzer
        pico_stdlib
        hardware_dma
        hardware_pio
        hardware_clocks
        hardware_flash
        pico_multicore
        pico_base_headers
        pico_multicore
        ${CYW_LIB}
        )

pico_add_extra_outputs(LogicAnalyzer)

target_include_directories(LogicAnalyzer PRIVATE ${CMAKE_CURRENT_LIST_DIR} )