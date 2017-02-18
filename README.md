# orrobustshscript
## Shell Language Basics
### Variables And Simple Output
```
a= "a   b"
echo "$a"
```
######printf
```
printf "one is %d two is %g" 1 2.4
```
###### %s and %b
```
printf "%s %b" "1\t2" "1\t2"
```
will print
```
1\t2 1 2
```
### Accessing Script Arguments
prefer a for loop to while + shift. shifting cannot be undone  

### Quoting And Execution Tracing
####04:27
```
sh -x file.sh a b '1 2 3'
```

### Redirection And Special Files Part - 1
```
od -c file.txt
```

### Redirection And Special Files Part - 2
'EOF' will print literal string.  
```
cat << 'EOF'
xxxx
EOF
```
EOF will not.
```
cat << EOF
xxxx
EOF
```



### Command Types; Command And Directory Searching
use
```
type -p
```
is useful for knowing the full path to a program  


## Simple Things To Do With Text
### Simple Text Processing Utilities

```
expand   //tab->space
unexpand  //space->tab
```










## Looping
### Working With Loops: Break, Continue, And Shift
test a user is log in
```
#! /bin/sh
while true
do
  if who | grep "$user" > /dev/null
  then
    break
  fi
  sleep 5
done

echo "$user is lggged on"
exit 0
```



test a user is log out
```
#! /bin/sh
while true
do
  if who | grep "$user" > /dev/null
  then
    sleep 5
    continue
  else
    break
  fi
done

echo "$user is lggged out"
exit 0
```
















## Working With Files
###1 Working With Files And Directories
```
POSIXLY_CORRECT=1 df
```

```
mkdir d1 d2
for i in d1/f1 d2/f2
do echo this is $1>$1
done
```

###2 File Comparison And Working With Temporary Files

```
cmp -l(-p) file1 file2
```
######robustness
```
cmp -s   //for simple file comparisons
```
use
```
trap ...EXIT
```
to cleanup temporary files



### Finding And Processing Files
```
find -exec cmd {}\;    //must escape the; tp pass it to find
find  -ok cmd {}\;
ls -l
find  ... -ls
```
(create a new process per file)

######ignore case
```
find / -iname pattern
```
######size=0
```
find / -print0
```
######empty files
```
find / -empty
```



### Finding And Processing Files - Demo
```
find | LC_ALL=C sort
```
######find files not belong to user
```
find / ! -user $USER
```

######best result
```
find . -name 'fun*' -print0 | xargs -0 grep fun
```
