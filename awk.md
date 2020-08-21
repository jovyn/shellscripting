## AWK 
------------------------------------------------------

Searches files for patterns and performs actions specified in the AWK body. 

#### Structure :
* ``` awk'program_to_perform_action' file1 file2 ...```
* Divided into 3 sections BEGIN, Main & END
* BEGIN - Code specified here is executed before executing the operations on the file.
* Main - Executed for ech line of the file.
* END - After awk process of all lines.
 
       awk'BEGIN{
           code_in_BEGIN_section}
       {Code_in_Main_Body}
       END{
           code_END_Section }'file1 file2 ...
         
Example:
        
        echo "one two three" | awk'BEGIN{begin_code}{main_code}END{end_code}'
    
Example 2:

        echo "one two three" | awk'{main_code}'

### [NOTE] In AWK body, Bash features DO NOT WORK. AWK has its own syntax.

* Hello World: ``` awk 'BEGIN{print "Hello world !"}' ```
* To print "Hello World !" on each line after Enter ``` awk '{print "Hello world !"}' ``` 
* Example: ``` echo "This is one line" | awk 'BEGIN{print "start"}{print "OK"}END{print "stop"}' ``` The output is as shown below. OK is printed once as there is just one line.

        Output:
        start
        OK
        stop
      
* Example (lets input a file hello.txt which has 3 lines): ``` cat hello.txt | awk 'BEGIN{print "start"}{print "OK"}END{print "stop"}' ``` OR ```awk 'BEGIN{print "start"}{print "OK"}END{print "stop"}' hello.txt ```

        output:
        start
        OK
        OK
        OK
        stop

### Fields :

* Fields are by default seperated by space.
* ``` $0 ``` prints entire line
* ``` $1 ``` prints the first field and so on ..
* Examples: 
    * ```echo "1 2 3 4 5" | awk '{print $0}'``` will output ``` 1 2 3 4 5 ```
    * ```echo "1 2 3 4 5" | awk '{print $1}'``` will output ``` 1```
    * ```echo "1 2 3 4 5" | awk '{print $3}'``` will output ``` 3 ```   

* Examples with a File (emp.txt)
* To print all columns in the file ``` awk '{print $0}' emp.txt```
    
    Output: 

       Name Age Unit
        Ant  23  IT
        Bec  25  HR
        Red  34  CEO
        Dua  32  FIN
* ``` awk '{print $1}' emp.txt```

        Name
        Ant
        Bec
        Red
        Dua

* ``` awk '{print $2}' emp.txt```

        Age
        23
        25
        34
        32

* ``` awk '{print $3}' emp.txt```

        Unit
        IT
        HR
        CEO
        FIN
* ``` awk '{print $1,$3}' emp.txt```

        Name Unit
        Ant IT
        Bec HR
        Red CEO
        Dua FIN


### Search Patterns : 

Awk performs operations line by line. Search pattern is defined between '//'.
AWK uses the default Regular Expressions

eg 1 :   ``` awk ' /CEO/ {print $1,$3}' emp.txt```

    output:
        Red CEO


### NF - Number of Fields : 

* ``` echo "1 two 3 four" | awk '{print NF}' ``` Output : ``` 4 ```
* ``` echo "1 two 3 four" | awk '{print $(NF-2)}' ``` Output : ```two```. 
* $NF = 4 and using this we could do mathemetical operations. Eg. To print the second last field we could '{print $(NF-1)}'

### NR - Number of Records :

Records in Awk are by default seperated by a newline.

Eg 1: ```  echo "1 two 3 four" | awk '{print $(NR)}' ``` . Output : ```1```

Eg 2:  ``` awk '{print NR}' emp.txt```

    Output:
        1
        2
        3
        4
        5
        6

As ```awk``` processess line by line, for each line it prints the nos. of records found. 

To print exact records from a file we could use ``END``.
Eg: ```awk 'END{print NR}' emp.txt```. Output : ```6```


### FS - Field Seperator :

Default is space. We can define custom values for the field seperator. 

* Eg: ```echo "102 202 303" | awk 'BEGIN{FS="0"} {print $1"-"$2"-"$3"-"$4}' ``` . Output of the above command : ```  1-2 2-2 3-3``` . We used ```0``` as FS.

### RS - Record Seperator :

By default seperated by newline. Can devine custom values for RS (record seperator).

* Eg: ``` echo "102 202 303" | awk 'BEGIN{RS="0"} END{print NR}' ``` . Output is ```4```.
* Now the default RS would return 1. as there is only one line. Eg. ``` echo "102 202 303" | awk 'END{print NR}' ```  Output : ```1```


### AWK Variables :

* Assignment :
    * ``` a=1 ```
    * ``` RS="\t" ```
    * ``` FS=":" ```

* Increment/ Decrement :
    * ``` a++ / a-- ```
    * ``` a=a+1 / a=a-1```

* Math Operations :
    * ``` a=b+c ``` add
    * ``` a=b*c ``` multiply
    * ``` a=b/c ``` divide
    * ``` a=b-c ``` subtract
    * ``` a=b%c ``` Modulus 
    * ``` a=b^c ``` Raise var to the power
    * ``` a=b**c ``` Raise var to the power









