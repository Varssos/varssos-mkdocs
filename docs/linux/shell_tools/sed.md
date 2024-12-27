# sed

[AGH SED tutorial](https://home.agh.edu.pl/~wojnicki/didactic/sed1line.txt)

!!! note

    You should put `\` backslash before chars like `[`  More info [here](<https://www.baeldung.com/linux/bash-escape-characters>)

## Common sed usage

### Get value between two strings

Get `0` between `[` `]` from `fstab.@mount[0].target='/mnt/sdcard'`

```bash
echo "fstab.@mount[0].target='/mnt/sdcard'" | sed -E 's/.*\[(.*)\].*/\1/'
```

Same but from `uci show fstab` and in reverse order
```bash
uci show fstab | grep "target='/mnt/sdcard'" | sed -E 's/.*\[(.*)\].*/\1/' | sort -r
```
    
### Remove first n charactrs from each line
```bash
sed -i -r 's/^.{3}//' gamepad.py
```

### Replace text in all files recursively

```bash
grep -rl oldtext . | xargs sed -i 's/oldtext/newtext/g'
```

    

Linux course examples
=====================

Tutorial:
<https://www.digitalocean.com/community/tutorials/the-basics-of-using-the-sed-stream-editor-to-manipulate-text-in-linux>

Download the [BSD.txt](./BSD.txt) file for exercises



1.  Display only processed lines (-n) `sed -n 'p' BSD`
2.  Print the first line `sed -n '1p' BSD`
3.  Print lines from 1 to 5 `sed -n '1,5p' BSD`
4.  Print from line 1 and the next 4 lines `sed -n '1,+4p' BSD`
5.  Print lines starting from 1 and every 4th line, i.e., 1,5,9.. `sed -n '1~4p' BSD`
6.  Delete every other line starting from 1 `sed '1~2d' BSD`
7.  Delete every other line starting from 1 and save to another file `sed '1~2d' BSD > everyother.txt`
8.  Delete every other line starting from 1, but in-place editing `sed -i '1~2d' everyother.txt`
9.  Delete every other line starting from 1, overwrite with backup `sed -i.bak '1~2d' everyother.txt`
10. Replace 'ma' with 'MA' in the test file `sed -i 's/ma/MA/' test` or vice versa `sed -i 's_MA_ma_' test` BUT, ONLY THE FIRST OCCURRENCE IN EACH LINE
11. Replace all occurrences of 'on' with 'forward' `sed 's/on/forward/g' song.txt`
12. Replace the second occurrence of 'on' with 'forward' `sed 's/on/forward/2' song.txt`
13. Replace from the second occurrence of 'on' with 'forward' `sed 's/on/forward/2g' song.txt`
14. Find 'SiNgInG' regardless of letter case and replace with 'saying' `sed 's/SiNgInG/saying/i' song.txt`
15. Find 'at' and everything before including 'at' and replace with 'REPLACED' `sed 's/^*at/REPLACED/' song.txt`
16. Find 'at' and everything before including 'at' enclosed in parentheses ( ) `sed 's/^.*at/(&)/' song.txt`
17. Swap the first and second word in each line `sed 's/\([^ ][^ ]*\) \([^ ][^ ]*\)\2 \1/' song.txt`
18. Lines with the string 'bash' `sed -n '/bash/p' /etc/passwd`
19. Everything except the third line `sed -n '3!p' /etc/passwd`

Exercise 1
==========

1.  Display the first 20 lines of a file. `sed -n '1,20p' /etc/passwd`
2.  Display the 4th line of text. `sed -n '4p' /etc/passwd`
3.  Comment out lines 5 to 10 in a file. `sed '5,10 s|.*|//&|' test`
4.  Comment out lines 5 to the end of the file. `cat -n /etc/passwd | sed '5,$ s|.*|//&|'`
5.  Number the lines in a file. `sed = /etc/passwd`
6.  Remove all empty lines in a file. `sed -i '/^$/d' test`
7.  Replace all round brackets with square brackets in a file. `cat test | sed -re 's/[(]/[/g' | sed -re 's/[)]/]/g'`
8.  Remove all dots and commas from the text. `cat pliktest | sed -e 's/,//g' -e 's/\.//g'`
9.  Replace all lowercase 'a' with uppercase 'A' in a file. `sed -e 's/a/A/g' test`

Exercise 2
==========

Here is a [article.txt](./article.txt) file. Perform the following tasks for it:

1.  Delete \<article\> and \</article\>. `sed -e 's|<article>||g' -e 's|</article>||g' article` (use \| because / appears in the pattern)
2.  Replace \<title\> with Title:, and remove \</title\>. `sed -i -e 's|<title>|Title: |g' -e 's|</title>||g' article`
3.  Delete \<para\> and \</para\>. `sed -i -e 's|<para>||g' -e 's|</para>||g' article`
4.  Replace \<emphasis\> and \</emphasis\> with \* character. `sed -i -e 's|<emphasis>|*|g' -e 's|</emphasis>|*|g' article`
