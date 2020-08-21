#### Commands for BASH Shell


* ```pwd```
* ```cd, cd ~; cd ../;``` 
    * ```cd -```   previous location
* ```ls; ls -a;  ls -la; ```
    * ```ls -t```  last modified  ```ls -lt``` - list all in order of last modified
* ``` mkdir```
    * ```mkdir -p ``` Make parent if does not exist. Eg: ```mkdir ~/foo/laaa/laa/loo.txt```
* ``` touch ``` eg: touch 1.txt 2.txt 3.doc  ... etc Can be used to change file time stamps.
* ```date``` 
    * eg: ```date +%H:%M:%S```
    * eg: Current Week No.   ```date +%V```
* ```cat```
    * ``` cat -n``` Display Line nos.
* ``` echo ```
    * ```echo -n "Enter value:" ```  Echo will not add a newline
* ```rm```
    * ```rm -rf``` 
* ```rmdir``` Remove Dir
* ```cp```
* ```mv```
* ```wc``` - prints newline, word and byte counts for each file.
    * ``` wc -l ``` Prints newlines
    * Eg: ``` cat somefile.txt | wc -l ```
* ```grep``` 
    * ``` grep -o <pattern>``` - Print only matched 'pattern'
    * ``` grep -c <pattern> ``` - Count occurences of 'pattern'
    * ``` grep -v <pattern>``` - Search all except 'pattern'
    * ``` grep [[:digit:]] ``` - Search any lines with digits
    * ``` grep -A 2 [[:digit:]]``` 2 Traailing lines after matching patterns
    * ``` grep -B 3 [[:digit:]]``` 3 lines before matching pattern
* ``` find  <start point> -name file2find -t type```
    * Eg:  ```find ~/ -name "*.csv" -type f ``` (Type File)
    * Eg:  ```find ~/ -name Mydir -type d ``` (Type Directory)
    * Eg:  ```find /usr/share --maxdepth 2 -name "*.config" -type f ``` (Search 2 levels. Default full depth of dirs)
    * Eg:  ```find /usr/share --maxdepth 5 -mtime +10 -name "*.config" -type f ``` (Search 5 levels and Files modified more than 10 days ago)
    * Eg:  ```find /usr/share --maxdepth 5 -mtime 10 -name "*.config" -type f ``` (Search 5 levels and Files modified exactly 10 days ago)
    * Eg:  ```find /usr/share --maxdepth 5 -mtime -10 -name "*.config" -type f ``` (Search 5 levels and Files modified LESS than 10 days ago)
    * ``` find -atime``` (When file was accessed)
    * ``` find -size +5M``` Search files more than 5 Mb
* join 
* sort
* ``` chmod ```
    * Permission  Owner, Group, Others   
    * r w x   read, write, execute
    * ``` chmod a+x file.sh```  Add Execute permission for all 
    * ``` chmod a-x file.sh```  Remove Execute permission for all 
    * ``` chmod u+x file.sh```  Add Execute permission for User/File owner
    * ``` chmod g+x file.sh```  Add Execute permission for Group
    * ``` chmod o+x file.sh```  Add Execute permission for Others 
    * ``` r = 4, w =2, x = 1 . r+w+x = 7. r+w = 6 ``` Eg: chmod 644 file.sh
* time 
    * ``` time nmap 127.0.0.1``` - This will tell us the time taken by the command to execute. Useful to check script/tool performance.