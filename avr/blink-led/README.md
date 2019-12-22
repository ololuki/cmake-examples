# CMake simple blink led project for AVR
This project can be built from command line or opened in Qt Creator.

# Usage

## Just build
```
mkdir build
cd build
cmake .. -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=MinSizeRel
make
```
or:
```
mkdir build
cd build
cmake .. -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=MinSizeRel
cmake --build . --target all
```

## Build with detailed log - print gcc parameters
```
mkdir build
cd build
cmake .. -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=MinSizeRel
make VERBOSE=1 --no-print-directory
```
or:
```
mkdir build
cd build
cmake .. -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=MinSizeRel
cmake --build . --target all -- VERBOSE=1 --no-print-directory
```
