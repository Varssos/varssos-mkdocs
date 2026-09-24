# CMake tutorial

[CMake tutorial for beginners](https://cmake.org/cmake/help/latest/guide/tutorial/index.html) and on [YouTube](https://www.youtube.com/watch?v=nlKcXPUJGwA&list=PLalVdRk2RC6o5GHu618ARWh0VO0bFlif4&index=1).

## Base project

`PROJ_DIR` contains:

- `CMakeLists.txt`
- source files (here `tutorial.cpp`)
- build directory (here: `./out/build/`)

### CMakeLists.txt
```cmake
cmake_minimum_required(VERSION 3.16.3)

project(OLAS) # It sets the ${PROJECT_NAME} variable

add_executable(${PROJECT_NAME} tutorial.cpp) # Makes a binary called ${PROJECT_NAME} from the source files
```

### tutorial.cpp
```cpp
#include <iostream>

int main(int argc, char* argv[])
{
    std::cout << "Hello" << std::endl;

    return 0;
}
```

Commands:
```bash
mkdir -p ./out/build
cmake -S . -B ./out/build # in PROJ_DIR
# -S indicates the folder with CMakeLists.txt
# -B indicates the build folder
cd ./out/build
make
./OLAS
```

## Adding a library

For this tutorial we will put the library into a subdirectory called `Adder`. This directory contains a header file `adder.hpp`, a source file `adder.cpp` which contains the `add` function, and a `CMakeLists.txt` which should contain:
```cmake
add_library(adder adder.cpp)
```

See [`add_library`](https://cmake.org/cmake/help/latest/command/add_library.html).

To make use of the new library we add an `add_subdirectory()` call in the top-level `CMakeLists.txt` so that the library gets built. We add the new library to the executable and link `adder`:

`CMakeLists.txt`:
```cmake
cmake_minimum_required(VERSION 3.16.3)

project(OLAS)

add_subdirectory(Adder)

add_executable(${PROJECT_NAME} tutorial.cpp)

target_link_libraries(${PROJECT_NAME} adder)

target_include_directories(${PROJECT_NAME} PUBLIC
                                        "${PROJECT_SOURCE_DIR}/Adder")
```

!!! note "TODO"
    1. Clean up all unnecessary data.
    2. Divide into important sections and fill them in.
