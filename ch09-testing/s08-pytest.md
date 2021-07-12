## Pytest

This is the top modern Python testing framework at this moment. It has a lot of options, it offers a lot of unique (non-Junit-style) testing capabilities that at the same time are much easier to compehend and extend if needed.

Pytest has also a runner.

To install and use the runner:

```bash
pip install -U pytest pytest-cov
```

This will add `pytest` binary to PATH allowing to run this command.

To see all `pytest` CLI options:

```bash
> pytest --help
```

This will produce a large list of options (In case additional plugins installer the help will be bigger).

Let's check the main Pytest options per functionality.

### Running pytest

* Auto-discovery of all tests starting with current directory:

`pytest`

* Run tests in a module

`pytest test_mod.py`

* Run tests in a directory

`pytest testing/`

Options:

* `-q` - quiet mode
* `-v` - verbose mode
* `-s` - no capture (show all `print()` stdout/stderr outputs)
* `-x` - exit instantly on first error or failed test.
* `--runxfail` - report the results of xfail tests as if they were not marked
* `--lf` - rerun only the tests that failed at the last run (or all if none failed)
* `--ff` - run all tests, but run the last failures first.
* `--nf` - run tests from new files first, then the rest of the tests sorted by file mtime

### Filtering tests

* Run tests by keyword expressions

`pytest -k "MyClass and not method"`

Here the keyword option allows to specify a query-like filter which is based on the checks of keyword presense in  filenames, class names and function names. The example above will run `TestMyClass.test_something` but not `TestMyClass.test_method_simple`.

* Run a specific test within a module:

`pytest test_mod.py::test_func`

`pytest test_mod.py::TestClass::test_method`

* Run tests by marker expressions (decorated with the `@pytest.mark.critical`)

`pytest -m critical`

`pytest -m "critical and security"`


### Reporting

* The `-r` flag can be used to display a “short test summary info” at the end of the test session, making it easy in large test suites to get a clear picture of all failures, skips, xfails, etc. It defaults to `fE` - faults/fails and errors.

Here is the full list of available characters that can be used:

* `f` - failed
* `E` - error
* `s` - skipped
* `x` - xfailed
* `X` - xpassed
* `p` - passed
* `P` - passed with output

Special characters for (de)selection of groups:
* `a` - all except pP
* `A` - all
* `N` - none, this can be used to display nothing (since fE is the default)


Additional reporting options:

* `--tb=style` - traceback print mode (auto/long/short/line/native/no).
* `--show-capture={no,stdout,stderr,log,all}`
    * Controls how captured stdout/stderr/log is shown on failed tests. Default is 'all'.
* `--full-trace` - don't cut any tracebacks (default is to cut).
* `--color=color` - color terminal output (yes/no/auto).
* `--code-highlight={yes,no}`
    * Whether code should be highlighted (only if --color is also enabled)
* `--pastebin=mode` - send failed|all info to bpaste.net pastebin service.
* `--junit-xml=path` - create junit-xml style report file at given path.
* `--junit-prefix=str` - prepend prefix to classnames in junit-xml output

### Coverage

Coverage shows what part of the code is covered by unittest. Also there is a metric called "branch coverage" which shows how much the logic of the application is covered by tests (all if/else branches are covered).

It possible to install the plugin for pytest for coverage:

```bash
pip install -U pytest-cov
```

And then to use it:

```bash
pytest --cov --cov-report=xml
```

to produce Cobertura-compliant XML-based report (that can be used in CI tool for reporting).