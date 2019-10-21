# Example of simple cmake project for x86 desktop with app and tests.
This project contains static library with core functionality, test executable to run tests and application executable. Test and app executables are linked against core library, that contains main logic.
This project can be open and build in Qt Creator.

# Steps to build and run (assume GNU as default toolchain):
mkdir build
cd build
cmake ..
make
./tests
./app

Sometimes CMake generates Visual Studio solution on Windows by default. To force generating Unix style makefiles and use GNU toolchain you can use:
cmake -G "Unix Makefiles" ..
