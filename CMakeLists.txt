cmake_minimum_required(VERSION 3.13)

# initialize the SDK based on PICO_SDK_PATH
# note: this must happen before project()
include(pico_sdk_import.cmake)

project(USBaudio)

# initialize the Raspberry Pi Pico SDK
pico_sdk_init()

# rest of your project

add_executable(USBaudio
        main.c 
		usb_descriptors.c
        )

# pull in common dependencies
target_link_libraries(USBaudio pico_stdlib pico_unique_id tinyusb_device tinyusb_board)

target_include_directories(USBaudio PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})

# create map/bin/hex/uf2 file etc.
pico_add_extra_outputs(USBaudio)