# Unix Text Processing

### Command-line utilities 

`grep` is a powerful command-line tool that allows to search files for lines that match a regex and writes each matching line to standard output.

```diff
# To leave initial file unchanged, you can use ">" and create new file with query changes applied:
file.txt > new_file.txt 

# Find text string by patterns:
grep 'pattern1\|pattern2' file.txt 

# Get number of rows in a file:
wc -l file.txt 

# Get only unique lines from file:
uniq text.txt  

# Print number of lines (NUM) of trailing context after matching lines (Pattern):
grep -A NUM 'Pattern' file.txt 
 
# Print number of lines (NUM) of leading context before matching lines:
grep -B NUM 'Pattern' file.txt 
```


### AWK

`AWK` is a versatile language designed for text processing. Like sed and grep, it is a filter. 

```diff
# Total sum of values in column (int):
awk -v N=1 '{ sum += $N } END { if (NR > 0) print sum  }' file.txt

# Filter column by values levels:
awk '{if($1<10)print$1}' < file.txt > 10.txt
awk '{if($1>=10 && $1<=20)print$1}' < file.txt > 10_20.txt
awk '{if($1>50)print$1}' < file.txt > 50.txt
 
# Get first word from each line:
awk '{print $1}' file.txt

# Get all even lines:
awk 'NR%2==0' file.txt
```


### SED

`sed` is a Unix utility that parses and transforms text, using a simple, compact programming language.

```diff
# Delete all lines containing pattern:
sed '/pattern/d' file.txt

# Delete all lines starting with specific symbol, e.g. "-":
sed  '/-$/ d' file.txt

# Get N lines after pattern match:
sed -n '/pattern/,+Np' file.txt

# Get number of lines from file into a variable:
export A="file.txt"
NUM_LINES_A=$(wc -l < "$A")

# Split values by chanks (10% chank):
split -n l/10/10 file.txt

 # Align all text flush right on a N'th-column width
 sed -e :a -e ‘s/^.{1,N}$/ &/;ta’ file.txt

# Delete all specific symbols from file (commas):
sed 's/,//g' file.txt

# Insert a blank line below every line which matches “patern”
sed ‘/patern/G’ file.txt

# Get rid of all letters from file, only number will remain:
sed 's/[A-Za-z]*//g' file.txt

# Get last 3 symbols from each line, each dot represents symbol:
sed 's/.*\(...\)/\1/' file.txt

# Add symbol to each line ("symbol"):
sed -e 's/^/symbol/' file.txt

# Number each line of a file, on left
sed ‘N; s/^/     /; s/ *(.{6,})n/1  /‘ file.txt

# Cut all after 1 char of each line:
sed -r 's/(.{1}).*/\1/' file.txt

# Delete line if N'th char is not matching exact symbol ("r"): 
sed -E '/^.{N}[^r]/d' file.txt

# Delete all lines with specific length (by number of symbols in line, NUM):
grep -vE '^.{NUM}$' file.txt

# Delete all lines longer than N characters in a line:
sed '/^.\{N\}./d' file.txt

# Cut characters in the end of line with pattern:
sed -e '/pattern/s/.\{NUM\}$//' file.txt

# Add line with timestamp to end of line with pattern
sed ':a $!N;s/\n2020/ 2020/;ta P;D' file.txt
```
