cmake_minimum_required(VERSION 3.10)

# usage: cmake -G "Unix Makefiles"
if(NOT "${CMAKE_GENERATOR}" STREQUAL "Unix Makefiles")
   message(FATAL_ERROR "CMAKE_GENERATOR must be set to Unix Makefiles: cmake -G \"Unix Makefiles\"")
endif()


# options to set used processor and crystal frequency
set(MCU   atmega32)
set(F_CPU 8000000)


# uncomment following line if you want Qt Creator to automatically generate
# verbose makefile to trace compiler and linker options in build log
# you can as well add parameter VERBOSE=1 to "make" or "cmake --build" command
# (in Qt Creator Project -> Build Steps -> Tool arguments)
#set(CMAKE_VERBOSE_MAKEFILE TRUE)


# this include must be before project() https://gitlab.kitware.com/cmake/community/wikis/FAQ#how-do-i-use-a-different-compiler
include(avr-gcc.cmake)


# add_compile_options have to be set before add_executable
# https://stackoverflow.com/questions/40516794/cmake-not-applying-compile-option-using-add-compile-options
add_compile_options("-mmcu=${MCU}")

# add optimization flags
add_compile_options(-ffunction-sections)
add_compile_options(-fdata-sections)
add_compile_options(-funsigned-char)
add_compile_options(-funsigned-bitfields)
add_compile_options(-fpack-struct)
add_compile_options(-fshort-enums)

# max debug info for more verbose dissassembly .lss file
# it does not affects hex size so it is always generated
add_compile_options(-g3)

# optimization for size
# no needed if invoked with CMAKE_BUILD_TYPE set to MinSizeRel
#add_compile_options(-Os)

# define crystal frequency
add_definitions(-DF_CPU=${F_CPU})


project(ProjectName)


add_executable(
    ${PROJECT_NAME}
    main.cpp)


# add linker options
# target_link_options or add_link_options can be used instead since cmake 3.13
target_link_libraries(${PROJECT_NAME} -mmcu=${MCU})
target_link_libraries(${PROJECT_NAME} -Wl,-Map=${PROJECT_NAME}.map,--cref)
target_link_libraries(${PROJECT_NAME} -Wl,--gc-sections)


# for older versions of Qt Creator (eg. 4.2.0) this needed to be defined
# in newest (4.10.0) this bug was fixed and now file avr/io.h is parsed properly
# so following line is commented out
# maybe this is a reason of improvements?
# https://www.qt.io/blog/2016/11/15/cmake-support-in-qt-creator-and-elsewhere
#add_definitions(-D__AVR_ATmega8A__) # for QtCreator


# post build - print size, generate hex, eeprom and listing with assembly
add_custom_command(TARGET ${PROJECT_NAME}
    POST_BUILD
    COMMAND ${AVR_SIZE_TOOL} --mcu=${MCU} --format=avr ${PROJECT_NAME}
    COMMAND ${AVR_OBJCOPY} -R .eeprom -O ihex ${PROJECT_NAME} ${PROJECT_NAME}.hex
    COMMAND ${AVR_OBJCOPY} --no-change-warnings -j .eeprom --change-section-lma .eeprom=0 -O ihex ${PROJECT_NAME} ${PROJECT_NAME}.eep
    COMMAND ${AVR_OBJDUMP} -h -S ${PROJECT_NAME} > ${PROJECT_NAME}.lss
)
