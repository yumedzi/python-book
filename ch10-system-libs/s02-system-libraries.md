# System libraries

## os, os.path

`os` and `os.path` have many useful functions to interact with file system

Main functions:
* `os.path.exists(path)`
    * Returns True if path exists
* `os.listdir(dir)`
    * List of filenames in that directory path (not including . and ..). The filenames are just the names in the directory, not their absolute paths.
* `os.mkdir(dir_path)`
    * Makes one dir (like mkdir <dir_path>)
* `os.makedirs(dir_path)`
    * Makes all the needed dirs in this path (like `mkdir –p <dir_path>`)


* `os.path.abspath(path)`
    * given a path, return an absolute form (/home/user/file.txt instead of './file.txt')
* `os.path.dirname(path)`
    * Returns dirname for a file or directory, given "boo/foo/file.txt", it will return the "boo/foo"
* `os.path.basename(path)`
    * Returns basename, given "boo/foo/file.txt", it will return the "file.txt"
* `os.path.join(path1, *pathes)`
    * Join two or more pathes components using default OS separator (for Windows "\\", for UNIX – '/')

### Example

Script lists filenames from a dir, prints their relative and absolute paths

`dir: /home/user/dir, file: foo.txt`

🪄 _<mark style="color:green;">Code:</mark>_

```python
def printdir(dir):
  filenames = os.listdir(dir)
  for filename in filenames:
    print(filename)
		# foo.txt
    print(os.path.join(dir, filename))
		# dir/foo.txt (relative to current dir)
    print(os.path.abspath(os.path.join(dir, filename)))
		# /home/user/dir/foo.txt
```

Another great method of iteration through directories and files: `os.walk`:

> `os.walk(top, topdown=True, onerror=None, followlinks=False)`

Generate the file names in a directory tree by walking the tree either top-down or bottom-up. For each directory in the tree rooted at directory top (including top itself), it yields a 3-tuple (`dirpath`, `dirnames`, `filenames`).


🪄 _<mark style="color:green;">Code:</mark>_

```python
# Code to list contents of /tmp dir
import os
for root, dirs, files in os.walk('/tmp/'):
    # if "Listeners" in files:
    #     print(f"Found in {root}")
    #     break
    print("ROOT:{}\nDIRS:{}\nFILES:{}\n".format(root, dirs, files))
```

📟 _<mark style="color:green;">Output:</mark>_

    ROOT:/tmp/
    DIRS:['com.apple.launchd.jhoY1qEd1J', 'com.apple.launchd.T3n42gvHZB', 'com.apple.launchd.xfxnszQVjh']
    FILES:['1']
    
    ROOT:/tmp/com.apple.launchd.jhoY1qEd1J
    DIRS:[]
    FILES:['org.macosforge.xquartz:0']
    
    ROOT:/tmp/com.apple.launchd.T3n42gvHZB
    DIRS:['testme']
    FILES:['Listeners']
    
    ROOT:/tmp/com.apple.launchd.T3n42gvHZB/testme
    DIRS:[]
    FILES:[]
    
    ROOT:/tmp/com.apple.launchd.xfxnszQVjh
    DIRS:[]
    FILES:['Render']
    


🪄 _<mark style="color:green;">Code:</mark>_

```python
# Mass file deleter - !DON'T TRY THIS AT HOME!
import os
for root, dirs, files in os.walk(top, topdown=False):
    for name in files:
        os.remove(os.path.join(root, name))
    for name in dirs:
        os.rmdir(os.path.join(root, name))
```

### Cheatsheet

* `os.getcwd()`, `os.curdir`
    * Returns current directory (absolute and relative ones)
* `os.chdir(dir)`
    * Changes current directory to path specified in dir
* `os.rename(src, dst)` 
    * Rename the file or directory src to dst. If dst is a directory, OSError will be raised.
* `os.remove(path)`
    * Remove (delete) the file path. If path is a directory, OSError
* `os.rmdir(path)`
    * Remove (delete) the directory path. Only works when the directory is empty
* `os.removedirs(path)`
    * Remove directories (empty) recursively.


## pathlib

> `pathlib` is modern lib for working with paths.

This lib is class-based wrapper on many `os` and `os.path` methods.

Few examples:


```python
from pathlib import Path

p = Path("example")

print(p)
print(p.resolve())  # os.path.abspath
```

📟 _<mark style="color:green;">Output:</mark>_

    example
    /notebooks/V2/Basics/example



🪄 _<mark style="color:green;">Code:</mark>_

```python
print(p.exists()) # `os.path.exists`
```

📟 _<mark style="color:green;">Output:</mark>_

    False



🪄 _<mark style="color:green;">Code:</mark>_

```python
p.mkdir()         # os.mkdir
print(p.exists()) 
print(p.is_dir()) # os.path.is_dir
```

📟 _<mark style="color:green;">Output:</mark>_

    True
    True



🪄 _<mark style="color:green;">Code:</mark>_

```python
test_file = p / "test.txt"
test_file
```




📟 _<mark style="color:green;">Output:</mark>_

    PosixPath('example/test.txt')




🪄 _<mark style="color:green;">Code:</mark>_

```python
test_file.write_text("Hello Pathlib!")
```




📟 _<mark style="color:green;">Output:</mark>_

    14




🪄 _<mark style="color:green;">Code:</mark>_

```python
test_file.read_text()
```




📟 _<mark style="color:green;">Output:</mark>_

    'Hello Pathlib!'



Listing dir's contents:


```python
[x for x in p.iterdir()]
```




📟 _<mark style="color:green;">Output:</mark>_

    [PosixPath('example/test.txt')]



Searching for particular files by pattern:


```python
[x for x in p.glob("*.txt")]
```




    [PosixPath('example/test.txt')]



Clearing our samples:


```python
test_file.unlink()
p.rmdir()
```

## shutil

> `shutil` module offers a number of high-level operations on files and collections of files. In particular, functions are provided which support file copying and removal. 

For individual operations like removing it's better to use `os.remove()` as it is more safe.

Mostly this module is about files and dirs copy and removal.

* Copying/Moving:
    * `shutil.copy(src, dst)`
        * Copy the file src to the file or directory dst. If dst is a directory, a file with the same basename as src is created (or overwritten) in the directory specified.
    * `shutil.copy2(src, dst)`
        * Same as `copy` but with preserving metadata.
    * `shutil.copytree(src, dst)`
        * Recursively copy an entire directory tree rooted at src. The destination directory, named by dst, must not already exist; it will be created as well as missing parent directories.
    * `shutil.move(src, dst)`
        * Recursively move a file or directory (src) to another location (dst).

* Removing:
    * `shutil.rmtree(path[, ignore_errors][, on_error])`
        * Delete an entire directory tree; path must point to a directory (but not a symbolic link to a directory).  If ignore_errors is true, errors resulting from failed removals will be ignored.

**HINT:**

* `os.remove(path)`
    * Remove a single file
* `os.rmdir(dir)`
    * Remove an empty dir
* `shutil.rmtree(path)`
    * Remove a tree
* `shutil.rmtree(path, ignore_errors=True)`
    * Remove a tree ignoring any errors

### Example

Backing up python source files:

```python
import shutil
import os

os.mkdir("backup")
for original in os.listdir("."):
    if os.path.splitext(original)[-1] == ".py":
        backup = os.path.join("backup", original)
        if not os.path.exists(backup) or os.path.getmtime(backup) < os.path.getmtime(original):
            shutil.copy2(original, backup)
```