# Example of simple cmake project for x86 desktop.
This project can be built from command line or opened in Qt Creator.

# Steps to build and run (assume GNU as default toolchain):
mkdir build
cd build
cmake ..
make
./helloworld.exe

Sometimes CMake generates Visual Studio solution on Windows by default. To force generating Unix style makefiles and use GNU toolchain you can use:
cmake -G "Unix Makefiles" ..
