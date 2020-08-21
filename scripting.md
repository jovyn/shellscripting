### Scriptitng Basics
----------------------------------------------------

* ``` #!/bin/bash ``` Sha-Bang. # -Sharp !- Bang   /bin/bash - invoke bash interpreter. If this line is not added all scripts would be run by ``` /bin/bash  script.sh```
* ``` ls -l /bin/sh ``` Default shell (eg> in Ubuntu : /bin/sh  >> dash )
* ``` ./file.sh ``` Execute the script in current directory.
* ``` echo $PATH ``` If file.sh path defined in PATH then file.sh can be invoked anywhere by typing the file name.
* ``` export PATH=$PATH:(path/of/file) ``` to export path. Eg. ``` export PATH=$PATH:$(pwd) ```

#### Variables
* 3 Ways to assign values to a variable
    * ``` VAR=value ``` Explicit definition (no spaces after =. If space is added bash sees it as 2 arguments after VAR)
        * PATH=/var/lib
        * Count =12
        * msg="hello world"
    * ``` read VAR ``` Read Command
         eg: ```echo -n "Enter age:"``` 
            ```read AGE```
            ``` echo -n "Age is $AGE"```
        * ``` read -p "Name: " NAME  ``` Read value 
        * ``` read -sp "Pword: " PASS ```  Read value but Entered value is NOT displayed
        *  ``` read HOST < /etc/hostname ``` Read the value of file /rtc/hostname to HOST var. Equal to assiging the output of cat /etc/hostname to the variable
    * ``` VAR=$(cmd) eg: VAR=$(pwd) ``` Command substitution
        * ```VAR=$(cmd) eg: VAR=$(pwd)``` $ prepend
        * ```VAR=`cmd` eg: VAR=`pwd`.``` using backticks
* Accessing variables
    * Access variables by prepending '$' 
    * eg:``` COUNT =10 echo "counter = $COUNT " ```

#### Math

* let
    * ``` NUMBER=5   let Result=NUMBER+5 ```
    * Increment ``` let NUMBER++ ``` ( i.e let NUMBER+=5)
    * Decrement ``` let NUMBER-- ``` ( i.e let NUMBER-=5)
* (()) - Eg:  ``` RESULT=$(( NUMBER + 5 )) ```
* [] - Eg: ``` RESULT=$[ NUMBER + 5 ] ```
* expr -- Need to add spaces around math operators
    * eg: ``` RESULT=$(expr $NUM1 + $NUM2) ```
    * eg: ``` RESULT=`expr $NUM1 + $NUM2` Alternate approach ```
* bc  - OPERATE FLOATING POINT. Put Mathematical expression in "" and | bc
    * Eg: ``` AREA=`echo "2 *$RADIUS * 3.14"|bc` ```

#### Arguments
* Passing args to scripts
* Passing args into function
* Eg: Calling script with args ``` ./arg.sh A1 A2 A3```
* Arguments - Accessing them from scripts
    * ```$0 ```-  script name
    * ```$1 ```- 1st arg
    * ```$2 ```- 2nd arg
    * ```$n ```- Nth arg
    * ```"$@" ```- all args, expands as "$1" "$2" "$3" etc .
    * ```"$*" ```- all args, expand as one string "$1c$2c$3c" where c is the first character of IFS (internal dield space) usually its space.
        * View default IFS first char ``` set | grep ^IFS ```
        *  To change IFS simply use var IFS="<char>" .Eg: ```IFS=","``` to change IFS char to``` ,```
    * ```$# ```- Args count.

#### Redirection & Piping
* STDIN (0) - STD input (data provided to the program)
* STDOUT (1) - STD output (what program prints.. default to the terminal)
* STDERR (2) - STD error (error msgs program prints)
* Redirection ``` > ``` or ```>>``` to append
    * Eg: ```cat file.txt > output.txt ```-- Redirect std output
    * Eg: ```cat file.txt 1> output.txt ```-- (Same as above) Redirect std output
    * Eg:``` cat file.txt 2> output.txt ```-- Redirect std error
    * Eg: ```cat file.txt 1> output.txt 2> error.log ```-- Redirect std out and std error to 2 files
    * Eg: ```cat file.txt 1> output.txt 2>&1 ```-- Redirect std err stream to std out stream 
    * Eg: ```cat file.txt &> output.txt ```-- Redirect std out and std error to one file
    * ``` wc -l file.txt ```  Vs ``` wc -l < file.txt ```
* Piping ```|``` 
    * sending output of one cmd to another
    * eg: ``` cat file | head -5 | tail -2 wc -l  ```
* Exit Status ``` echo $? ```
    * 0 - successful
    * non-zero - not successful
    * exit 0,  exit1 .... exit 255

####  If Else
        if [cond] 
        then
        statements
        fi  
* AND && , OR || , NOT !
* if elif else 

#### For Loops
* For Eg: ``` for p in a b c; do echo $p; done ```
* For on string ``` $STR=A cool char``` will print each word on a newline ``` for p in $STR; do echo $p; done ```. And if ``` for p in "$STR"; do echo $p; done ``` output of $STR will be printed in one line. The default IFS is space ``` IFS=$'\t\n' ``` this can be changed and For will behave accordingly.
* Eg. Print all txt files ``` for p in *.txt; do echo $p; done ```
* Eg. Range ``` for p in {1..10}; do echo $p; done ``` loop through 1 to 10
* Eg. Loop through arguments ``` for ARG in "$@"; do echo $ARG; done ```
* C-Style Incremental and decremental ``` for ((i=1; i<=12; i++)); do echo &i; done```

#### While Loop
* Syntax ``` while [cond]; do [action]; done ``` Eg: ``` while true; do ping 8.8.8.8; done ```
* Reading Files with While Loop :
    * 1. ``` while read line; do echo $line; done < "$FILENAME" ```
    * 2. ``` cat "$FILENAME" | while read line; do echo $line; done ```

#### Case 
    case "$VAR" in 
    "$cond1")
      commands...
      ;;
    "$cond2")
      commands..
      ;;
     *)
      commands
      ;;
    esac  
* shift https://tldp.org/LDP/Bash-Beginners-Guide/html/sect_09_07.html 

#### Math Operands
* ``` -eq ```
* ``` -ne ```
* ``` -gt ```
* ``` -lt ```
* ``` -ge ```
* ``` -le ```

#### String Comparision 
* Compare 2 strings (notice the spaces)
    * ``` [ "$Str1" = "$Str2" ] ``` equals
    * ``` [ "$Str1" != "$Str2" ] ``` not equals 
    * ``` [ "$Str1" = "Hello" ] ```
    * ``` [ "$Str1" != "Hello" ] ```
    * ``` [[ $Str1 = $Str2 ]] ``` equals with []
    * ``` [[ $Str1 != $Str2 ]] ``` not equals  []
    * ``` [[ $Str1 = Hello ]] ```
    * ``` [[ $Str1 != Hello ]] ```   
    * ``` [[ $Str1 = "Hello" ]] ```  [] and "string"
    * ``` [[ $Str1 != "Hello" ]] ```   
* Test if string is empty
    * ``` [ -z "$Str1" ] ``` - returns true if Str1 holds an empty string
    * ``` [ -n "$Str1" ] ``` - rteturns if the Str1 holds a non-empty string
    * ``` [[ -z $Str1 ]] ``` 
    * ``` [[ -n $Str1 ]] ```
* Alphabetically compare 2 strings
    * ``` [[ $Str1 > $Str2 ]] ```
    * ``` [[ $Str1 < $Str2 ]] ```

* Wildcards
    * ```?``` Single character eg: hel? (hell,held,help ..etc)
    * ```*``` Any nos. of characters eg: hel* (helll, helljdkljd, hel12 .. etc)
    * ```[]``` Single character from a range. eg: hel[pqr]; hel[4-7] (help, helq. helr) (hel4, hel5, hel6, hel7)
    * ```{}``` Comma seperated terms. eg: {*.txt, *.exe} (a.exe, b.txt, c.txt .. etc)
    * ```[!]``` Any Character not listed eg: hel[!p] (hell, helo, helx .. etc)
    * Gobbling patterns (character classes)
        * ```[:upper:]``` - Uppercase character
        * ```[:lower:]``` - Lowercase character
        * ```[:alpha:]``` - Alphabetic character
        * ```[:digit:]``` - Number character
        * ```[:alnum:]``` - Alphanumeric character
        * ```[:space:]``` - Whitespace character (space, tab, newline)
    * Wildcards in string Comparision ```[[ $STR == <pattern> ]] ```
        * eg:``` [[ $STR == *.sh ]]```
        * eg:``` [[ $STR == log[1-9].txt ]]```
        * eg:``` [[ $STR == conf* ]]```

* RegEx
    * ``` . ``` Any single Character eg: hel. (help, hell, helo .. etc)
    * ``` * ``` Preceding Character must match 0 or more times eg: he*lo (hlo, helo, heeeelo, heelo .. etc)
    * ``` ? ``` Preceding Character must match 1 or 0 times eg: he?lo (helo, hlo)
    * ``` ^ ``` Start of the line marker eg: ^Hello (Line starting with Hello)
    * ``` $ ``` End of the line marker eg: hello$ (Line ending with hello)
    * ```[]``` Any of the characters enclosed in [] eg: Hel[lop] (Hell, Helo, Help)
    * ```[-]``` Any of the characters within the range eg: file[1-3] (file1, file2, file3)
    * ```[^]``` Any of the characters except the ones enclosed in [] eg: file[^13] (file0, file2, file4 ...etc)
    * ``` + ``` Preceding item must match 1 or more times eg: file+ (file, files, file1, filex ... etc)
    * ```{n}``` Preceding item must match n times eg: [0-9]{3} (Any 3 digit no .. 111, 134, 098, 678 .. etc)
    * ```{n, }``` Preceding item must match at least n times eg: [0-9]{3} (Any 3 or more digit no .. 111, 134, 0981, 67887, 71236 .. etc)
    * ```{n,m}``` Minimum and maximum nos of times the preceding item must match. eg: [0-9]{2,3} (Any 2 or 3 digit no .. 111, 134, 98, 78 .. etc)
    * ``` \ ``` Escape Character eg: he\*ro (he*ro)
    * Reg Ex Character classes :
        * ```[:upper:]``` - Uppercase character
        * ```[:lower:]``` - Lowercase character
        * ```[:alpha:]``` - Alphabetic character
        * ```[:digit:]``` - Number character
        * ```[:alnum:]``` - Alphanumeric character
        * ```[:space:]``` - Whitespace character (space, tab, newline)
    * Reg Ex in Bash: ```[[ $STR =~ $REGEX ]] ```
        * eg: ``` REGEX="http://.*\.jpg" ``` (eg: http://images.jpg)
        * ```${BASH_REMATCH[0]} ```- Part of the STR which matches REGEX eg: (http://images.jpg)
        * ```${BASH_REMATCH[1]} ```- Part of the REGEX which is enclosed in the first parentheses eg: ```REGEX="http://(.*)\.jpg ```which reperesents as "images"
    
* File System Related Tests:
    * ```[ -e $VAR ] ``` - True if variable holds an existing file or dir.
    * ```[ -f $VAR ] ``` - True if variable holds an existing regular file.
        * eg: ``` if [-f $FILE]; then   echo "$FILE exists" ```
    * ```[ -d $VAR ] ``` - True if variable holds an existing dir.
    * ```[ -x $VAR ] ``` - True if variable holds an executable file.
    * ```[ -L $VAR ] ``` - True if variable holds the path of a symlink.
    * ```[ -r $VAR ] ``` - True if variable holds an existing file thats readable.
    * ```[ -w $VAR ] ``` - True if variable holds an existing file thats writable.
    
* Using && and || 
    * 1. ``` if [ -f file.txt ]; then echo exists; else echo does not exists; fi ```
    * 2. && return if true ``` if [ -f file.txt ] && echo exists ``` Output: "exists" if file.txt exists
    * 3. || return if false ``` if [ -f filex.txt ] || echo does not exist ``` Output: "does not exist" as filex.txt is not present.
    * 4. If else ``` if [ -f filex.txt ]  && echo exists || echo does not exist ``` eg. ``` if [ $? -eq 0 ]  && echo exists || echo does not exist ```

* Argument Parsing:
    * Manual parsing using Case statements with ```shift``` (https://tldp.org/LDP/Bash-Beginners-Guide/html/sect_09_07.html)
    * ``` getopts()``` - easy way to parse short positional params (-f). Does not support long positional params (--help)
  
    * ``` getopt() ``` Enchanced version of getopts()
        * Eg: ``` opts=`getopt -o a::b:cd --long file::,name:,help -- "$@" ` ```; ```eval set --"$opts"```
        * ```eval set --"$opts"``` is used to parse script arguments.
        * Short parameters specified after ``` -o ```
        * Long parameters specified after ``` --long ``` and parameters have to seperated by ``` , ```
        * In the end specify all arguments with ```-- "$@"``` 
        * ```:```  - Parameters with a required argument.
        * ```::``` - Parameters can be followed by optional parameters.
            * For short parameters specify optional args without spaces. Eg.```./script.sh -ab ``` where b is an optional arg.
            * For long parameters specify optional args with ```=```. Eg. ```./script.sh --file=test.txt ``` where test.txt is an optional arg.



##### getopts() (: $OPTARG) example:
    while getopts a:b:cd param; 
    do
    case $param in
        a) echo "param 'a' with Argument. Access argument using $OPTARG" 
        ;;
        b) echo "param 'b' with Argument. Access argument using $OPTARG"
        ;;
        c) echo "param 'c' without Argument (no colon)"
        d) echo "param 'd' without Argument (no colon)"
    esac
    done

##### getopt() example :
    #!/bin/bash

    echo "All args: $@"
    opts=`getopt -o a::b:cd --long file::,name:,help -- "$@"`
    eval set -- "$opts"
    echo "All args after getopt: $@"
    
    while [ $# -gt 0 ]
    do
        case "$1" in
                -a) echo "param 'a' - arg $2 "
                ;;
                -b) echo "param 'b' -arg $2 "
                    shift 2
                ;;
                -c) echo "param 'c'"
                    shift 2
                ;;
                -d)  echo "param 'd'"
                    shift 2
                ;;
                --file) echo "param 'file' with arg $2 "
                    shift 2
                ;;
                --name) echo "param 'name' with arg $2"
                    shift 2
                ;;
                --help) echo "paaram 'help'"
                    shift 2
                ;;
                *)  shift
                ;;
        esac
    done


#### Arrays
* Declaring Arrays:
    * ARRAY=(val1 val2 ... valN) 
    * eg:  ``` ARRAY=(a,b,c)  ``` 
* Calling Arrays
    *  ``` ${ARRAY[0]} ``` # a
    *  ``` ${ARRAY[1]} ``` # b
    *  ``` ${ARRAY[2]} ```  # c
* Other ways to call arrays
    *  ``` ${ARRAY[@]} ``` # ALL items in an array
    * ``` ${ARRAY[*]} ``` # All items in an Array, delimited by first character of IFS
    * ``` ${!ARRAY[@]} ``` # All indexes in the array (@/*)
    * ``` ${#ARRAY[@]} ``` # Number of items in the array (@/*)
    * ``` ${#ARRAY[0]} ``` # Length of item 0 


####  Functions
* Syntax: 
    * ``` function_name () {} ```
    * OR ``` function function_name {} ```
    * Declaration of the functions should be before calling
    * Use of ``` local ``` variables in functions.



