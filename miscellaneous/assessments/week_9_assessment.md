# Setting up a project
## Rails with testing frameworks and CI

This week we would like to assess your ability to scaffold a new Rails project. 

**Assessment time - up to 45 minutes**

As you work on this exercise, please 'think aloud.' That means verbally describing your mental process as it develops, including the doubts and questions you have, the solution strategies you consider, and the reasons that justify your decisions.”

### Think Aloud Clarification

The 'Think-aloud' protocol involve the participant thinking aloud as he are performing a set of specified tasks or working on an excercise. The participant are asked to say whatever comes into his mind as he complete the task. This might include what he is looking at, thinking, doing, and feeling. This gives the coach valuable insight into the participant's cognitive processes (rather than only their final product), to make thought processes as explicit as possible during task performance. Sessions should be recorded so that coaches can go back and refer to what participants did and how they reacted.


## Challenge

Your project team will be starting a new project - a crowdsourced transportation platform called ** Unter **. You ware assigned the following chores by your team:

### Set up main repository
**Description**

>As a developmet team
>In order to be able to collectively work on the same codebase
>We would like to have a main repository on GitHub we all can use as the upstream repository_

**Tasks (Acceptance Criteria)**

- [ ] Set up a repository on GitHub (Please treat your own account as the account for this organization for the sake of this exercise)
- [ ] Create a `development` branch and set it as the main branch of the project
- [ ] Share repo with team

### Set up application structure

**Description**

>As a developent team
>In order to be able to start adding features
>We would like to have an basic application structure_ 

**Tasks (Acceptance Criteria)**

- [ ] Scaffold a Rails application
- [ ] Turn off generators for helpers, assets and all specs (accept model specs)
- [ ] Clean up the generated code from unnecessary comment for good readability


### Set up testing environment

**Description**

>As a developent team
>In order to be able to make sure my code is doing what it is supposed to do
>We would like to be able to write and run automated tests_

**Tasks (Acceptance Criteria)**

- [ ] Add and configure Cucumber for Acceptance tests
- [ ] Add and configure Rspec for Unit and Request specs


### Set up Continious Ingegration

**Description**

>As a developent team
>In order to make sure that the code we add to the code base is functional
>We would like to run full test suite on a remote service_

**Tasks (Acceptance Criteria)**

- [ ] Set up CI on Semaphore or Travis

### Set up Test Coverage Metrics
**Description**

>As a developent team
>In order to see how much of our code is covered in tests
>We would like to measure test coverage using a remote service__ 

**Tasks (Acceptance Criteria)**

- [ ] Set up Coveralls for the main repository
- [ ] Add and configure Coveralls for RSpec and Cucumber
- [ ] Coverage results needs to be merged in order to get metrics from both tools

### Set up Continious Deployment
**Description**

>As a developent team
>In order to automate the deployment process during development
>We would like all code that has been merged in to the code base to be deployed to a server_

**Tasks (Acceptance Criteria)**

- [ ] Create an application on Heroku
- [ ] Set up deployment using the CI tool
