# Continiuos integration

> Continiuos integration (CI) is the practice of building or merging all developer working copies to a shared mainline several times a day or by triggering some predefined event. During build process it is common practice to run tests as part of the process. Via doing this each commit is verified against existing test cases.

In this sub-chapter main practices of CI/testing workflow will be shown. It is very common to use combination of `nose` test runner with `Jenkins` CI application.


## Nose

> [Nose](http://nose.readthedocs.io) itself is powerful testing framework. At some point it was forked from very popular [pytest](https://docs.pytest.org/en/latest/) framework. It is possible (and very easy also) to write unit tests based on `nose` but nowadays it is more popular as test runner then testing framework. This means `nose` is used to run test written on `unitest`.

Nose is handy to run all tests in a directory:

```
pip install nose

$ nosetests```

This command - `nosetests` - will automatically look for any modules (and packages) with tests (there are unittest or nose tests in modules in working directory and sub-directories if the names of those packages match "test" subword).

Useful options:

* Current directory is used as default working directory. It is possible to specify needed one (or several) via `-w` option:
```sh
nosetests -w parsing/ -w export/csv/tests/
```

* Specifying a list of tests to run. `nose` allows specifying a set of tests on the command line. Only tests that are both discovered and in this set of tests will be run. For example,
```sh
nosetests -w parsing tests/test_csv.py:test_bigdata
```
    * only runs the function `test_bigdata` found in `parsing/tests/test_csv.py`.
    

* Not capturing `stdout` via `-s` option. By default, nose captures all output and only presents stdout from tests that fail. So `print()` calls won't show anything. By specifying `-s`, this can be turned off.

* Parralel execution by nosetests (number of cores = processes):
```sh
nosetests --processes=4
```
    * when testing UI with Selenium (please note that more than 4 parallel processes is bad for performance because of each process starts own browser window)

* It is possible to run doctests via `--with-doctest` parameter


## Jenkins

> [Jenkins](https://jenkins.io/) is one of the most popular open source automation server. It is used forbuilding, deploying and automating projects.
> Jenkins can be installed through native system packages, Docker, or even download `jenkins.war` file and run it standalone on any machine with the Java Runtime Environment installed.

### Main features


Auto start of tests:
+ schedule
+ by commit
+ by configurable event
+ manually

Reports:
* Junit parsing
* draw graphics,
* keep history of all builds, dynamics
* store time of runs

xUnit-style reports:
* To generate xUnit-style report tick the box named “Publish JUnit test result report” and specify the name of file:
    ```
**/nosetests.xml
    ```
* Add `--with-xunit` option to `nosetests` command:
    ```
nosetests --with-xunit
```

### Installation

Basic installation:

1. Download Jenkins: [stable jenkins.war](http://mirrors.jenkins.io/war-stable/latest/jenkins.war).
2. Open up a terminal in the download directory and run java -jar jenkins.war --httpPort=8080
3. Browse to http://localhost:8080 and follow the instructions to complete the installation.

Example of installation in Ubuntu:

```sh
wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo aptitude update
sudo aptitude install jenkins
```
    
### Basic job overview

Here is main steps needed when defining new simple job (taken from great [Alex Conrad's article](http://www.alexconrad.org/2011/10/jenkins-and-python.html)):

#### Creating new job

* Click "New job" button

![](/assets/tr_09_01.png)

Create a new job and call it something without spaces! Jenkins creates a directory of the same name on the filesystem, but pip (or virtualenv?) will choke on spaces. Then select "Build a free-style software project".
    
To clone a git repo, you can use the [Jenkins GIT plugin](http://wiki.jenkins-ci.org/display/JENKINS/Git+Plugin). Once installed, go to "Configure System" and under "Git plugin" set the variables for Global "Config user.name" and "Global Config user.email" (required by the plugin to tag the source on each build).


![](/assets/tr_09_02.png)

Return to your project and under "Source Code Management", configure the repo you want to clone. I pass the git Read-Only URL.

![](/assets/tr_09_03.png)

If you run "Build Now", it should clone your Github repo. You can make sure the files show up under your project's "Workspace".

![](/assets/tr_09_04.png)

#### Run tests, build reports

Now we have the Python source code, we want to install it in a virtualenv. Under "Build", add a build step "Execute shell":

![](/assets/tr_09_05.png)

... and tweak the following code to fit your needs:

```python
PYENV_HOME=$WORKSPACE/.pyenv/

# Delete previously built virtualenv
if [ -d $PYENV_HOME ]; then
    rm -rf $PYENV_HOME
fi

# Create virtualenv and install necessary packages
virtualenv --no-site-packages $PYENV_HOME
. $PYENV_HOME/bin/activate
pip install --quiet nosexcover
pip install --quiet pylint
pip install --quiet $WORKSPACE/  # where your setup.py lives
nosetests --with-xcoverage --with-xunit --cover-package=myapp --cover-erase
pylint -f parseable myapp/ | tee pylint.out
```

The environment variable `$WORKSPACE` is made available during the script execution, it's the path to where Jenkins creates your build, e.g., `/var/lib/jenkins/jobs/foo/workspace/`.

The package `nosexcover` (don't misread it) is a nose plugin that introduces the `--with-xcoverage` nose option. It generates Cobertura-style XML reports.


#### Interpreting reports

When nose runs, it will generate report files in your workspace that Jenkins has to interpret.

* `nosetests.xml`: This file is generated by the `--with-xunit` option and can be interpreted by checking "Publish JUnit test result report"

    ![](/assets/tr_09_06.png)

* `coverage.xml`: The coverage file is generated by `--with-xcoverage`. Jenkins can interpret this report after installing the Cobertura plugin. It will be available as "Publish Cobertura Coverage Report", and the report pattern must be **/coverage.xml.

    ![](/assets/tr_09_07.png)

* `pylint.out`: For this one, you have to install the Violations plugin, which will make the checkbox "Report Violations" available. The plugin supports a bunch of different reports. Look for `"pylint"` and enter `**/pylint.out` as the "XML filename pattern".

![](/assets/tr_09_08.png)

Run "Build Now" and tweak the Shell script until nose runs all the way through (regardless if your tests pass). Make sure the report files are generated. Eventually, you will get nice charts on your job's page.

![](/assets/tr_09_09.png)

![](/assets/tr_09_10.png)

![](/assets/tr_09_11.png)


#### Github, notify Jenkins!

Finally, we want to run the build every time your Github project receives new code (push). Let's have Jenkins ready to receive notifications from Github. We need to check "Trigger builds remotely (e.g., from scripts)".

![](/assets/tr_09_12.png)

Once enabled, set the "Authentication Token" to, e.g., GIT_PUSH_NOTIFY.

Now go to your Github project page, click the "Admin" button to configure a "Post-Receive URLs" service hook, and copy/paste the URL given under the "Authentication Token" input field.

![](/assets/tr_09_13.png)

Finally replace, the `JENKINS_URL` part by the URL to your own Jenkins server. Github has a "Test hook" button to simulate a code push and trigger an actual HTTP call. Jenkins should start building your Python project automatically.


















































