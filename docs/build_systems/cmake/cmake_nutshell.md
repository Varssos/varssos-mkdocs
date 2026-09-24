# CMake in a nutshell

## Basic invoking of cmake

Defaults:

- `FOLDER_WHERE_CMAKELISTS.TXT_IS` = `.`
- `BUILD_DIR` = `build`

```bash
# Create makefile
cmake -S {FOLDER_WHERE_CMAKELISTS.TXT_IS} -B {BUILD_DIR} -DCMAKE_BUILD_TYPE=Debug -DTESTS=True

# build
cmake -S {FOLDER_WHERE_CMAKELISTS.TXT_IS} --build {BUILD_DIR}

# install
sudo cmake -S {FOLDER_WHERE_CMAKELISTS.TXT_IS} --install build
```

In most cases:
```bash
cmake -B build
cmake --build build
sudo cmake --install build
```

## Necessary things to do in CMake

1. Set the required minimum cmake version:
```cmake
cmake_minimum_required(VERSION 3.16)
```

2. Set languages:
```cmake
enable_language(CXX)
enable_language(C)
```

3. Set project/binary name:
```cmake
project(${TARGET_NAME} LANGUAGES CXX VERSION ${VERSION})
```

4. Set the C++ standard:
```cmake
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)
```

5. Set source paths:
```cmake
set(SOURCES_PATH "${CMAKE_CURRENT_LIST_DIR}/sources/")
set(SOURCES_SRC_PATH "${SOURCES_PATH}/src/")
set(SOURCES_INC_PATH "${SOURCES_PATH}/inc/")
```

6. Set source file paths:
```cmake
file(GLOB SOURCE_DIRS ${SOURCES_SRC_PATH}/*)

foreach(SOURCE_DIR ${SOURCE_DIRS})
    if(IS_DIRECTORY ${SOURCE_DIR})
        aux_source_directory(${SOURCE_DIR} SRC_FILES_PATH)
    endif()
endforeach()
```

7. Make a binary named `${PROJECT_NAME}` using the previously retrieved `${SRC_FILES_PATH}`:
```cmake
add_executable(${PROJECT_NAME} ${SRC_FILES_PATH})
```

8. Include the `inc` directory:
```cmake
target_include_directories(${TARGET_NAME} PRIVATE
    $<BUILD_INTERFACE:${SOURCES_INC_PATH}>
)
```

9. Link libraries:
```cmake
target_link_libraries(${TARGET_NAME} PRIVATE ${MODULE_DEPS})
```

## Things you can set

1. App version:
```cmake
set(MAJOR 0)
set(MINOR 1)
set(PATCH 0)
set(VERSION ${MAJOR}.${MINOR}.${PATCH})
```

2. Set `CMAKE_BUILD_TYPE`, e.g. `Debug` or `Release`:
```cmake
if(NOT CMAKE_BUILD_TYPE)
    message(STATUS "CMAKE_BUILD_TYPE not defined. Set to Release")
    set(CMAKE_BUILD_TYPE Release)
elseif(NOT (${CMAKE_BUILD_TYPE} STREQUAL "Debug" OR ${CMAKE_BUILD_TYPE} STREQUAL "Release"))
    message(FATAL_ERROR "CMAKE_BUILD_TYPE must be either Release or Debug")
endif()
```

3. Include test cmake:
```cmake
if(NOT DEFINED TESTS)
    SET(TESTS "False")
endif()

if(${TESTS} STREQUAL "True")
    include(tests.cmake)
endif()
```
