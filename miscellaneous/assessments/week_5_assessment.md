As you work on this exercise, please 'think aloud.' That means verbally describing your mental process as it develops, including the doubts and questions you have, the solution strategies you consider, and the reasons that justify your decisions.”

### Think Aloud Protocol

The 'Think-aloud' protocol involve the participant thinking aloud as he are performing a set of specified tasks or working on an excercise. The participant are asked to say whatever comes into his mind as he complete the task. This might include what he is looking at, thinking, doing, and feeling. This gives the coach valuable insight into the participant's cognitive processes (rather than only their final product), to make thought processes as explicit as possible during task performance. Sessions should be recorded so that coaches can go back and refer to what participants did and how they reacted.

## Setup

Return to the repository you created at the beginning of the week when we covered the Acceptance-Unit Test Cycle. You will be working on that code base during this assessment.

## Challenge
Your task is to modify the feature you've created and make sure that information about the Author of the Article is being displayed on the view alongside the creation date.

Note that we will NOT stub out (create fake) dates so your tests will only go green today. If you run them tomorrow, they will fail. Think about it as the final question in this challenge is to explain why that is.

Modify your feature file to look like this:
```gherkin
Feature: List articles on landing page
  As a visitor,
  when I visit the application's landing page,
  I would like to see a list of articles

  Background:
    Given the following articles exist
      | title                | content                          | author |
      | A breaking news item | Some really breaking action      | Thomas |
      | Learn Rails 5        | Build awesome rails applications | Faraz  |

  Scenario: Viewing list of articles on application's landing page
    When I am on the landing page
    Then I should see "A breaking news item"
    And I should see "Some really breaking action"
    And I should see "Written by Thomas at 2018-01-12"
    And I should see "Learn Rails 5"
    And I should see "Build awesome rails applications"
    And I should see "by Faraz at 2018-01-12"
```

1. Your primary task is to make these scenarios pass. You WILL get errors running the background steps so you need to address that using the Acceptance-Unit Test approach.

2. We want you to add a debugger to your application (unless it's already added) and demonstrate that you know how to set a break point in:
  * A step definition. (What kind of objects can you see?)
  * In the model. (Can you Access `self` and what is that?)

3. Describe why the scenarios will not pass if you run them tomorrow?

4. Create a Pull Request toward your own repository's `master` branch with a title and a PR description that you consider to be of high quality. 
