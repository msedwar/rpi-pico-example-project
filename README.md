# Raspberry Pi Pico Project Setup

## Submodule Dependencies
```
$ git submodule update --init --recursive
```

## Additional Dependencies

### Linux
```
$ sudo apt install cmake gcc-arm-none-eabi libnewlib-arm-none-eabi libstdc++-arm-none-eabi-newlib
```

### Mac
```
$ brew tap ArmMbed/homebrew-formulae
$ brew install armmbed/formulae/arm-none-eabi-gcc
```

## Building

### Initializing CMake
```
$ export PICO_SDK_PATH=../lib/pico-sdk
$ mkdir build
$ cd build
$ cmake ..
```

### Building
```
$ make -j4
```

## Flashing
Plug the RPI Pico in to the host machine via USB while holding the BOOTSEL button. The UF2 binary can then be dragged and dropped into the Pico Flash Storage USB device.

To flash via the command line, you must install `picotool` (see the Pico [datasheet](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf)).

```
$ picotool load build/main.uf2
```
