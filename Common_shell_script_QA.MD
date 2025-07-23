## common programming questions on Shell Scripting

* Basics
What is a shell? What is a shell script?
How do you write and run a shell script?
What is the difference between sh and bash?
How do you make a script executable?
e.g., chmod +x script.sh

* Variables and Input
How do you define a variable in a shell script?
How do you read user input in a shell script?
e.g., read name
What's the difference between $var, ${var}, and "$var"?

* Conditionals and Loops
How do you write an if statement in shell?
How do you use case statements?
What are the different types of loops in shell?
for, while, until
How do you compare numbers or strings in shell?
-eq, -lt, ==, !=, etc.

* Functions
How do you declare and call a function?
Can functions return values in shell scripts?

* File and Directory Operations
How do you check if a file exists?
if \[ -f filename ]
How to read a file line by line?
How to check if a directory exists?
How to find files using find and grep?

* String and Array Handling
How to get the length of a string?
How to extract substrings?
How to split strings or parse CSV files?
How to work with arrays in bash?

* Scripting Concepts
What is exit status in shell?
How does redirection work (>, >>, 2>\&1)?
What are pipes (|) used for?
What is the difference between " and ' in shell?

* Process Management
How do you run a command in the background?
e.g., command \&
How to get the process ID (PID)?
What is cron and how is it used in automation?

* Advanced / Practical Questions
Write a script to backup a directory.
Write a script to monitor disk usage.
Write a script to count the number of lines, words, and characters in a file.
Write a script to find duplicate files in a directory.
How do you handle errors in shell scripts?

🔹 1. What is a shell? What is a shell script?

Shell: A command-line interpreter that allows users to interact with the OS using commands.

Shell Script: A file containing a series of shell commands. It automates tasks.

\#!/bin/bash

echo "Hello, World!"



🔹 2. How do you write and run a shell script?

Steps:

Create a file, e.g., myscript.sh

Add commands.

Make it executable: chmod +x myscript.sh

Run: ./myscript.sh



🔹 3. What is the difference between sh and bash?

sh is the original Bourne shell.

bash (Bourne Again SHell) is an enhanced version with more features.



🔹 4. How do you make a script executable?

chmod +x script.sh



🔹 5. How do you define a variable?

name="John"

echo "Hello, $name"



🔹 6. How do you read user input?

echo "Enter your name:"

read name

echo "Hi, $name!"



🔹 7. What's the difference between $var, ${var}, and "$var"?

$var and ${var} are usually equivalent. {} helps avoid ambiguity.

"$var" preserves whitespace and prevents word splitting.



🔹 8. Example of if statement:

num=10

if \[ $num -gt 5 ]; then

&nbsp;   echo "Greater than 5"

else

&nbsp;   echo "5 or less"

fi



🔹 9. case Statement

echo "Enter a number between 1 and 3:"

read num



case $num in

&nbsp; 1) echo "You chose One" ;;

&nbsp; 2) echo "You chose Two" ;;

&nbsp; 3) echo "You chose Three" ;;

&nbsp; \*) echo "Invalid choice" ;;

esac



🔹 10. Types of Loops

for loop:

for i in 1 2 3; do

&nbsp; echo "Number: $i"

done



while loop:

count=1

while \[ $count -le 3 ]; do

&nbsp; echo "Count: $count"

&nbsp; ((count++))

done



until loop:

count=1

until \[ $count -gt 3 ]; do

&nbsp; echo "Count: $count"

&nbsp; ((count++))

done



🔹 11. Number and String Comparison

Numbers:

a=5

b=10



if \[ $a -lt $b ]; then

&nbsp; echo "$a is less than $b"

fi

Strings:

str1="hello"

str2="world"



if \[ "$str1" != "$str2" ]; then

&nbsp; echo "Strings are different"

fi



🔹 12. Functions in Shell

greet() {

&nbsp; echo "Hello, $1"

}

greet "Alice"



🔹 13. Return Value from Functions

add() {

&nbsp; result=$(( $1 + $2 ))

&nbsp; return $result

}



add 3 4

echo "Sum is $?"  # $? contains return value

Note: Shell functions can only return numbers (0–255) directly. Use global vars for larger values.



🔹 14. Check if File Exists

file="myfile.txt"

if \[ -f "$file" ]; then

&nbsp; echo "$file exists"

else

&nbsp; echo "$file does not exist"

fi



🔹 15. Read File Line by Line

while IFS= read -r line; do

&nbsp; echo "$line"

done < file.txt



🔹 16. Check if Directory Exists

dir="/home/user/docs"

if \[ -d "$dir" ]; then

&nbsp; echo "Directory exists"

else

&nbsp; echo "Directory does not exist"

fi



🔹 17. Find Files Using find and grep

\# Find all .log files

find /var/log -name "\*.log"



\# Search for "error" in all .txt files

grep "error" \*.txt



🔹 18. Get Length of a String

str="Hello World"

echo "Length: ${#str}"  # Output: 11



🔹 19. Extract Substring

str="HelloWorld"

echo "${str:0:5}"  # Output: Hello



🔹 20. Split String

str="apple,banana,orange"

IFS=',' read -ra fruits <<< "$str"

for fruit in "${fruits\[@]}"; do

&nbsp; echo "$fruit"

done



🔹 21. Arrays in Bash

arr=("one" "two" "three")

echo "First element: ${arr\[0]}"

echo "All elements: ${arr\[@]}"



🔹 22. Exit Status

ls /tmp

echo $?  # Returns 0 if command was successful, else non-zero



🔹 23. Redirection Operators

command > file.txt    # stdout to file

command >> file.txt   # append stdout

command 2> error.txt  # stderr to file

command > out.txt 2>\&1  # both stdout and stderr



🔹 24. Pipes

ls -l | grep "^d"  # List directories only



🔹 25. Quoting in Shell

name="John"



echo "$name"     # Correct (preserves spaces, expands variable)

echo '$name'     # Prints: $name (no expansion)



🔹 26. Background Processes

sleep 60 \&

echo "Background PID: $!"



🔹 27. Get PID of a Process

pidof bash

Or:

ps aux | grep process\_name



🔹 28. Cron Jobs (Automation)

To open crontab editor:

crontab -e

Example job: Run backup script every day at 2 AM:



0 2 \* \* \* /home/user/backup.sh



🔹 29. Script to Backup a Directory

\#!/bin/bash

src="/home/user/documents"

dest="/home/user/backup\_$(date +%F).tar.gz"



tar -czf "$dest" "$src"

echo "Backup created at $dest"



🔹 30. Disk Usage Monitor Script

\#!/bin/bash

usage=$(df -h / | awk 'NR==2 {print $5}' | sed 's/%//')



if \[ $usage -gt 80 ]; then

&nbsp; echo "Disk usage is above 80%!"

else

&nbsp; echo "Disk usage is normal."

fi



🔹 31. Count Lines, Words, Characters in a File

\#!/bin/bash

file="sample.txt"

wc "$file"



🔹 32. Find Duplicate Files in a Directory

\#!/bin/bash

find . -type f -exec md5sum {} + | sort | uniq -d --check-chars=32



🔹 33. Error Handling with set

\#!/bin/bash

set -e  # Exit on error

cp file1.txt file2.txt

echo "Copy successful"

Add trap for custom error messages:



trap 'echo "An error occurred."' ERR





🧠 Logic \& Algorithm Questions

FizzBuzz: Print numbers 1 to 100; multiples of 3 print "Fizz", multiples of 5 print "Buzz", both print "FizzBuzz".

Reverse a string or array.

Check if a string is a palindrome.

Find the factorial of a number.

Find the largest/smallest number in an array.

Remove duplicates from an array.

Check if two strings are anagrams.

Count the number of vowels in a string.

Implement binary search.

Fibonacci sequence (iterative and recursive).

