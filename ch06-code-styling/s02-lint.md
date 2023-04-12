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
* [ruff](https://github.com/charliermarsh/ruff) - an extremely fast Python linter, written in Rust
* [bandit](https://bandit.readthedocs.io) - security checker
* [mypy](https://mypy.readthedocs.io) - static type checker

## Flake8

> Much better than "default" pylint - the code style is more modern, the comments are more usable

Installation:

```sh
pip install flake8
```

### CLI

Two most useful command examples:

1. Stop the build if there are Python syntax errors or undefined names.
```sh
flake8 . --count --select=E9,F63,F7,F82 --show-source --statistics
```

2. Exit-zero treats all errors as warnings. The GitHub editor is 127 chars wide.
```sh
flake8 . --count --exit-zero --max-complexity=10 --max-line-length=127 --statistics
```

The arguments can be moved to a config as well.

### Config

`Flake8` supports storing its configuration in the following places:

Your top-level user directory.
In your project in one of setup.cfg, tox.ini, or .flake8.
Example:

```ini
setup.cfg
  [flake8]
  ignore = E266,E402,E241
```

or 

```ini
setup.cfg
  [flake8]
  ignore = D203
  exclude =
    .git,
    __pycache__,
    docs/source/conf.py,
    old,
    build,
    dist
  max-complexity = 10
```

### Error status codes

> The symbol associated with a specific check. For example, pycodestyle implements checks that look for whitespace around binary operators and will either return an error code of W503 or W504.

Using `Flake8` gives error codes from `Flake8` and the lower level `PyCode` project.

* Flake8 docs
    * [Error codes](https://flake8.pycqa.org/en/latest/user/error-codes.html)
    * Flake8 errors start with F - F4XX, F5XX, F6XX, F8XX and F901.
* PyCode style
    * [Error codes - linked from the Flake8 docs](https://pycodestyle.pycqa.org/en/latest/intro.html#error-codes)
    * E errors - EXXX.
    * W warnings - WXXX. It looks like these are mostly taken care of by using an IDE to format the code and not using any deprecated code patterns.   
      * 100 indentation
      * 200 whitespace
      * 300 blank lines
      * 400 imports
      * 500 line length
      * 600 deprecation
      * 700 statements
      * 900 syntax error
  

Examples:

```ini
F404 	future import(s) name after other statements

E266 	too many leading ‘#’ for block comment
E402 	module level import not at top of file
E241 (*) 	multiple spaces after ‘,’

W606 	‘async’ and ‘await’ are reserved keywords starting with Python 3.7
```

## Ruff

* ⚡️ 10-100x faster than existing linters
* 🐍 Installable via pip
* 🤝 Python 3.11 compatibility
* 📦 Built-in caching, to avoid re-analyzing unchanged files
* 🔧 Autofix support, for automatic error correction (e.g., automatically remove unused imports)
* 📏 Over 500 built-in rules
* ⚖️ Near-parity with the built-in Flake8 rule set
* 🔌 Native re-implementations of dozens of Flake8 plugins, like flake8-bugbear
* ⌨️ First-party editor integrations for VS Code and more

Installation:

```sh
pip install ruff
```

### Usage

CLI commands examples:

```sh
ruff check .                        # Lint all files in the current directory (and any subdirectories)
ruff check path/to/code/            # Lint all files in `/path/to/code` (and any subdirectories)
ruff check path/to/code/*.py        # Lint all `.py` files in `/path/to/code`
ruff check path/to/code/to/file.py  # Lint `file.py`
```

### Config

Configuration can be done via pyproject.toml, ruff.toml, or .ruff.toml:

```ini
[tool.ruff]
# Enable pycodestyle (`E`) and Pyflakes (`F`) codes by default.
select = ["E", "F"]
ignore = []

# Allow autofix for all enabled rules (when `--fix`) is provided.
fixable = ["A", "B", "C", "D", "E", "F", "..."]
unfixable = []
```

### VS Code extension

* [Extension on VS Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=charliermarsh.ruff)
* [GitHub link](https://github.com/charliermarsh/ruff-vscode)

Once installed in Visual Studio Code, ruff will automatically execute when you open or edit a Python file.

Interesting commands among others:
* "Fix all": automatically fix all auto-fixable violations
* "Organize Imports": isort-compatible import sorting