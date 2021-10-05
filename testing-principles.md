# Philosophy of Automated Testing

The purposes
1. Confidence - testing
2. Fast feedback loop - automate
3. Written down - documentation

An automated test suite is a tool.  As we know every tool has a purpose. An automated test suite serves two purposes.  The first purpose to note is the automation itself.  There are two main reasons to automate testing.  First, automating testing reduces the total amount of time needed to test. Every person's time, attention and mental capabilities are valuable. By automating the testing process we free brilliant minds to solve problems sooner.  The second reason to automate testing is to dramatically improve an engineer's feedback loop.  It is critically important to note that the automation only exists because the test suite is valuable. Never spend time automating tasks which aren't valuable. 

So, what is the purpose of test suite, why is it valuable?  Consider this tweet from Kent C. Dodds.

> The more your tests resemble the way your software is used, the more confidence they can give you.
> - Kent C. Dodds [source](https://twitter.com/kentcdodds/status/977018512689455106)

This tweet from 2018 highlights main purpose of testing as well as a hard truth.  The purpose of testing is not to find bugs.  If finding bugs were the true purpose then we would measure the success of testing by the number of bugs found. We all know intuitively the number of bugs found during the testing process is not a good measurement of success. Finding bugs is merely the result of the testing process. So, if finding bugs isn't the purpose of testing, what is? The true purpose of testing is confidence that the system is working as intended.  It's the confidence that confirms what we've built works and can be shipped to its customer, and you can move on to the next thing.

As noted, this tweet also contains a hard truth.  Not all tests are equal. That is to say, when fully executed, not all tests suites give you the warm fuzzy confident feeling when you ship the code. This could be for a couple of reasons.  First, the test suites are incomplete.  It has limited test cases.  If you know the test suite is missing key test cases, you will not so confident your shipped product is working as expected.  Secondly, some tests in the test suite may be testing the wrong thing. The prinicples outlined below are intended to guide the development of a well written automated test suite.  An automated test suite that when executed, grants a high level of confidence that the next code shipment which devlivers value to the customer the first time.


# Testing Principles

The following principles will enable effective development for automated tests suites that will enable the development team to ship software as quickly as possible, _with confidence!_

### 1. Write tests that reseble how your software is used
  
> The more your tests resemble the way your software is used, the more confidence they can give you.
> - Kent C. Dodds [source](https://twitter.com/kentcdodds/status/977018512689455106)

- Write tests from the perspective of the user
- Use of tesing library
  - Which query should I use? avoid test id
  - RTL designed to promote using UI as it was intended
- Use of cypress pre-e2e and e2e

### 2. Well written tests are essential documentation

> A failing test should read like a high-quality bug report.
> - Eric Elliot, [5 Questions Every Unit Test Must Answer](https://medium.com/javascript-scene/what-every-unit-test-needs-f6cd34d9836d) 

- assert the code is correct - leading to confidence.
- 5 Questions:
  1. What were you testing?
  2. What should it do?
  3. What was the output (actual behavior)?
  4. What was the expected output (expected behavior)?
  5. How can the test be reproduced?

- use of jest conventions - consistency - speeds up developer loop
  
### 3. Value Test Case Coverage over Code Coverage

> Code coverage is a measurement that highlights potentially valuable tests cases may not be covered.
     
Code coverage is only a metric. It is not the real goal.  As a result we _cannot_ define success with code coverage. Testing is about confidence not metrics.  Our confindence is derived from knowing that the test suite covers as many valid test cases as possible. A single feature or use case/user story likely has several valid test cases. One of those test cases, the "happy path" case as an example, may very well cover more than 80% of the total code surface.  This is especially true with the use of tools like Cypress. But what about those "edge cases", "negative cases", "error case"?  These cases have direct impact on the user and overal system. For that reason these cases are important too!  Writing these tests gives us additional confidence that when the software will fail gracefully.

When writing tests, carefully consider all of the possible valid uses cases and write a test for each.  The result will be increased confidence that the software is working correctly.

- Discernment is required to understand if spending the engergy to fill in coverage gaps is useful.

### 4. Optimize for fastest possible developer feedback loop.

   "Shift Left", Identify issues as early as possible.  Starts with unit tests, then functional/integration tests, then e2e tests
   
> The sooner you catch a failure  

The time between when a feature or change is implemented and when it's test cases have been executed is the feedback loop.  As example, a new field to a form so its data can be persisted to the database. Imagine, the UI portion of the code is complete and we are ready to test.  Now, start your timer and execute these steps:

- Commit the code to the repository
- Deploy the code to the development server, wait for deployment
- Manually Open the browser, navigate to the page, test the funcationality works
- Stop the timer

How long did it take to execute these steps?  5 minutes? 20 minutes? This is the feedback loop. After the test cases are complete, you can know what adjustments need to be made.  After you make those adjustments, then you perform the tests again.  It's obivious that a faster feedback loop is advantagous.  

Automation is the most critical method for increasing the feedback loop.  As a result if a task is valuable and can be automated, it should be automated. This is why CI/CD exists and why we automate tests.  However, just automating the tests may not enough.  We want to optimize for the fastest possible feedback loop. This means making careful considerations related to: 

- Where are located in the source code
- How quickly tests can execute
- Which types of tests are used: unit tests, integration tests, e2e tests, etc
- How much effort is needed to create tests

### References

[Which is more important, line coverage or branch coverage?](https://ardalis.com/which-is-more-important-line-coverage-or-branch-coverage/)
[Measure manage Quote](https://medium.com/centre-for-public-impact/what-gets-measured-gets-managed-its-wrong-and-drucker-never-said-it-fe95886d3df6)
[5 Questions Every Test Should Answer](https://medium.com/javascript-scene/what-every-unit-test-needs-f6cd34d9836d)
