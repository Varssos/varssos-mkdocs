# CMake environment setup

## Install cmake on Windows

1. Install cmake from [here](https://cmake.org/download/) with `Add CMake to the system PATH for all users`.
2. Add the installed cmake `bin` folder to your Path, e.g. `C:\Program Files\CMake\bin\`.
3. If you are using MinGW, use the MinGW Installation Manager to install `mingw32-make-bin` or `mingw32-make`. In that case you should also add `C:\MinGW\bin\` to Path.
4. You would then be forced to use cmake like this: `cmake -G "MinGW Makefiles" ..`.

## Install cmake on Linux

1. Update and upgrade package repositories:
```bash
sudo apt update && sudo apt upgrade -y
```

2. Install with the APT repository:
```bash
sudo apt install cmake
```

3. Check the installed cmake version:
```bash
cmake --version
# Output:
cmake version 3.16.3

CMake suite maintained and supported by Kitware (kitware.com/cmake).
```

Or, if apt has an old cmake version, install from [snap](https://graspingtech.com/upgrade-cmake/) instead.
