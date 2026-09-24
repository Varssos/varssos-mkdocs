# Setup environment

[VS code C++ template project with gtest and cmake](https://github.com/Varssos/Cpp_CMake_GTest_Template)

[C_Cmake_NoTests_Template](https://github.com/Varssos/C_CMake_NoTests_Template)

[C_Makefile_NoTests_Template](https://github.com/Varssos/C_Makefile_NoTests_Template.git)

## Visual studio code setup

At first install the C/C++ extension and C/C++ extension pack

### VS code keyboard shortcut

1. `File->Preferences->Keyboard Shortcut`
2. Remove shortcut `ctrl+shift+b` for `Tasks: Run Build Task`
3. Find: `Tasks: Run Task`, set shortcut `ctrl+shift+b`
4. On the top right corner `Open Keyboard Shortcuts (JSON)`
5. Add on the bottom JSON object (`~/.config/Code/User/keybindings.json`):

```json
[
    {
        "key": "ctrl+shift+b",
        "command": "-workbench.action.tasks.build"
    },
    {
        "key": "ctrl+shift+b",
        "command": "workbench.action.tasks.runTask"
    },
    {
        "key": "ctrl+k",
        "command": "workbench.action.terminal.focus"
    },
    {
        "key": "ctrl+k",
        "command": "workbench.action.focusActiveEditorGroup",
        "when": "terminalFocus"
    }
]
```

### Project configuration

1. Open folder with project
2. `ctrl+P` -> `>` -> `Edit configurations (JSON)`
3. In `includePath` you can add some extra header files for external libraries
4. Adjust `cppStandard` for project standard
5. c_cpp_properties.json

```json
{
    "configurations": [
    {
            "name": "Linux",
            "includePath": [
                "${workspaceFolder}/**",
                "/usr/local/include/{HERE_INSERT_subfolder}/*"
            ],
            "defines": [],
            "compilerPath": "/usr/bin/gcc",
            "cStandard": "gnu17",
            "cppStandard": "gnu++17",
            "intelliSenseMode": "linux-gcc-x64"
        }
    ],
    "version": 4
}
```

### Tasks configuration

1. `Terminal->Configure Tasks...` or `F1` -> `Tasks: Configure Task`
2. Add on the bottom:

```json
{
    "label": "build",
    "type": "shell",
    "options": {
        "cwd": "${workspaceRoot}"
    },
    "command": "cmake --build build",
    "problemMatcher": []
},
{
    "label": "install",
    "type": "shell",
    "options": {
        "cwd": "${workspaceRoot}"
    },
    "command": "sudo cmake --install build",
    "problemMatcher": []
},
{
    "label": "clean",
    "type": "shell",
    "options": {
        "cwd": "${workspaceRoot}"
    },
    "command": "cmake --clean build",
    "problemMatcher": []
},
{
    "label": "run_tests",
    "type": "shell",
    "options": {
        "cwd": "${workspaceRoot}"
    },
    "command": "./build/tests",
    "problemMatcher": []
}
```

## Launch

1. `Run->Add Configuration`
2. launch.json

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(gdb) Launch",
            "type": "cppdbg",
            "request": "launch",
            "program": "{path_to_bin}",
            "args": [
                "-c",
                "{here are additional flags}"
            ],
            "stopAtEntry": false,
            "cwd": "${fileDirname}",
            "environment": [],
            "externalConsole": true,
            "MIMode": "gdb",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ]
        }
    ]
}
```

### Alternative launch.json

This way you have to specify `Set the default build target` and `Select the target to launch`

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Debug target",
            "type": "cppdbg",
            "request": "launch",
            "program": "${command:cmake.launchTargetPath}",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": false
        }
    ]
}
```

### Debug configuration

If the app is very simple just watch [VS debugging](https://www.youtube.com/watch?v=G9gnSGKYIg4), otherwise if it is not enough try the hints described below.

Before you start, make sure that the binary and shared libraries are built with the arg `-g` or, in CMake, `CMAKE_BUILD_TYPE` set to `Debug`. Otherwise gdb will not stop on desired breakpoints.

**Building binary with Cmake:**

1. Navigate to {project_directory}
2. `mkdir build`
3. `cd build`
4. `cmake -DCMAKE_BUILD_TYPE=Debug ../`
5. After that, when you type `cmake --build build` and `cmake --install build` in {project_directory} it will build as a debug bin/shared_obj

**Steps to configure debugging in VS**

1. Go to the "Run and Debug" section on the left hand side, click "create a launch.json file" and choose GDB
2. In launch.json change the section "program" to the program binary location e.g.: `/usr/local/bin/{bin_name}`
3. If any args are needed set them in this way:

```json
"args": [
    "-c", 
    "{directory}/config_file.cfg" ],
```

4. It is possible to specify the gdb binary location, just add the section `"miDebuggerPath": "/usr/bin/gdb"`

## Install MinGw in Windows

1. [Install gcc/g++](https://www.youtube.com/watch?v=8CNRX1Bk5sY)

    [MinGW installer](https://osdn.net/projects/mingw/releases/)

2. Add c++ extension to VS code
3. Prepare a makefile like this

```bash
CXX = g++

TARGET = thread

FLAGS = -g -Wall -std=c++17

all: $(TARGET).cpp
    $(CXX) $(FLAGS) -o $(TARGET) $(TARGET).cpp

clean: 
    rm thread.exe
```

## Windows WSL for C/C++

Try this video first:

[C++ vs code wsl environment setup](https://www.youtube.com/watch?v=NY5izJWXi0U)

### Install WSL

1. Open cmd
2. `wsl --install`

### Set up your Linux environment in WSL

```bash
# Navigate to your vs code project,
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install build-essential gdb cmake
```

### VS code setup in WSL with my C template projects

1. Open VS code
2. Install the WSL VS code extension if not installed
3. Click in the bottom left corner and `Open Folder in WSL`
4. Use make or cmake to build the app as described in my C project template
5. Move to the `Run and Debug` section on the left hand side in VS code.
6. Choose `gdb_Windows`
7. Run debug

### Alternative VS code setup in WSL

1. Open VS code
2. Install the WSL VS code extension
3. Click in the bottom left corner and `Open Folder in WSL`
4. Write your code
5. `Terminal` -> `Configure Default Build Task`. Choose `/usr/bin/gcc` or `/usr/bin/g++`
6. `Run` -> `Start Debugging` -> `/usr/bin/gcc` or `/usr/bin/g++`
7. Done. Remember to set a breakpoint during debugging
8. You can git clone my C/C++ project listed on the top of this page

## Disable auto completion in VS code

Copilot -> Settings -> Copilot -> Editor: Enable Auto Completions
Suggestions -> Settings -> type "suggestions" -> Editor: Quick Suggestion -> Item: other -> off
