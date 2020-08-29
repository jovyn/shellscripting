## SED
------------------------------------------------------

*  SED is a stream editor.

#### Structure :
* sed OPTIONS ... [SCRIPT] [INPUTFILE....]
* cat [INPUTFILE] | sed OPTIONS ... [SCRIPT]
* SCRIPT:
    * ``` [addr]X[options] ```
        * ``` [addr] ``` - can be a single line, number, a regular expression, or range of lines. If ``` [addr] ``` is specified, the command X will be executed only on the matched lines.
        * ``` X ``` - single-letter sed command.
        * Additional ```[options]``` for sed command.  

    *  Eg:  ```sed '30,35d' infile.txt > outfile.txt ```
        * Delete range of lines Line 30 - line 35 from infile and save output to outfile.txt
        * ```d``` - is the delete command
* Sed by default does not alter the inputfile, only prints. 
* Sed accepts one single command at a time. To use multiple commands use ``` -e ``` option

#### Example file to be used throughout : emp.txt

        cat emp.txt

        output:
        Name Age Unit
        Ant  23  IT
        Bec  25  HT
        Red  34  CEO
        Dua  32  FIN
        Wui  29  PR
        Wui  29  PR
        Van  27  Dev
        Kim  26  Dev

#### Sed Commands :

* ``` a ``` -  Append text after a line.
    * eg: Append after IT some text : ```  sed '/IT/a QWE  ## XY' emp.txt ```

        output:
        Name Age Unit
        Ant  23  IT
        QWE  ## XY
        Bec  25  HT
        Red  34  CEO
        Dua  32  FIN
        Wui  29  PR
        Van  27  Dev
        Kim  26  Dev

* ``` i 'text' ``` - insert text before a line
    * eg: Insert before IT some text : ```  sed '/IT/i QWE  ## XY' emp.txt ```

        output:
        Name Age Unit
        QWE  ## XY
        Ant  23  IT
        Bec  25  HT
        Red  34  CEO
        Dua  32  FIN
        Wui  29  PR
        Van  27  Dev
        Kim  26  Dev


* ``` d ``` - delete the pattern
    * eg: Delete all lines containing 'Dev' : ```  sed '/Dev/d' emp.txt ```

        output:
        Name Age Unit
        Ant  23  IT
        Bec  25  HT
        Red  34  CEO
        Dua  32  FIN
        Wui  29  PR


* ``` p  ``` - print the pattern.
    * eg:  ```  sed -n '/Dev/p' emp.txt ``` '-n' is used to explicitly disable print all, as sed prints all by default. 
            
            output:
            Van  27  Dev
            Kim  26  Dev

    * eg: "Print 2nd line"  ```sed -n '2p' emp.txt ``` 

            output:
            Ant  23  IT

    * eg: "Print from line 2 to 5"  ```sed -n '2,5p' emp.txt ``` 

            output:
            Ant  23  IT
            Bec  25  HT
            Red  34  CEO
            Dua  32  FIN
    
* ``` c ``` - Change command used to change lines.
    * eg: Change all lines with 'Dev' to XXXXXX... - ```  sed '/Dev/c xxxxxxxxxxxxxxxxxxxxxxx' emp.txt ```

        output:
        Name Age Unit
        Ant  23  IT
        Bec  25  HT
        Red  34  CEO
        Dua  32  FIN
        Wui  29  PR
        xxxxxxxxxxxxxxxxxxxxxxx
        xxxxxxxxxxxxxxxxxxxxxxx

* ``` q[exit-code] ``` - exit sed without processing any more commands or input.
    * eg:  ```sed '/Bec/q2' emp.txt``` will quit once the search pattern matches and will receive exit status code 2. ```echo $?``` gives an output of ``` 2```

        output:
        Name Age Unit
        Ant  23  IT
        Bec  25  HT


* ``` s/regexp/replacement/[flags]``` - (substitute) Match the regex against the content of the pattern space. If found replace matched string with 'replacement'. Use ```g ``` to substitute globally. 
    * Eg: ``` echo "1110000111" | sed 's/000/XXX/' ``` --> output:  ``` 111XXX0111 ```
    * Eg: ```  echo "The quick brown fox  , trots away     ...  " | sed 's/[[:space:]]/#/g' ```. This will replaces all spaces globally. Output : ``` The#quick#brown#fox##,#trots#away#####...## ```
    * Eg: ``` echo "The quick brown fox  , trots away     ...  " | sed 's/[[:space:]]/#/ ``` . Without the global flag (g) will simply replace the first instance. --> output: ``` The#quick brown fox  , trots away     ...   ```
    * Eg: Replace specific lines in a file. ``` sed '8s/Dev/Manager/' emp.txt ``` --> Replace 'Dev' with 'Manager' on the 8th line.

            output:
            Name Age Unit
            Ant  23  IT
            Bec  25  HT
            Red  34  CEO
            Dua  32  FIN
            Wui  29  PR
            Van  27  Dev
            Kim  26  Manager
    
    * Eg: Replace  all lines we use range ``` 1,$ ```. Use command ``` sed '1,$s/e/EE/' emp.txt ``` to replace all instances of 'e' with 'EE'.

            output:
            NamEE Age Unit
            Ant  23  IT
            BEEc  25  HT
            REEd  34  CEO
            Dua  32  FIN
            Wui  29  PR
            Van  27  DEEv
            Kim  26  DEEv


* Command-Line- Options:
    * ``` -n ``` - disable automatic printing; sed produced output when explicitlytold via the p command.
    * ``` -e script ``` - add script
        * eg:  Search some text and quit with exit code 2 : ``` sed -ne '/CEO/p' -ne '/CEO/q2' emp.txt  ``` and ``` echo $? ``` will return 2.

            output:
            Red  34  CEO

        * eg: Print "000- before/after -000" before and after lines containing 'Dua' :  ``` sed -e '/Dua/a 000- after -000' -e '/Dua/i 000- before -000' emp.txt  ```

            output:
            Name Age Unit
            Ant  23  IT
            Bec  25  HT
            Red  34  CEO
            000- before -000
            Dua  32  FIN
            000- after -000
            Wui  29  PR
            Van  27  Dev
            Kim  26  Dev

    * ``` -r ``` - use extended regular expressions rather than basic regular expressions.

    * ``` -i ``` - Use this flag to modify the input file. 
        * We take a copy of emp.txt as emp2.txt and perform the following :  ```  sed -ni '/Wui/p' emp2.txt ```
        * ``` cat emp2.txt ``` :

            output:
            Wui  29  PR

        
    *  ``` e ``` To run scripts. This is different than ``` -e ```
        * ``` sed '/Name/e echo -n "Date:"; date' emp.txt ```  - Run and print date before 'Name'.

                output:
                Date:Sat Aug 29 08:00:34 IST 2020
                Name Age Unit
                Ant  23  IT
                Bec  25  HT
                Red  34  CEO
                Dua  32  FIN
                Wui  29  PR
                Van  27  Dev
                Kim  26  Dev

        * ``` sed '1 e echo -n "Date:"; date' emp.txt ``` - Print date on the first line.

            output:
            Date:Sat Aug 29 08:05:41 IST 2020
            Name Age Unit
            Ant  23  IT
            Bec  25  HT
            Red  34  CEO
            Dua  32  FIN
            Wui  29  PR
            Van  27  Dev
            Kim  26  Dev

        * ```  sed '1,$ e echo -n "Date:"; date' emp.txt ``` - Print date before every line.

            output:
            Date:Sat Aug 29 08:16:09 IST 2020
            Name Age Unit
            Date:Sat Aug 29 08:16:09 IST 2020
            Ant  23  IT
            Date:Sat Aug 29 08:16:09 IST 2020
            Bec  25  HT
            Date:Sat Aug 29 08:16:09 IST 2020
            Red  34  CEO
            Date:Sat Aug 29 08:16:09 IST 2020
            Dua  32  FIN
            Date:Sat Aug 29 08:16:09 IST 2020
            Wui  29  PR
            Date:Sat Aug 29 08:16:09 IST 2020
            Van  27  Dev
            Date:Sat Aug 29 08:16:09 IST 2020
            Kim  26  Dev
            Date:Sat Aug 29 08:16:09 IST 2020

        * 

#### Examples:
