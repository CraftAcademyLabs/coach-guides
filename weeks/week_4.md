## Week 4 Rails Week
### Introduction to this week

#### Swedish
**Software as a Service med Ruby on Rails**

Den här veckan dyker vi djupare in i Ruby on Rails - ett ramverk som hjälper programmeraren att följa designmönstret Model-View-Controller (MVC) och lär dem att jobba efter grundprinciperna Convention Over Configuration (Konvention före konfiguration) och Don't Repeat Yourself (DRY) som går ut på att motverka duplicering av kod. Vi introducerar också mer omfattande teststrategier och befäster deltagarnas kunskaper för hur de använder tester i sin utvecklingsprocess. Vi forsätter med att fördjupa oss i Rails och går igenom mer avancerade tekniker för hur man använder externa bibliotek (gems), API'er, websockets, mm.


#### English
**Software as a Service with Ruby on Rails**

Software as a Service - Work the web! This week we introduce Ruby on Rails and introduce strategies to work effectively with legacy code. We present more complex testing strategies and help you understand how testing can greatly improve your workflow. This week we deepen our knowledge of external libraries (gems), APIs, websockets, etc.

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

### Head coach: Faraz
#### First Line: Thomas

### Guide
- **Monday:** RED day


- **Tuesday:** 
  - [ ] Morning: Introduce Rails & AUT Part 1 (intro to Articles challenge, Factorybot, Fixtures) - Thomas
  - [ ] Morning: Introduce Rails & AUT Part 2 (intro to Articles challenge, Factorybot, Fixtures) - Thomas
  - [ ] Introduce to web architecture (MVC) - Thomas or Faraz (make it a discussion) - Faraz


- **Wednesday:**
  - [ ] Morning: Check the submissions of the AUT code on GitHub - All Coaches
  - [ ] Morning: Introduce the Legacy Code Challenge - Faraz
  - [ ] Afternoon: Mobsession making and reviewing PRs - Faraz, Oliver & Thomas (timebox for max 30 min 15 min coding 15 min review)

- **Thursday:**
  - [ ] Morning: Validations in Rails and instance methods - Thomas
  - [ ] Morning: The concept of the params hash [Use this as reference](https://www.youtube.com/watch?v=y57OnWV6dRE) - Faraz
  - [ ] Afternoon: Introduce Heroku, walkthrough of how to deploy [For Reference](https://devcenter.heroku.com/articles/getting-started-with-ruby)- Oliver - Make them deploy the AUT challenge ( problem with buildpack for bundler 2 add a specific buildpack) - Make sure by the end of the day through submissions OLIVERRR
  
  This is the buildpack you need to use (if you add it from CLI): 

  ```
  heroku create --buildpack https://github.com/bundler/heroku-buildpack-bundler2.git
  ```
      
- **Friday:**
  - [ ] Afternoon: Rails demo: routing (plus resources) [Slides](https://docs.google.com/presentation/d/1Eu_x1eO9Zkmkb1RyflUONTipOjnDUtfUmSabO8-jyoQ) - Faraz (`--skip-routes` `--skip-views`)
  - [ ] Introduce the Weekend Challenge - Faraz 
  - [ ] Retro - All coaches  
  
