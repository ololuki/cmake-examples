# CMake simple blink led project for AVR

# Usage

## Just build
```
cmake .. -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=MinSizeRel
make
```
or:
```
cmake .. -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=MinSizeRel
cmake --build . --target all
```

## Build with detailed log - print gcc parameters
```
cmake .. -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=MinSizeRel
make VERBOSE=1 --no-print-directory
```
or:
```
cmake .. -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=MinSizeRel
cmake --build . --target all -- VERBOSE=1 --no-print-directory
```
