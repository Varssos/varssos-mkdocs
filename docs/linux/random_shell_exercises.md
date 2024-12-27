# Random linux shell exercises


1.  Using the locate program, find all entries that have the word "mozilla" in their name.

    ??? example
        ```bash
        locate "mozilla"
        ```

2.  Using the locate program, find all entries that have the word "mozilla" in their name and are located in the subdirectories of the /usr directory.

    ??? example
        ```bash
        locate /usr/ --basename "mozilla"
        ```


3.  Using the find program, find all files that have the word "mozilla" in their name and are located in the subdirectories of the /usr directory.

    ??? example
        ```bash
        find /usr/ -name "mozilla"ls -alSr | grep -v ^d
        ```


4.  Using the find program, find all directories with the name "bin" that are located in the /usr directory.

    ??? example
        ```bash
        find /usr/ -name "bin" -type d
        ```


5.  Copy all regular files with a size between 10 and 100 bytes from the /usr/bin directory to the /tmp/files directory (use the find command with the -exec parameter).

    ??? example
        ```bash
        find /usr/bin -type f -size +10c -size -100c -exec cp {} /tmp/files/ \; -print 
        ```


6.  In the home directory, create a file named plik.txt and check its access permissions.

    ??? example
        ```bash
        touch plik.txt
        ls -la
        ```


7.  Add write permission for the group to the file plik.txt.

    ??? example
        ```bash
        sudo chmod g+w plik.txt
        ```


8.  Remove write permission for the owner from the file plik.txt.

    ??? example
        ```bash
        sudo chmod u-r plik.txt
        ```


9.  Add execute permission for all users to the file plik.txt.

    ??? example
        ```bash
        sudo chmod +x plik.txt
        ```


10. Restore the original permissions for the file plik.txt using numeric notation.

    ??? example
        ```bash
        chmod 644 test.txt
        ```


11. Create a symbolic link named plik2.txt to the file plik.txt in the home directory.

    ??? example
        ```bash
        ln -s plik.txt plik2.txt
        ```


12. Create a symbolic link to the directory kat1/kat2 named abc in the home directory.

    ??? example
        ```bash
        ln -s kat1/kat2 abc
        ```


13. Display the file /etc/passwd with pagination, assuming each page has 5 lines of text.

    ??? example
        ```bash
        more -5 /etc/passwd
        ```


14. Use the cat command to create a file named tekst3 that consists of the contents of the file tekst1, a string entered from standard input (keyboard), and the contents of the file tekst2.

    ??? example
        ```bash
        cat tekst1 > tekst3 && cat >> tekst3 && cat tekst2  >> tekst3
        ```


15. Display the first 5 lines of all files in your home directory in a way that their names are not displayed.

    ??? example
        ```bash
        head -5 * 2>/dev/null -q
        ```


16. Display lines 3, 4, and 5 from the file /etc/passwd.

    ??? example
        ```bash
        cat -n /etc/passwd | head -5 | tail -3
        ```


17. Display lines 7, 6, and 5 from the end of the file /etc/passwd.

    ??? example
        ```bash
        tac  /etc/passwd | head -7 | tail -3
        ```


18. Display the contents of /etc/passwd in a single line.

    ??? example
        ```bash
        cat /etc/passwd | tr '\n' ' '
        ```


19. Use the tr filter to modify a file by placing each word on a separate line.

    ??? example
        ```bash
        cat pliktest | tr ' ' '\n' > pliktest2
        ```


20. Count all files in the /etc directory and its subdirectories.

    ??? example
        ```bash
        find /etc/ -type f | wc -l
        ```


21. Write a command that counts the total number of characters in the first three lines of the file /etc/passwd.

    ??? example
        ```bash
        head -3 /etc/passwd | wc -c
        ```


22. Display a list of file names in the current directory, converting all lowercase letters to uppercase.

    ??? example
        ```bash
        ls | tr [:lower:] [:upper:]
        ```


23. Display a list of access permissions, file sizes, and names of files in the current directory.

    ??? example
        ```bash
        ls -al | tr -s ' '| cut -f1,5,9 -d ' ' | tr ' ' '\t'
        ```


24. Display a list of files in the current directory, sorted by file size.

    ??? example
        ```bash
        ls -la | tr -s ' ' | sort -k 5 -n
        ls -alSr | grep -v ^d
        ```


25. Display the contents of the file /etc/passwd sorted by UID numbers in descending order.

    ??? example
        ```bash
        cat /etc/passwd | sort -t : -k 3 -n -r
        ```


26. Display the contents of the file /etc/passwd sorted first by GID numbers in descending order, and then by UID numbers.

    ??? example
        ```bash
        cat /etc/passwd | sort -t : -k4 -k3 -n -r
        ```


27. Provide the number of files for each user.

    ??? example
        ```bash
        find /home/student -type f | wc -l
        find ~ -type f -user student | wc -l
        ```


28. Generate a statistics of access permissions (for each access permission, indicate how many times it has been assigned).

    ??? example
        ```bash
        ls -al | cut -f1 -d ' ' | grep -v total | sort | uniq -c
        ```


29. Provide the names of the three smallest files in the directory, sorted by name.

    ??? example
        ```bash
        ls -alSr | grep -v total | head -3 | sort -k 9
        ```


30. Provide the names of the top five users with the highest number of running processes.

    ??? example
        ```bash
        ps aux | sort | cut -f1 -d ' ' | grep -v USER | uniq -c | head -5
        ```


31. Display the contents of the three largest subdirectories in the current directory.

    ??? example
        ```bash
        ls -al `sudo du | sort -n -r | head -4 | tail -3 | cut -f2`
        ```


32. Display the names of users who use an interpreter other than bash by default.

    ??? example
        ```bash
        cat /etc/passwd | grep -v bash | cut -f1 -d:
        ```


33. Display the names of all header files used in the files of the current directory.

    ??? example
        ```bash
        find ./ -type f -exec cat {} \; | grep "^#include" | cut -f2 -d ' ' | sort | uniq -c | sort -n -r
        ```


34. Display statistics of used commands (without arguments) in the form of a sorted list: count command (use the history command).

    ??? example
        ```bash
        history | tr  -s ' ' | cut -f3 -d ' ' | sort | uniq -c | sort -n -r
        ```


35. From the given name `rapidjson_1.1.0-1_mips_24kc.ipk`, extract the file name up to the first delimiter `_`.

    ??? example
        ```bash
        echo "rapidjson_1.1.0-1_mips_24kc.ipk" | cut -d '_' -f 1
        ```
