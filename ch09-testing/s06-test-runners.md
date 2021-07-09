# Test runners

> test runner - is a component which orchestrates the execution of tests and provides the outcome to the user. The runner may use a graphical interface, a textual interface, or return a special value to indicate the results of executing the tests.

`unittest` framework is very popular and used in many projects. But there is one area that often is replaced with parts of other testing frameworks - test runner component.

Modern framework do much better in term of auto-discovery of tests than `unittest`.

## Unittest Test Discovery

You can run unit test (written via `unittest`) with the CLI command `python -m unittest`. The help for this command is:

```bash
> python -m unittest --help
usage: python.exe -m unittest [-h] [-v] [-q] [--locals] [-f] [-c] [-b]
                              [-k TESTNAMEPATTERNS]
                              [tests [tests ...]]

positional arguments:
  tests                a list of any number of test modules, classes and test
                       methods.

optional arguments:
  -h, --help           show this help message and exit
  -v, --verbose        Verbose output
  -q, --quiet          Quiet output
  --locals             Show local variables in tracebacks
  -f, --failfast       Stop on first fail or error
  -c, --catch          Catch Ctrl-C and display results so far
  -b, --buffer         Buffer stdout and stderr during tests
  -k TESTNAMEPATTERNS  Only run tests which match the given substring
```

From `Python 3.2` `unittest` has it's own Test Discovery (if comparing to other framework's test runner/discovery the options are pretty basic):

```bash
> python.exe -m unittest discover [-h] [-v] [-q] [--locals] [-f] [-c]
                                       [-b] [-k TESTNAMEPATTERNS] [-s START]
                                       [-p PATTERN] [-t TOP]

optional arguments:
  -h, --help            show this help message and exit
  -v, --verbose         Verbose output
  -q, --quiet           Quiet output
  --locals              Show local variables in tracebacks
  -f, --failfast        Stop on first fail or error
  -c, --catch           Catch Ctrl-C and display results so far
  -b, --buffer          Buffer stdout and stderr during tests
  -k TESTNAMEPATTERNS   Only run tests which match the given substring
  -s START, --start-directory START
                        Directory to start discovery ('.' default)
  -p PATTERN, --pattern PATTERN
                        Pattern to match tests ('test*.py' default)
  -t TOP, --top-level-directory TOP
                        Top level directory of project (defaults to start
                        directory)

For test discovery all test modules must be importable from the top level
directory of the project.
```