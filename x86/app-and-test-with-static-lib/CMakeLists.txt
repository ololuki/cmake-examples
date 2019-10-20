cmake_minimum_required(VERSION 3.10)
project(Project)

# Core logic
set(CORE_SOURCES
    core/Calculator.cpp)
add_library(core ${CORE_SOURCES})                                    #compile core as static library

# Application
set(APP_SOURCES
    app/main.cpp)
add_executable(app ${APP_SOURCES})
target_include_directories(app PUBLIC ${CMAKE_SOURCE_DIR})           #add main directory to include path

# Tests
set(TEST_SOURCES
    tests/TestMain.cpp
    tests/CalculatorTest.cpp)
add_executable(tests ${TEST_SOURCES})
target_include_directories(tests PUBLIC ${CMAKE_SOURCE_DIR})         #add main directory to include path
target_include_directories(tests PUBLIC ${CMAKE_SOURCE_DIR}/lib)     #include Catch library

# Link test and app with core library
target_link_libraries(tests core)
target_link_libraries(app core)

set_property(TARGET tests PROPERTY CXX_STANDARD 11)                  #Catch library requires C++11 support
