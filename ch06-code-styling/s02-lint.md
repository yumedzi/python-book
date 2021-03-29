# Lint

http://www.pylint.org

`pip install pylint`

* Checking line-code's length,
* Checking if variable names are well-formed according to your coding standard
* Checking if imported modules are used

Usage:

`pylint script.py`

To decipher warnings and other messages:
* http://pylint-messages.wikidot.com/all-codes

Also it is possible to force pylint to ignore some rule checks:
* In comments in your code before code to ignore:

```# pylint: disable=C0321```

Create/use pylint config file with all needed settings:
```sh
$PYTHON_PATH/lib/site-packages/pylint/standard.rc
pylint --generate-rcfile > standard.rc
disable=W0511, C0321 >> standard.rc
pylint --rcfile=<path>/standard.rc```

Another good linters/checkers are:
* [flake8](https://flake8.pycqa.org) - alternative PEP8 checker
* [bandit](https://bandit.readthedocs.io) - security checker
* [mypy](https://mypy.readthedocs.io) - static type checker