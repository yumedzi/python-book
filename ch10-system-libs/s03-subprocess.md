# Subprocess

The subprocess module allows us to:

* spawn new processes
* connect to their input/output/error pipes
* obtain their return codes

This module is wrapper for sys calls/functions:

* `os.system()`
* `os.spawn*()`
* `os.popen*()`
* `popen2.*()`
* `commands.*()`

## Most important methods:

> These methods cover 95% of cases:

* `call`
  * When it is only needed to run some command without checking it's output
  * Also there is `check_call` method which additionally checks the exit status
* `getoutput`
  * When it's only needed to get the command's output
  * Also there is `check_output` method which additionally checks the exit status
* `Popen`
  * powerfull method which can run any kind of external command and even to pass it's output to another's command input

Parameters for all `subprocess` methods are very similar. In fact they are all based on argument list for `Popen` method. The difference is that some of the methods don't utilize all of them.

```python
Popen(args, bufsize=-1, executable=None, stdin=None, stdout=None, stderr=None, preexec_fn=None, close_fds=True, shell=False, cwd=None, env=None, universal_newlines=None, startupinfo=None, creationflags=0, restore_signals=True, start_new_session=False, pass_fds=(), *, encoding=None, errors=None, text=None)
```

These are most important `Popen` arguments (see it's help for a full list and their meaning):

* `args`: A string, or a sequence of program arguments.
* `stdin`, `stdout` and `stderr`: These specify the executed programs' standard `input`, `standard output` and `standard error` file handles, respectively.
* `shell`: If true, the command will be executed through the shell.
* `cwd`: Sets the current directory before the child is executed.

The command which we need to run (`args` argument, as shown above) should be passed as a list for UNIX (for Windows it doesn't matter):

`["ls", "-la", "/tmp"]` for command `ls -la /tmp`

This is due to the security reason to avoid the possibility of command injection.

Executing shell commands that incorporate unsanitized input from an untrusted source makes a program vulnerable to shell injection, a serious security flaw which can result in arbitrary command execution. For this reason, the use of `shell=True` is strongly discouraged in cases where the command string is constructed from external input:

🪄 _<mark style="color:green;">Code (</mark>_<mark style="color:blue;">>>></mark>_<mark style="color:green;">) and</mark>_ <mark style="color:green;">📟</mark> _<mark style="color:green;">Output</mark>_<mark style="color:green;">:</mark>

```python
>>> from subprocess import call
>>> filename = input("What file would you like to display?\n")
What file would you like to display?
non_existent; rm -rf /
>>> call("cat " + filename, shell=True) # Uh-oh. This will end badly...
```

### `subprocess.call`

> Easiest way to just run some external command

```python
subprocess.call(['ls', '-la'])
```

This will:

* Run command with arguments.
* Wait for command to complete or timeout
* `return` the `returncode` attribute.

🪄 _<mark style="color:green;">Code:</mark>_

```python
!ls
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
111					Basics_07_OOP.ipynb
Basics_01_Introduction.ipynb		Basics_08_Decorators.ipynb
Basics_02_Strings_numbers.ipynb		Basics_09_Testing.ipynb
Basics_03_Containers.ipynb		Basics_10_System_libs.ipynb
Basics_04_Functions.ipynb		images
Basics_05_Functional_Programming.ipynb	OWNED
Basics_06_PEP8_Styling.ipynb
```
{% endcode %}

🪄 _<mark style="color:green;">Code:</mark>_

```python
import subprocess

subprocess.call(["touch", "111.txt"])
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
0
```
{% endcode %}

🪄 _<mark style="color:green;">Code:</mark>_

```python
!ls 111.txt
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
111.txt
```
{% endcode %}

🪄 _<mark style="color:green;">Code:</mark>_

```python
subprocess.call(["rm", "111.txt"])
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
0
```
{% endcode %}

🪄 _<mark style="color:green;">Code:</mark>_

```python
subprocess.call(["ls", "111.txt"])
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
2
```
{% endcode %}

### `subprocess.check_call`

> This is similar to `subprocess.call` but additionally will check result code

```python
subprocess.check_call(['ls', '-la'])
```

This will run command with arguments and wait for command to complete. If the exit code was zero (this mean it was completed successfully) then return, otherwise raise `CalledProcessError`. The `CalledProcessError` object will have the return code in the `returncode` attribute.

🪄 _<mark style="color:green;">Code:</mark>_

```python
subprocess.check_call(["touch", "111.txt"])
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
0
```
{% endcode %}

🪄 _<mark style="color:green;">Code:</mark>_

```python
subprocess.check_call(["ls", "111.txt"])
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
0
```
{% endcode %}

🪄 _<mark style="color:green;">Code:</mark>_

```python
subprocess.check_call(["rm", "111.txt"])
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
0
```
{% endcode %}

🪄 _<mark style="color:green;">Code:</mark>_

```python
subprocess.check_call(["ls", "111.txt"])
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```

CalledProcessErrorTraceback (most recent call last)

<ipython-input-18-bf1b71ed0249> in <module>
----> 1 subprocess.check_call(["ls", "111.txt"])


/opt/conda/lib/python3.7/subprocess.py in check_call(*popenargs, **kwargs)
    345         if cmd is None:
    346             cmd = popenargs[0]
--> 347         raise CalledProcessError(retcode, cmd)
    348     return 0
    349 


CalledProcessError: Command '['ls', '111.txt']' returned non-zero exit status 2.
```
{% endcode %}

🪄 _<mark style="color:green;">Code:</mark>_

```python
# Create a temp lock file
subprocess.check_call(["touch", ".lock"])

# WORK....

# Remove a lock:
subprocess.check_call(["rm", ".lock"])
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
0
```
{% endcode %}

### `subprocess.getoutput`

> Easiest way to get the result of running some external command (the contents of it's `STDOUT`) using shell directly.
>
> **Note: only argument is the command to run as string.** (Other subprocess method described here use `**popenargs` mentioned above.

```python
subprocess.getoutput('ls -la')
```

🪄 _<mark style="color:green;">Code:</mark>_

```python
import subprocess

subprocess.getoutput("date")
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
'Wed Dec 11 10:42:17 UTC 2019'
```
{% endcode %}

🪄 _<mark style="color:green;">Code:</mark>_

```python
import subprocess

print("Result 1:", subprocess.getoutput("touch 111.txt"))
print("Result 2:", subprocess.getoutput("ls -la 111.txt"))
print("Result 3 (status code for <rm -rf 111.txt> command):", subprocess.call(["rm", "-rf", "111.txt"]))
print("Result 4:", subprocess.getoutput("ls -la 111.txt"))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Result 1: 
Result 2: -rwxrwxrwx 1 jovyan users 0 Dec 11 10:42 111.txt
Result 3 (status code for <rm -rf 111.txt> command): 0
Result 4: ls: cannot access '111.txt': No such file or directory
```
{% endcode %}

### `subprocess.check_output`

> This is similar to `subprocess.getoutput` but:
>
> * uses `*popenargs` arguments
> * additionally will check result code

```python
subprocess.check_output(['ls', '-la'])
```

Run command with arguments and return its output. If the exit code was non-zero it raises a `CalledProcessError`. The `CalledProcessError` object will have the return code in the `returncode` attribute and output in the `output` attribute.

🪄 _<mark style="color:green;">Code:</mark>_

```python
import subprocess

print("Result 1:", subprocess.check_output(["touch", "111.txt"]))
print("Result 2:", subprocess.check_output(["ls", "-la", "111.txt"]))
print("Result 3 (status code for <rm -rf 111.txt> command):", subprocess.call(["rm", "-rf", "111.txt"]))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Result 1: b''
Result 2: b'-rwxrwxrwx 1 jovyan users 0 Sep 20 12:16 111.txt\n'
Result 3 (status code for <rm -rf 111.txt> command): 0
```
{% endcode %}

🪄 _<mark style="color:green;">Code:</mark>_

```python
print("Result 4:", subprocess.check_output(["ls", "-la", "111.txt"]))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```

CalledProcessErrorTraceback (most recent call last)

<ipython-input-45-ff7b35de820f> in <module>
----> 1 print("Result 4:", subprocess.check_output(["ls", "-la", "111.txt"]))


/opt/conda/lib/python3.7/subprocess.py in check_output(timeout, *popenargs, **kwargs)
    393 
    394     return run(*popenargs, stdout=PIPE, timeout=timeout, check=True,
--> 395                **kwargs).stdout
    396 
    397 


/opt/conda/lib/python3.7/subprocess.py in run(input, capture_output, timeout, check, *popenargs, **kwargs)
    485         if check and retcode:
    486             raise CalledProcessError(retcode, process.args,
--> 487                                      output=stdout, stderr=stderr)
    488     return CompletedProcess(process.args, retcode, stdout, stderr)
    489 


CalledProcessError: Command '['ls', '-la', '111.txt']' returned non-zero exit status 2.
```
{% endcode %}

* `os.system(cmd)` -> exit\_status
  * Easiest way of running OS commands:

🪄 _<mark style="color:green;">Code:</mark>_

```python
import os
status = os.system("ls")
status
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
0
```
{% endcode %}

It's not possible to get results of the command but you can redirect output to some file and read it:

`os.system("ls > /tmp/ls.out")`

* `subprocess.call()` -> exit\_status
  * Simply wait until the command completes and gives us the exit status.

> `subprocess.call(args, *, stdin=None, stdout=None, stderr=None, shell=False)`

args is sequence with command like:

* `"ls -la"`
* `["ls", "-la"]`

`stdin`, `stdout`, `stderr` – file objects (StringIO is usefull here)

`shell` – run commands through shell not relying on python implementations. By default it is `False`

> There is a difference in `args` depending on `shell`. If it `True` args must be a string - but this may lead to a seriuos risk.

Executing shell commands that incorporate unsanitized input from an untrusted source makes a program vulnerable to shell injection, a serious security flaw which can result in arbitrary command execution. For this reason, the use of shell=True is strongly discouraged in cases where the command string is constructed from external input:

🪄 _<mark style="color:green;">Code (</mark>_<mark style="color:blue;">>>></mark>_<mark style="color:green;">) and</mark>_ <mark style="color:green;">📟</mark> _<mark style="color:green;">Output</mark>_<mark style="color:green;">:</mark>

```python
>>> from subprocess import call
>>> filename = input("What file would you like to display?\n")
What file would you like to display?
non_existent; rm -rf / #
>>> call("cat " + filename, shell=True) # Uh-oh. This will end badly...
```

> So it's often recommended to split command to run via using `shlex` module

🪄 _<mark style="color:green;">Code:</mark>_

```python
import shlex

command_to_run = "find / -type=d -name='super file'"

print(shlex.split(command_to_run))
print(command_to_run.split())
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
['find', '/', '-type=d', '-name=super file']
['find', '/', '-type=d', "-name='super", "file'"]
```
{% endcode %}

## Popen

> Popen is ultimate universal method for running external programs. Popen allows to do everything - reading and writing data to pipes, do pipelines of commands etc.

It allows to watch both stdout and stderr and much more. Just look at syntax:

> `subprocess.Popen(args, bufsize=-1, executable=None, stdin=None, stdout=None, stderr=None, preexec_fn=None, close_fds=True, shell=False, cwd=None, env=None, universal_newlines=False, startupinfo=None, creationflags=0, restore_signals=True, start_new_session=False, pass_fds=())`

🪄 _<mark style="color:green;">Code:</mark>_

```python
import subprocess
proc = subprocess.Popen(['echo', 'Hello POPEN', '!!!'], 
                        stdout=subprocess.PIPE,
                        )
stdout_value, stderr_value = proc.communicate()
print('STDOUT:', stdout_value)
print('STDERR:', stderr_value)
print(proc.pid)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
STDOUT: b'Hello POPEN !!!\n'
STDERR: None
72
```
{% endcode %}

```python
import subprocess

with open('tmp_file', "w") as f:
    proc = subprocess.Popen(['cat'],
                            stdin=subprocess.PIPE,
                            stdout=f, 
                            )
    proc.communicate(b'SENDING SOMETHING TO STDIN ---> 2021/04/16\n')
```

🪄 _<mark style="color:green;">Code:</mark>_

```python
import subprocess, os, platform

print(os.path.abspath(os.path.curdir))

if platform.system == "Windows":
    proc = subprocess.Popen(['type', 'tmp_file'], 
                            stdout=subprocess.PIPE,
                            shell=True)
else:
    proc = subprocess.Popen(['cat', 'tmp_file' ], 
                            stdout=subprocess.PIPE)

stdout_value = proc.communicate()[0]
print('STDOUT:', stdout_value) # Bytes is physical char bytes string
print(stdout_value.decode("utf-8"))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
/notebooks/V2/Basics
STDOUT: b'SENDING SOMETHING TO STDIN ---> 2021/04/16\n'
SENDING SOMETHING TO STDIN ---> 2021/04/16
```
{% endcode %}

Or like this:

🪄 _<mark style="color:green;">Code:</mark>_

```python
import shlex

cmd = "cat tmp_file"
print(shlex.split(cmd))

#subprocess.check_output(shlex.split(cmd))
subprocess.getoutput("cat tmp_file")
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
['cat', 'tmp_file']





'SENDING SOMETHING TO STDIN ---> 2021/04/16'
```
{% endcode %}

Pipeline:

🪄 _<mark style="color:green;">Code:</mark>_

```python
! df -ah | grep /notebooks
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
/dev/vg1000/lv  7.0T  6.6T  459G  94% /notebooks
```
{% endcode %}

🪄 _<mark style="color:green;">Code:</mark>_

```python
p1 = subprocess.Popen(['df', '-ah'], stdout=subprocess.PIPE)
p2 = subprocess.Popen(['grep', '/notebooks'], stdin=p1.stdout, stdout=subprocess.PIPE, text=True)

if p1.wait() == 0:  # Wait for p1 to finish with status 0
    #p1.stdout.close()  # Allow p2 to detect a SIGPIPE if p1 exits
    p2_output = p2.communicate()[0]
    print(p2_output)
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
/dev/vg1000/lv  7.0T  6.6T  459G  94% /notebooks
```
{% endcode %}

Need `awk`? No problem:

🪄 _<mark style="color:green;">Code:</mark>_

```python
import shlex

p1 = subprocess.Popen(['df','-ah'], stdout=subprocess.PIPE)
p2 = subprocess.Popen(['grep', '/notebooks'], stdin=p1.stdout, stdout=subprocess.PIPE)
p3 = subprocess.Popen(shlex.split("awk '{print $5;}'"), stdin=p2.stdout, stdout=subprocess.PIPE, text=True)

if p1.wait() == p2.wait() == 0:  # Wait for p2 to finish with status 0
    print(p3.communicate()[0])
else:
    p3.kill()
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
94%
```
{% endcode %}

Or - via Python:

🪄 _<mark style="color:green;">Code:</mark>_

```python
print(p2_output.split()[4])
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
94%
```
{% endcode %}

🪄 _<mark style="color:green;">Code:</mark>_

```python
import re
print(re.search(r'(\d+%)', p2_output).group(1))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
94%
```
{% endcode %}

Another example - let's get how much memory Jupyter Notebook uses.

Shell commands used:

🪄 _<mark style="color:green;">Code:</mark>_

```python
!ps auxw | grep jupyter-notebook | grep -v grep
!ps auxw | grep jupyter-notebook | grep -v grep | awk '{print $5}'
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
jovyan       6  0.0  1.0 229712 64068 ?        Sl   Apr09   1:09 /opt/conda/bin/python /opt/conda/bin/jupyter-notebook
229712
```
{% endcode %}

Via `subprocess.check_output()`:

🪄 _<mark style="color:green;">Code:</mark>_

```python
cmd = "ps auxw | grep jupyter-notebook | grep -v grep | awk '{print $5}'"

print(float(subprocess.getoutput(cmd).rstrip()))
print(float(subprocess.check_output(cmd, shell=True).decode("utf8").rstrip()))
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
251984.0
251984.0
```
{% endcode %}

Via `subprocess.Popen()`:

🪄 _<mark style="color:green;">Code:</mark>_

```python
p1 = subprocess.Popen(["ps", "auxw"], stdout=subprocess.PIPE)
p2 = subprocess.Popen(["grep", "jupyter-notebook"], stdin=p1.stdout, stdout=subprocess.PIPE)
p3 = subprocess.Popen(shlex.split("grep -v grep"), stdin=p2.stdout, stdout=subprocess.PIPE)
p4 = subprocess.Popen(shlex.split("awk '{print $5}'"), stdin=p3.stdout, stdout=subprocess.PIPE)

print(f'Jupyter Notebook eats {int(p4.communicate()[0].decode("utf8")) / 1024:5.2f} MB of memory')
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
Jupyter Notebook eats 224.33 MB of memory
```
{% endcode %}

We can also use context manager for `subprocess.Popen` to clean resources after running processes:

🪄 _<mark style="color:green;">Code:</mark>_

```python
with subprocess.Popen(["ls", "-la", "."], stdout=subprocess.PIPE, text=True) as proc:  
    print(proc.pid)                                                               
    print("Alive" if proc.poll() is None else "Terminated")                       
    print("OUTPUT:")                                                              
    print(proc.communicate()[0])
```

📟 _<mark style="color:green;">Output:</mark>_

{% code overflow="wrap" %}
```
112
Alive
OUTPUT:
total 744
drwxrwxrwx 1 jovyan users    606 Apr 16 09:50 .
drwxrwxrwx 1 jovyan users     84 Oct  2  2019 ..
-rwxrwxrwx 1 jovyan users  52631 Feb 24 11:26 Basics_01_Introduction.ipynb
-rwxrwxrwx 1 jovyan users 133308 Apr  4 09:38 Basics_02_Strings_numbers.ipynb
-rwxrwxrwx 1 jovyan users 134635 Mar 15 11:16 Basics_03_Containers.ipynb
-rwxrwxrwx 1 jovyan users  60168 Apr  4 16:31 Basics_04_Functions.ipynb
-rwxrwxrwx 1 jovyan users  47696 Mar 22 11:39 Basics_05_Functional_Programming.ipynb
-rwxrwxrwx 1 jovyan users  30427 Mar 29 10:17 Basics_06_PEP8_Styling.ipynb
-rwxrwxrwx 1 jovyan users  71901 Apr  7 06:37 Basics_07_OOP.ipynb
-rwxrwxrwx 1 jovyan users  50381 Apr  9 10:05 Basics_08_Decorators.ipynb
-rwxrwxrwx 1 jovyan users  70916 Apr 14 09:38 Basics_09_Testing.ipynb
-rwxrwxrwx 1 jovyan users  84181 Apr 16 09:50 Basics_10_System_libs.ipynb
lrwxrwxrwx 1 jovyan users     17 Aug 23  2019 images -> /notebooks/images
drwxrwxrwx 1 jovyan users    762 Feb 24 11:26 .ipynb_checkpoints
-rwxrwxrwx 1 jovyan users     43 Apr 16 09:41 tmp_file
```
{% endcode %}
