# awk

- [tutorialspoint awk](https://www.tutorialspoint.com/awk/index.htm)
- [linuxhandbook](https://linuxhandbook.com/awk-command-tutorial/)

## AWK - glossary

!!! note

    FS - field separator. Default: space

    NF - number of fields ( in the current record/line)

    NR - number of the current records (lines)

    FNR - number of the current records (lines) in the current file

    OFMT - output format for numbers. Default: %.6g

    OFS - output field separator. Default: space

    ORS - output record separator. Default: newline

    RLENGTH - length of the string matched by the match function

    RS - record separator. Default: newline

    RSTART - index of the string matched by the match function

    SUBSEP - subscript separator. Default: \034

    $0 - whole line

    $n - n-th field in the current record/line


## AWK - print at program start-up

```bash
awk 'BEGIN {print "Hello world!"}'
```


## AWK - print line which starts with a Zosia word, comma separated

```bash
awk '/^Zosia/ { print "Hello " $0; }' FS=,  input.txt
```

## AWK - print at the end of the program

```bash
awk 'END { print "END" }' input.txt
```


## AWK - combine BEGIN, process text and END

```bash
awk 'BEGIN { print "Begin to process text" } /^Zosia / { print "Hello " $0; } END { print "END" } ' FS=,  input.txt
```

    

## AWK - assign variable

```bash
awk -v name=Jerry 'BEGIN { printf "Hello %s!\n", name}'
# Hello Jerry!
```

    

## AWK - dump program variables to default awkvars.out

```bash
awk --dump-variables -v name=Jerry 'BEGIN { printf "Hello %s!\n", name}'
```

    

## AWK - print column with description

```bash title="marks.txt"
1)  Amit    Physics  80
2)  Rahul   Maths    90
3)  Shyam   Biology  87
4)  Kedar   English  85
5)  Hari    History  89
```

```bash
awk '{printf "Name: %s, Subject: %s, score: %s\n", $2, $3, $4}' marks.txt
```

    

## AWK - count lines which has \'a\'

```bash
awk '/a/ {++cnt} END {print "Count = ", cnt}' marks.txt
```

    

## AWK - print line which has less than 23 characters

```bash
awk 'length($0) < 23' marks.txt
# or only 3rd column
awk 'length($0) < 23 {print $3}' marks.txt
```

    

## AWK - show line which contain more than 2 fields in line
```bash
echo -e "One Two\nOne Two Three\nOne Two Three Four" | awk 'NF>2'
```

    

## AWK - use NR to print line number
```bash
echo -e "One Two\nOne Two Three\nOne Two Three Four" | awk '{printf "%d: %s\n", NR, $0}'
```

    

## AWK - get max from variables
```bash
awk 'BEGIN { a = 10; b = 20; (a > b) ? max = a : max = b; print "Max = " max}'
```

    

## AWK - string concatenation
```bash
awk 'BEGIN { str1 = "Hello, "; str2 = "world"; str3= str1 str2; print str3 }'
```

    

## AWK - print line which (not)contain pattern 9
```bash
awk '$0 ~ 9' marks.txt
# or not
awk '$0 !~ 9' marks.txt
```
    

## AWK - regular expressions
```bash
# match single character `f*n`
echo -e "cat\nbat\nfun\nfin\nfan" | awk '/f.n/'
# match start of line with 'The'
echo -e "This\nThat\nThere\nTheir\nthese" | awk '/^The/'
# match end of line with letter 'n'
echo -e "knife\nknow\nfun\nfin\nfan\nnine" | awk '/n$/'
# match Call or Tall
echo -e "Call\nTall\nBall" | awk '/[CT]all/'
# exclude Call or Tall
echo -e "Call\nTalll\nBall" | awk '/[^CT]all/'
# match Call or Talk
echo -e "Call\nTalk\nBall\nSmall\nShall" | awk '/Call|Talk/'
# match Colour and Color. Make u optional. Zero or one occurence
echo -e "Colour\nColor" | awk '/Colou?r/'
# match ca, cat, catt. Make t optional. Zero or more occurence
echo -e "ca\ncat\ncatt" | awk '/cat*/'
# match cat, catt. One or more occurence 't'
echo -e "ca\ncat\ncatt" | awk '/cat+/'
# match Apple Juice or Apple Cake (grouping with ())
echo -e "Apple Juice\nApple Pie\nApple Tart\nApple Cake"  | awk '/Apple (Juice|Cake)/'
```

    
