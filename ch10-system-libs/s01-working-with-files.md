# Working with files

> File (file descriptor) in Python is object (as everything else)

* Opening file:
```f = open(<path>[, mode="<modificator>"][, encoding="utf-8"])```

* Modificators:
    * ```r``` – read only (default method)
    * ```r+``` – read and write
    * ```w``` – write (with flushing) (`>` in shell)
    * ```a``` – appending (`>>` in shell)
    * ```b``` – binary mode


## Basic operations

* Reading:
    * ```f.read(N)``` – read N bytes (into string)
    * ```f.readline()``` – read one line (with separator)
    * ```f.readlines()``` – read all file in a list
* ```f.close()``` – closing file (Python closes it on exit)

* Writing:
    * ```f.write(text)``` – write string to file (w/o closing)
    * ```f.writelines(lines)``` – write list of strings to file
    * ```f.flush()``` – sync buffer to disk (w/o closing file)

Changing position:

> From `Python 3.2`:
> In text files (those opened without a `"b"` in the mode string), only seeks relative to the beginning of the file are allowed (the exception being seeking to the very file end with `seek(0, 2)`).

* ```f.tell()``` – returns the file’s current position
* ```f.seek(N, [whence=0])``` – shift N bytes from the beginning
    where ```whence``` (direction) can be:
    * `0` (from beginning)
    * ```1``` (from current position)
    * ```2``` (from the end)

Example:

> Here we are using so-called "context managers" - via *with as" keywords. This allows us to not worry about closing the file descriptor after block of with-as code.


```python
filename = "/tmp/1.txt"
# filename = r"D:\tmp.txt"

with open(filename, "w") as f:
    f.write("Test string!!!\n")
    
with open(filename) as f:
    print(f.read())
    
print(f.closed)
```

_<mark style="color:purple; font-family: Hack, Consolas, Menlo, Mono, monospace; border-left: .25em solid #bc0000;border-radius: 4px;">📟 Output:</mark>_

    Test string!!!
    
    True



```python
%ls -la /tmp/1.txt
```

    -rw-r--r-- 1 jovyan users 15 Jun 20 11:52 /tmp/1.txt