cmake_minimum_required(VERSION 3.14)
set(PICO_BOARD pico_w)
include(pico_sdk_import.cmake)

project(test_picow)

pico_sdk_init()

add_executable(test_picow
    main.c
)

target_include_directories(test_picow PRIVATE
        ${CMAKE_CURRENT_LIST_DIR}
)
# Add pico_stdlib library, add more if used
target_link_libraries(test_picow pico_cyw43_arch_lwip_threadsafe_background pico_stdlib)

# enable usb output, disable uart output
pico_enable_stdio_usb(test_picow 1)
pico_enable_stdio_uart(test_picow 0)

# Need to generate UF2 file for upload to RP2040
pico_add_extra_outputs(test_picow)