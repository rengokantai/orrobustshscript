# orrobustshscript

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
