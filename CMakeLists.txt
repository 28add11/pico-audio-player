cmake_minimum_required(VERSION 3.13)

# initialize the SDK based on PICO_SDK_PATH
# note: this must happen before project()
include(pico_sdk_import.cmake)

project(my_project)

# initialize the Raspberry Pi Pico SDK
pico_sdk_init()

# rest of your project
add_executable(picoSpeaker
    main.c
	usb_descriptors.c
)

pico_enable_stdio_usb(picoSpeaker 0)
pico_enable_stdio_uart(picoSpeaker 1)

# Add pico_stdlib library which aggregates commonly used features
target_link_libraries(picoSpeaker pico_stdlib pico_unique_id tinyusb_device tinyusb_board)

target_include_directories(picoSpeaker PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})

# create map/bin/hex/uf2 file in addition to ELF.
pico_add_extra_outputs(picoSpeaker)
