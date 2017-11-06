## Week 5 Rails Week
### Introduction to this week

#### Swedish
**Software as a Service med Ruby on Rails**

Den här veckan introducerar vi deltagarna till Ruby on Rails - ett ramverk som hjälper programmeraren att följa designmönstret Model-View-Controller (MVC) och lär dem att jobba efter grundprinciperna Convention Over Configuration (Konvention före konfiguration) och Don't Repeat Yourself (DRY) som går ut på att motverka duplicering av kod. Vi introducerar också mer omfattande teststrategier och befäster deltagarnas kunskaper för hur de använder tester i sin utvecklingsprocess. Vi forsätter med att fördjupa oss i Rails och går igenom mer avancerade tekniker för hur man använder externa bibliotek (gems), API'er, websockets, mm."

#### English
**Software as a Service with Ruby on Rails**

This week we introduce Ruby on Rails, a popular and in-demand framework that allows programmers to build complex, exciting web applications. We present more complex testing strategies and help you understand how testing can greatly improve your workflow. This week we deepen our knowledge of external libraries (gems), APIs, websockets, etc.

### Week Lab
The students are introduced to Ruby on Rails this week. We are exposing them to the 'magic' of Rails AND to the best practice of using various testing frameworks to drive their development.

The Legacy Code Challenge aims at allowing students to write both acceptance tests and unit tests for a ready made application
1. Acceptance-Unit Test Cycle with Rails (individual assignment)
2. Legacy Code challenge (pairing assignment)


### Learning objectives
* Learn about Ruby on Rails
  - structure of a RoR application
  - params
  - routes (resources, members, etc)
  - most common helpers
  - migrations
  - CRUD controller actions
* Learn about the Model-View-Controller pattern
* Learn to work with legacy code
* Learn about best practices in Rails: DRY, Convention Over Configuration
* Learn how to identify what gems provide a lot of functionality and how to read and use documentation
* Learn about how to use tests (High level acceptance tests and Low level unit tests) to drive the development process.
* Practice Team collaboration
  - planning and assigning tasks
  - git flow in teams

### Weekend challenge
Comments Challenge
Extending the basic Rails application that you created at the beginning  of the week. Your task is to add a feature that allows visitors to comment on published articles. Visitors should be able to comment on an article and optionally provide their email address that will be displayed together with the comment.

### Learning objectives
* Practive the Acceptance - Unit test Cycle
* Learn about adding associations between models
 - `belongs_to`
 - `has_many`
* Learn about nested routes in Rails


### Guide
- **Monday:**
  - [ ] Morning: How Rails is different than Sinatra. - Raoul
    - Why you used Sinatra in week 3
    - Brief overview of where things are in Rails.
    - Introduce the Acceptance-Unit Test Cycle in Rails w/ challenge
- **Tuesday:**
  - [ ] Morning: Check the submissions of the AUT code on GitHub - Philip, Sigu and Raoul
  - [ ] Morning: Introduce the Legacy Code Challenge - Raoul
    - Rails demo: routing (plus resources) and params (plus sanitation)
  - [ ] Afternoon: Rails demo: Active Record (migrations, associations, CRUD functions) - Raoul
- **Wednesday:**
  - [ ] Morning: In depth Rails demo: `form_for` vs `form_tag` - Raoul **Is it relevant?**
  - [ ] Afternoon: In depth Rails demo: Most common helpers - Raoul
- **Thursday:**
  - [ ] Morning: Validations in Rails and instance methods - Raoul
  - [ ] Afternoon: Adding associaions and nested routes (use the AUT app and extend it with commenting on articles functionality. See the weekend challenge). - Raoul
- **Friday:**
  - [ ] Introduce the Weekend Challenge - Thomas (if @office) or Raoul
  - [ ] [Assessment](https://github.com/CraftAcademy/coach-guides/blob/master/miscellaneous/assessments/week_5_assessment.md)
