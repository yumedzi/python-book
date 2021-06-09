## Dev unit testing vs QA automated testing

There are some questions that are hard for understanding by a lot of people:
* Who should write automated tests?
* Should developer write tests when there is a QA team?
* Which tests should the developer write and which ones - the QA engineer?

Yes, unit tests are essential is the form of Functional testing. But in practice, Unit tests and Functional tests are separated by many nuances outlined below. Sometimes Functional tests are named as End-to-end tests.

### Dev unit testing

Unit testing is a software testing method by which individual units of code are tested in isolation. The purpose of unit testing is to isolate the smallest testable parts of an API and verify that they function properly in isolation. A unit test can verify different behavioral aspects of the system under test(SUT), but mainly it verifies that the SUT produces the correct results.

From the developer’s perspective, the purpose of unit testing is to create a robust codebase with a minimal cost. Another important purpose of unit tests is to provide documentation for high-level testing, i.e. Integration testing and Functional testing.

Developer's unit tests follow `White box testing technique` - when the test knows exactly what the unit should or should not return. If the test failes - the developer will know precisely which part of the application behaves incorrectly.

So, as the summary, the main purposes of unit tests written by developers:
* Verify that an individual unit is working correctly in isolation before it is combined with other components.
* To ease the updating or adding of new features:
    * Checks that each component is working in isolation from others - this allows to focus on it's requirements
    * Checks that new code doesn't break exisiting core functionality
* Proving that bug fixes are valid and indeed resolve the issues
    * Ideally each bug fix should be supplied with related unit tests covering target issue
* Quick method of checking the status of the code
    * This maybe needed after updating the version of some library in use or other dependencies
    * Key point - the speed of checks, no dev time wasted on waiting for long time. Because of this tests cover all possible combinations of input data if this is quick, otherwise - only main of them.

Main questions during writing each unit test / test case:
* Which component is under test?
* What is the expected behavior?
* What was the actual result?
* What is the expected result?

### QA functional testing

In functional end-to-end testing, a tester isn't concerned with the actual code, rather he/she need to verify the output based on given the user requirements with the expected output.

The prime objective of this type of testing is to check the functionalities of the system. Functional tests check the entire application, its hardware, and networking infrastructure, from the front end UI to the back-end database systems. In that sense, functional tests are also a form of integration testing, ensuring that different components are working together as expected.

QA's end-to-end tests follow `Black box testing technique` - when the test does not know the internals of the application. It feed input data and expect specific output or other determined behavioral changes to happen.

Unlike unit tests, the functional tests don't tell what is broken or where to locate the failure in the code base. They just tell you something is broken. 

As the summary, the main purposes of automated tests written by QA engineers:
* Automate time-consuming manual testing
    * Usually it all starts with manual testing and compiling a big list of test scenarios that later should be ideally converted into automated tests.
* To check the flow end-to-end
    * Contrary to dev unit tests QA engineers check the process works from the beginning to the end according to requirements/specifications.
    * Old checks coexist with recently added to ensure that there is no regression.
* Run a ton of tests to cover all possible scenario and data variation
    * Even if these tests take hours - it's OK

Difference between DEV and QA tests:

|Factor            | DEV unit tests     | QA automated tests  
|------------------|--------------------|--------------------------------------------------
| Purpose          | Individual unit is working correctly in isolation before it is combined with other components. | Testing end-to-end functionality per Tech specification/requirements.
| Complexity       | Easy to write and fast to execute | More complex and slow - end-to-end check of each stage
| Technique        | White box testing  | Black box testing
| Focus            | Individual module/unit works as expected | Entire application works as expected
| Coverage         | Number of units, code lines  | Number of Tech requirements
| Maintenance      | Low        | High
| Programming language | The same of the code | Any language, usually: `Python`, `Java`
| Changes          | High       | Low
| Written by       | Developers | QA engineers
| Written at       | Start of the development | When feature is added, ready for tests
| Automation       | Must be automated      | Manual + automated