# ExifTool

[ExifTool documentation](https://exiftool.org/exiftool_pod.html)

## Install exiftool
From official Ubuntu repo. It's not the latest :/
```
sudo apt update
sudo apt install libimage-exiftool-perl
```


## [JPEG] Useful exiftool commands


### Change dates in jpegs
```
EXIF_DATE="2023:08:15 14:30:00"; exiftool -P -DateTimeOriginal="$EXIF_DATE" -CreateDate="$EXIF_DATE" -ModifyDate="$EXIF_DATE" ./file.jpg
```

GPS part
```
exiftool -P -GPSDateStamp="2023:08:15" -GPSTimeStamp="14:30:00" ./file.jpg
```

- `-P` - keep original
```
File Modification Date/Time     : 2025:01:09 20:58:57+01:00
File Access Date/Time           : 2025:12:20 13:00:35+01:00
```

Can't be changed:
```
File Inode Change Date/Time     : 2025:12:20 13:00:33+01:00
```

### How to erase all metadata from jpeg
```
exiftool -all= ./file.jpg
```

### How to erase all geo metadata
```
exiftool -gps:all= ./file.jpg
```

### How to erase all dates (Profile Date Time is not writable:/)
```
exiftool -AllDates= ./file.jpg
```

## [MP4] Useful exiftool commands

## CHange dates in mp4
```
EXIF_DATE="2023:08:15 14:30:00";
exiftool  -P \
  -DateTimeOriginal="$EXIF_DATE" \
  -CreateDate="$EXIF_DATE" \
  -ModifyDate="$EXIF_DATE" \
  -TrackCreateDate="$EXIF_DATE" \
  -TrackModifyDate="$EXIF_DATE" \
  -MediaCreateDate="$EXIF_DATE" \
  -MediaModifyDate="$EXIF_DATE" \
  ./file.mp4
```

