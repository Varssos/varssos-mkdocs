# Steam on Linux

## Tricks
- Show fps: Steam->Settings->In Game -> Show performance monitor (choose something)




## Games
### Asseto Corsa Competezione
Kubuntu 26.04: Works with Proton 9.0-4

### Asseto Corsa EVO
Kubuntu 26.04: Proton Experimental, but low FPS, launch options:
```
VKD3D_CONFIG=descriptor_heap PROTON_ENABLE_HIDRAW=1 PROTON_FORCE_LARGE_ADDRESS_AWARE=1 %command% -popupwindow -window-mode borderless
```

- Full screen `alt+enter`

<details>
<summary>Issues</summary>

1) On clean proton >=10

Wine C++ Runtime Library
Assertion failed!
Program:
Z:\nome\sw/ steam\debian-installation\steamapps\common\Assetto
Corsa EVO\AssettoCorsaEVO.exe
File: ./s¢-wine/dlls/winevulkan/loader_thunks.c
Une: 2775
Expression: “Istatus 66. "vkCreateComputePipelines™
Press OK to exit the program, or Cancel to start the Wine debugger.
—s Cancel


</details>

### Asseto Corsa Rally

Kubuntu 26.04: Works with Proton 9.0-4

<details>
<summary>Issues</summary>
- On proton >=10 steering wheel snaps to full lock upon pausing

</details>


### Counter-Strike 2

Processing Vulkan shaders takes a lot of time...

### DIRT Rally 2.0

Kubuntu 26.04: Works with Proton 9.0-4
### Euro Truck Simulator 2
Kubuntu 26.04: Works with steam Linux Runtime 1.0
### F1 24
:no_entry:
`Wine, Proton and Stream Deck are not supported by this application!`

Not possible due to anticheats on linux

### Stronghold Crusader HD

Ubuntu 26.04: Works with Proton 11.0-2 and earlier