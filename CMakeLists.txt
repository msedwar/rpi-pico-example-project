cmake_minimum_required(VERSION 3.13)

set(PICO_COMPILER "pico_arm_gcc" CACHE INTERNAL "Specify GCC for toolchain compiler")

# Include the SDK submodule.
# Note: This must happen before project() declaration.
if (DEFINED ENV{PICO_SDK_PATH})
  message("Using environment PICO_SDK_PATH")
  set(PICO_SDK_PATH $ENV{PICO_SDK_PATH}/pico_sdk_init.cmake)
else()
  set(PICO_SDK_PATH lib/pico-sdk/pico_sdk_init.cmake)
endif()
include(${PICO_SDK_PATH})

project(rpi_pico C CXX ASM)

# Initialize the SDK.
pico_sdk_init()

# Main executable.
add_executable(main
  src/main.c
)
target_link_libraries(main
  pico_stdlib
)

# Enable USB, disable UART output.
pico_enable_stdio_usb(main 1)
pico_enable_stdio_uart(main 0)

# Create UF2 in addition to standard ELF binary.
pico_add_extra_outputs(main)
