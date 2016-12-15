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
      | Learn Rails 5        | Build awesome rails applications | Amber  |

  Scenario: Viewing list of articles on application's landing page
    When I am on the landing page
    Then I should see "A breaking news item"
    And I should see "Some really breaking action"
    And I should see "Written by Thomas at 2016-12-15"
    And I should see "Learn Rails 5"
    And I should see "Build awesome rails applications"
    And I should see "by Amber at 2016-12-15"
```

1. Your primary task is to make these scenarios pass. You WILL get errors running the background steps so you need to address that using the Acceptance-Unit Test approach.

2. We want you to add a debugger to your application (unless it's already added) and demonstrate that you know how to set a break point in:
  * A step definition. (What kind of objects can you see?)
  * In the model. (Can you Access `self` and what is that?)

3. Describe why the scenarios will not pass if you run them tomorrow?

4. Create a Pull Request toward your own repository's `master` branch with a title and a PR description that you consider to be of high quality. 
