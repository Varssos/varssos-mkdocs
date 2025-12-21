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
The most important date for Immich/Google Photos etc is `DateTimeOriginal`
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

### How to find files with .jpg extension which are not JPEG

```
find . -type f \( -iname '*.jpg' -o -iname '*.jpeg' \) -exec file {} + | grep -v JPEG
```

### How to find jpegs which has format error

```
find . -type f \( -iname '*.jpg' -o -iname '*.jpeg' \) -exec sh -c 'exiftool "$1" 2>&1 | grep -q "JPEG format error" && echo "$1"' _ {} \;
`


## [MP4] Useful exiftool commands

### Change dates in mp4
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
- `-overwrite_original` - to work on original file


### Automated changing dates in mp4
Assumptions:
```
├── 1998
├── 2002
├── 2003
├── 2004
├── 2008
├── 2009
└── set_date_from_csv_to_mp4_in_local_dirs.sh
```

- In each dir there is a `date.csv` file with csv format:
```
ABC.mp4;1998:12:19 19:39:00
XYZ.mp4;1998:12:14 19:00:00
```

- `set_data_from_csv_to_mp3_in_local_dirs.sh`:

```
#!/usr/bin/env bash

# Loop through all subdirectories
for DIR in */; do
  # Only process directories
  [[ ! -d "$DIR" ]] && continue

  CSV_FILE="${DIR}date.csv"

  # Skip directories without date.csv
  if [[ ! -f "$CSV_FILE" ]]; then
    continue
  fi

  echo "📂 Processing directory: $DIR"

  # Read CSV inside this directory
  while IFS=';' read -r FILE EXIF_DATE; do
    # Skip empty lines
    [[ -z "$FILE" || -z "$EXIF_DATE" ]] && continue

    FILE_PATH="${DIR}${FILE}"

    # Check if referenced file exists
    if [[ ! -f "$FILE_PATH" ]]; then
      echo "❌ File not found: $FILE_PATH"
      continue
    fi

    echo "▶ Setting date $EXIF_DATE for $FILE_PATH"

    exiftool -api LargeFileSupport=1 \
      -P -overwrite_original \
      -DateTimeOriginal="$EXIF_DATE" \
      -CreateDate="$EXIF_DATE" \
      -ModifyDate="$EXIF_DATE" \
      -TrackCreateDate="$EXIF_DATE" \
      -TrackModifyDate="$EXIF_DATE" \
      -MediaCreateDate="$EXIF_DATE" \
      -MediaModifyDate="$EXIF_DATE" \
      "$FILE_PATH"

  done < "$CSV_FILE"

done
```


Or script in the same file as date.csv
```
#!/usr/bin/env bash

# Loop through all subdirectories
for DIR in */; do
  # Only process directories
  [[ ! -d "$DIR" ]] && continue

  CSV_FILE="${DIR}date.csv"

  # Skip directories without date.csv
  if [[ ! -f "$CSV_FILE" ]]; then
    continue
  fi

  echo "📂 Processing directory: $DIR"

  # Read CSV inside this directory
  while IFS=';' read -r FILE EXIF_DATE; do
    # Skip empty lines
    [[ -z "$FILE" || -z "$EXIF_DATE" ]] && continue

    FILE_PATH="${DIR}${FILE}"

    # Check if referenced file exists
    if [[ ! -f "$FILE_PATH" ]]; then
      echo "❌ File not found: $FILE_PATH"
      continue
    fi

    echo "▶ Setting date $EXIF_DATE for $FILE_PATH"

    exiftool -api LargeFileSupport=1 \
      -P -overwrite_original \
      -DateTimeOriginal="$EXIF_DATE" \
      -CreateDate="$EXIF_DATE" \
      -ModifyDate="$EXIF_DATE" \
      -TrackCreateDate="$EXIF_DATE" \
      -TrackModifyDate="$EXIF_DATE" \
      -MediaCreateDate="$EXIF_DATE" \
      -MediaModifyDate="$EXIF_DATE" \
      "$FILE_PATH"

  done < "$CSV_FILE"

done
```