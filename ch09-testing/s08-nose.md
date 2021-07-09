## Nose
Nose is handy to run all tests in a directory

```sh
pip install nose

$ nosetests
```

This command - `nosetests` - will automatically look for any modules (and packages) with tests (there are unittest or nose tests in modules in working directory and sub-directories if the names of those packages match "test" subword (`-m` option, `NOSE_TESTMATCH`).

Useful options:

* Current directory is used as default working directory. It is possible to specify needed one (or several) via `-w` option:

```sh 
nosetests -w parsing/ -w export/csv/tests/
```

Nose by default will look in current dir (or in `-w` specified) and will try to find files/dirs/tests that are matched by (`-m` argument).

* Specifying a list of tests to run. nose allows specifying a set of tests on the command line. Only tests that are both discovered and in this set of tests will be run. For example:

```sh
nosetests -w parsing tests/test_csv.py:test_bigdata
```

only runs the function test_bigdata found in `parsing/tests/test_csv.py`.

* Not capturing stdout via `-s` option. By default, nose captures all output and only presents `stdout` from tests that fail. So `print()` calls won't show anything. By specifying `-s`, this can be turned off for debugging purposes.

Other options:

* `-v` - Verbose mode
* `-m` - regex (`NOSE_TESTMATCH`) with files/dirs/tests to considered as tests 
    * (default=`(?:^|[\b_\.\-])[Tt]est`)
    * better not change
* `-I` - regex what files to ignore (`--ignore-files=REGEX`)
* `-i` - regex with files/dirs/tests to be included
    * add something that is not covered by default `-m`
* `-e` - regex with files/dirs/tests to be excluded
    * if we don't want to test specific files/cases
* `--processes` - Parallel execution by nosetests (number of cores = processes):

```sh
nosetests --processes=4 tests.py
```
This is useful when testing UI with Selenium - but using number of parallel processes bigger than number of CPU cores is bad for performance.