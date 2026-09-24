# Static vs shared library

We have 2 types of libraries in C/C++: static and shared.

Static is used by executable program on compile time, it copy necessary content to this executable. So:

Memory
:   memory of our app will be increased

Recompilation
:   each time when library has changed, our app has to be compiled again

Standalone
:   app after compiling can work standalone, without static library files

Extensions
:   `.a` on linux and `.lib` on windows

Shared library:

Memory
:   memory of our app can be reduced

Recompilation
:   each time when library has changed, we don't need to compile our app

Dependency
:   our app has a strong dependency from these files and probably can't work without these shared library files

Extensions
:   `.so` on linux and `.dll` on windows

## How to create static/shared libraries

[static vs shared bulldogjob](https://bulldogjob.pl/readme/biblioteki-dynamiczne-i-statyczne-w-jezyku-c)

Example project tree:

```
├── app.cpp
├── build
├── CMakeLists.txt
├── device.cpp
└── device.hpp
```

### Static library on linux

1. Create object files( device.o ):

```bash
g++ -c device.cpp
```

2. Create static library ( libdevice.a ):

```bash
ar rc libdevice.a device.o
# r - replace existing or insert new file(s) into the archive
# c - do not warn if the library had to be created
```

3. Link static library to your executable file:

```bash
g++ app.cpp -ldevice -o app -L .
# or
g++ app.cpp -l:libdevice.a -o app -L .

# -L indicate a directory which should be search for library to avoid:
# /usr/bin/ld: cannot find -ldevice
# collect2: error: ld returned 1 exit status
```

!!! warning
    In `g++ app.cpp -ldevice -o app -L .` You have to specify .cpp files first then library!

Display content of the archive:

```bash
ar t libdevice.a
# or
nm libdevice.a
```

Determine type of files:

```bash
file ./app
# output:
app: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=3200b2d6ab6019315de7fbb9b858d19fc239e99c, for GNU/Linux 3.2.0, not stripped
```

You can add flag `-static` to make whole app truly static:

```bash
g++ app.cpp -l:libdevice.a -o app -L . -static
# then: check:
file ./app
# output :
app: ELF 64-bit LSB executable, x86-64, version 1 (GNU/Linux), statically linked, BuildID[sha1]=6a43a97cb5e98bdc575606c81845f471ad6cb15b, for GNU/Linux 3.2.0, not stripped
```

### Static library with CMake

Basic CMake example

```cmake
cmake_minimum_required( VERSION 3.16 )

project( app )

set( LIB_SRC device.cpp)

add_library(device STATIC ${LIB_SRC})
add_executable( app app.cpp)

target_link_libraries( app device)
```

### Shared library on linux

[How to create shared library in C++](https://iq.opengenus.org/create-shared-library-in-cpp/)

1. Create object files( device.o ) with Position Independent Code `-fPIC`:

```bash
g++ -fPIC -c device.cpp
```

2. Create shared library ( libdevice.so ):

```bash
g++ -shared -o libdevice.so device.o
```

3. Link shared library to your executable file:

```bash
g++ app.cpp -L . -ldevice -o app
```

4. Install shared lib in standard location or export path to that shared library:

```bash
export LD_LIBRARY_PATH=/full_path_to_your_library_location/libname:$LD_LIBRARY_PATH
```

### Shared library with CMake

Basic CMake example

```cmake
cmake_minimum_required( VERSION 3.16 )

project( app )

set( LIB_SRC device.cpp)

add_library(device SHARED ${LIB_SRC})
add_executable( app app.cpp)

target_link_libraries( app device)
```
