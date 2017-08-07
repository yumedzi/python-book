# Working with files

> File (file descriptor) in Python is object (as everything else)

* Opening file:
```f = open(<path>, [<modificator>])```

* Modificators:
    * ```r``` – read only (default method)
    * ```r+``` – read and write
    * ```w``` – write (with flushing)
    * ```a``` – appending
    * ```b``` – binary mode


## Basic operations

* ```f.close()``` – closing file (Python closes it on exit)
* ```f.tell()``` – returns the file’s current position
* ```f.seek(N, [whence])``` – shift N bytes from the beginning
    where ```whence``` (direction) can be:
    * ```1``` (from current position)
    * ```2``` (from the end)
* Reading:
    * ```f.read(N)``` – read N bytes (into string)
    * ```f.readline()``` – read one line (with separator)
    * ```f.readlines()``` – read all file in a list



* Writing:
    * ```f.write(text)``` – write string to file (w/o closing)
    * ```f.writelines(lines)``` – write list of strings to file
    * ```f.flush()``` – sync buffer to disk (w/o closing file)

Example:

> Here we are using so-called "context managers" - via *with as" keywords. This allows us to not worry about closing the file descriptor after block of with-as code.


```python
filename = "/tmp/1.txt"

with open(filename, "w") as f:
    f.write("Test string!!!\n")
    
with open(filename) as f:
    print(f.read())
```
Output:

    Test string!!!
    
    