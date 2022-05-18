cmake_minimum_required(VERSION 3.13)

set(PICO_COMPILER "pico_arm_gcc" CACHE INTERNAL "Specify GCC for toolchain compiler")

# Include the SDK submodule.
# Note: This must happen before project() declaration.
include(lib/pico-sdk/pico_sdk_init.cmake)

if (APPLE)
  # Homebrew arm-none-eabi-gcc installation path.
  include_directories(/usr/local/Cellar/arm-none-eabi-gcc/10.3-2021.07/gcc/arm-none-eabi/include)
endif()

project(rpi_pico C CXX ASM)

# Initialize the SDK.
pico_sdk_init()

# Main executable.
add_executable(main
  src/main.c
)
target_link_libraries(main pico_stdlib)

# Enable USB, UART output.
pico_enable_stdio_usb(main 1)
pico_enable_stdio_uart(main 1)

# Create UF2 in addition to standard ELF binary.
pico_add_extra_outputs(main)
