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
* Practice the Acceptance - Unit test Cycle
* Learn about adding associations between models
 - `belongs_to`
 - `has_many`
* Learn about nested routes in Rails
* Group challenge
* Acceptance-Unit Test challenge is a pair programming challenge

### Head coach: Thomas

### Guide
- **Monday:**
  - [ ] Morning: How Rails is different than Sinatra and why you used Sinatra in week 4 incl. overview of where things are in Rails - Thomas
  - [ ] Morning: Introduce the Acceptance-Unit Test Cycle in Rails w/ challenge - Raoul (split up in pairs)
- **Tuesday:**
  - [ ] Morning: Check the submissions of the AUT code on GitHub - All Coaches 
  - [ ] Morning: Introduce the Legacy Code Challenge - Magnus
  - [ ] Rails demo: routing (plus resources) and params (plus sanitation) - Raoul (resource: https://www.youtube.com/watch?v=y57OnWV6dRE)
- **Wednesday:**
  - [ ] Morning: Rails demo: Active Record (migrations, associations, CRUD functions) - Raoul
  - [ ] Afternoon: In depth Rails demo: Most common helpers (focus on forms) - Thomas
      - https://m.patrikonrails.com/rails-5-1s-form-with-vs-old-form-helpers-3a5f72a8c78a?gi=c7e478d9361b
- **Thursday:**
  - [ ] Morning: Validations (conditional and custom) in Rails and instance methods - Raoul
  - [ ] Afternoon: Adding associations and nested routes (use the AUT app and extend it with commenting on articles functionality. See the weekend challenge). - Thomas
  - [ ] Talk about the midcourse project - Thomas
- **Friday:**
  - [ ] Introduce the Weekend Challenge - Thomas 
  - [ ] Retro - All coaches
  
  
