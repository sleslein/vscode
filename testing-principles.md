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

1. Write tests that reseble how your software is used
  
  - Notes on what well written means
    - Eric Elliot's Every test should answer 5 questions.
    - use of jest conventions
    - Use of tesing library
    - Use of cypress pre-e2e
  
2. Value Test Case Coverage over Code Coverage

    Automated tests are for confidence, not metrics
    - Code Coverage is not a measure of success. Code coverage is a measurement that highlights potentially valuable tests cases may not be covered.  


3. Optimize for fastest possible developer feedback loop.

   "Shift Left", Identify issues as early as possible.  Starts with unit tests, then functional/integration tests, then e2e tests


## Rants.notes

# Automated Testing Philosophy

**Purpose of this document:** Give team a better understanding/perspective of\*\*
**The battle over automated testing rages on, but in new ways. **
**You're writing your automated tests wrong! **

- Maybe only in case of UI testing?

https://testing-library.com/docs/guiding-principles

## Outline

- Purpose of document

  - Give better perspective on what, why, how we test.
  - Contrary to belief, not about code coverage, or number of tests.
  - Positive impact on how we develop software.

  The true purpose of testing softare is self-evident. Testings ensures the quality of of the software. It has always been and will always be an essential part of the software development process. Effective testing is an expensive and repetative process which never ends. It requires the time and energy of many. Those testing are performing a noble important task. We have beautiful creative minds, don't we? When focused our minds can solve the problems which haunt us. However, our beautiful creative minds cannot recognize their true potential and solve important problems while performing the reptative task of testing. So, it is not surprising that we have a desire to automate as much testing as possible.

  Automated testing has always been a battle. In the early days the battle was usually organizational infighting. Automated testing has an upfront cost. In light of the upfront costs, it was challening to convince your engineering colleagues to write unit tests along side features. It was a challenge to convince management and leadership of the benefits of automated testing knowing it would have an impact on delivery schedules. Thankfully, in many organizations those dark days are over!. Automated testing is becoming the standard.

  Today, however, the autotmated testing battle rages on, in a different and unexpected way. As an organization understanding of the benefits of automated testing hit critical mass, leadership and management get invovled. This is a good thing because buy-in from leadership/management is absolutely required for lasting and meaningful change to any process. With leadership and management on board casting a pro-automated testing vision, engineers can move forward with peace of mind. With the vision in place, leaders and managers look to measure the progress of the vision. This is where the present battle starts to unfold.

  ## "Whatever gets measured gets managed..."

  In order to measure something you have to quantify it. So, as it relates to automated testing, what do we quantify and measure? In many cases the default measurement of automated testing success has become code coverage. Now, don't mistake me. Code coverage is an important metric and it should be measured and reported. The real problem is two fold. First, code coverage as become THE metric which defines success. Meaning, code coverge is the primary metric leadership and management discuss when it comes to the effectiveness of a teams automated testing efforts. As the old saying goes, "whatever gets measured gets managed". This results in tests being written with the primary purpose of increasing code coverage. Writing these tests is often times very easy. These test however pose a serious problem. They don't offer any real value. Sure, leadership and management are appeased to see the metrics improve. However, a test written only with the purpose of code coverage in mind doesn't meet the true purposes of automated testing. They offer real confidence that a change didn't add a true regression bug. In fact they hurt, because they add noise to the codebase.

  - Merits of code coverage: It's a spotlight on missing test cases.

  As modern day software engineers in an engineering/tech company, we are constantly bombarded with the message that when it comes to automated testings, code coverage is king! L As a result we often define the success of our testing efforts soley on the code coverage metric.

  Let's review the benefits of automated testing. In doing so, lets also define why we test software.

  So, in summary, the main purpose of

- Purpose of Automated Testing

  - Confidence - This is the big idea!
  - Not about finding bugs
  - Testing always

- What do we test? ???? Keep specific to UI ????

  - Unit Tests
  - Integration Tests

- Purupose of Automated Testing

  - Faster feedback loop for Devs
  - Faster Development Cycles

- Purpose of Code Coverage
  - Not the goal of automated testing.
  - Leading indicator concerning which uses cases have been tested
    - Deep work, leading indicators
  -

### References

[Which is more important, line coverage or branch coverage?](https://ardalis.com/which-is-more-important-line-coverage-or-branch-coverage/)
[Measure manage Quote](https://medium.com/centre-for-public-impact/what-gets-measured-gets-managed-its-wrong-and-drucker-never-said-it-fe95886d3df6)
[5 Questions Every Test Should Answer](https://medium.com/javascript-scene/what-every-unit-test-needs-f6cd34d9836d)
