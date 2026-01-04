# JPEG

## JPEG files recovery

[JPEG files recovery](./jpeg_files_recovery.md)


## JPEG structure

![JPEGRGB dissected](JPEGRGB_dissected.png)

General info:

- JPEG consist of many segments
- Usually JPEGs have different structures of segments but generally something like:
    ```
    FF D8        → SOI
    FF E0        → APP0 (JFIF)
    FF E1        → APP1 (EXIF)
    FF DB        → DQT
    FF C0        → SOF0
    FF DA        → SOS
    ... image ...
    FF D9        → EOI
    ```
- Each segment has multiple fields
- Each field has value
- __The most important segment about matadata is APP1__

### SOI - first segment
It consists of the start marker.
```
FF D8
```

- `FF` - marker
- `D8` - segment type

### APPn - Application Segments
It consists of a marker, length field, and application-specific data.
```
FF XX [LEN_H] [LEN_L] [DATA..]
```

- `APP0` - `FF E0` - JFIF/JFXX
- `APP1` - `FF E1` - EXIF/XMP
- ...
- `APP14` - `FF EE` - Adobe

#### APP0 - JFIF/JFXX
- basic metadata (no GPS, date, device)

#### APP1 - EXIF/XMP
Example EXIF:

```
Hex View  00 01 02 03 04 05 06 07  08 09 0A 0B 0C 0D 0E 0F
 
00000000  FF D8 FF E1 3F 4F 45 78  69 66 00 00 49 49 2A 00  ....?OExif..II*.
00000010  08 00 00 00 0B 00 0F 01  02 00 07 00 00 00 92 00  ................
00000020  00 00 10 01 02 00 08 00  00 00 99 00 00 00 12 01  ................
00000030  03 00 01 00 00 00 01 00  00 00 1A 01 05 00 01 00  ................
00000040  00 00 A1 00 00 00 1B 01  05 00 01 00 00 00 A9 00  ................
00000050  00 00 28 01 03 00 01 00  00 00 02 00 00 00 31 01  ..(...........1.
00000060  02 00 15 00 00 00 B1 00  00 00 32 01 02 00 14 00  ..........2.....
00000070  00 00 C6 00 00 00 13 02  03 00 01 00 00 00 01 00  ................
00000080  00 00 69 87 04 00 01 00  00 00 DA 00 00 00 25 88  ..i...........%.
00000090  04 00 01 00 00 00 B8 03  00 00 A5 04 00 00 47 6F  ..............Go
000000A0  6F 67 6C 65 00 50 69 78  65 6C 20 37 00 48 00 00  ogle.Pixel 7.H..
```

##### APP1 Pattern
```
FF E1 [LEN_H] [LEN_L] [IDENTIFIER] [DATA...]
```

- `3F 4F` - length
- `45 78 69 66 00 00` - exif identifier

##### TIFF Header
```
49 49 2A 00 08 00 00 00
```

- `49 49` - Little-endian
- `2A 00` - TIFF magic number
- `08 00 00 00` - offset to IFD0

##### IFDO - Primary Image File Directory
```
0B 00 - 11 directory entries
```

##### Entry pattern
```
[Tag (2)] [Type (2)] [Count (4)] [Value or Offset (4)]
```

##### First entry
```
0F 01  02 00 07 00 00 00 92 00 00 00
```

- `0F 01` -> 0x010F - tag: make
- `02 00` -> 0x0002 - type: ASCII
- `07 00 00 00` -> 7 bytes
- `92 00 00 00` -> 0x00000092 offset (starting from TIFF base (0x49 - little endian))

Real data: 
`47 6F 6F 67 6C 65 00` -> `Google`



### DQT - Define Quantization Table
It consists of a marker, length, quantization table information, and 64 quantization values.
```
FF DB [LEN_H] [LEN_L] [PQ_TQ] [Q0..63]
```

- `FF DB` - marker
- `LEN_H LEN_L` - length of segment (including itself)
- `PQ_TQ` - precision (4 bits) and table destination (4 bits)
- `Q0..63` - 64 quantization values

### SOF0 - Start of Frame (Baseline DCT)
It consists of a marker, length, image dimensions, precision, number of components, and component details including sampling factors.
```
FF C0 [LEN_H] [LEN_L] [P] [Y_H Y_L] [X_H X_L] [Nf] [C1..Nf] [H1 V1 Q1] ...
```

- `FF C0` - marker
- `LEN_H LEN_L` - length
- `P` - precision (8 or 12 bits)
- `Y_H Y_L` - height
- `X_H X_L` - width
- `Nf` - number of components
- For each component: component ID, horizontal/vertical sampling, quantization table

### DHT - Define Huffman Table
It consists of a marker, length, table class and destination, code lengths, and Huffman values.
```
FF C4 [LEN_H] [LEN_L] [Tc_Th] [L1..16] [V1..]
```

- `FF C4` - marker
- `LEN_H LEN_L` - length
- `Tc_Th` - table class (0=DC, 1=AC) and table destination
- `L1..16` - number of codes of each length
- `V1..` - Huffman values

### SOS - Start of Scan
It consists of a marker, length, number of components, component selectors, table selectors, and scan parameters.
```
FF DA [LEN_H] [LEN_L] [Ns] [Cs1..Ns] [Td1 Ta1] ... [Ss] [Se] [Ah Al]
```

- `FF DA` - marker
- `LEN_H LEN_L` - length
- `Ns` - number of components in scan
- For each component: component selector, DC/AC table selectors
- `Ss Se` - start/end spectral selection
- `Ah Al` - successive approximation

### EOI - End of Image
It consists of the end marker.
```
FF D9
```

- `FF D9` - marker
- Indicates end of JPEG file

