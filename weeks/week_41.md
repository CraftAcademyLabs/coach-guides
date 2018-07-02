## Week 4
### Introduction to this week

#### Swedish
**Parprogrammering och Användarorienterad utveckling**

Vi inleder denna vecka med att lägga grunden för ett onlinesystem som låter användarna beställa mat online (SlowFood Challenge). Vi introducerar Ruby on Rails, ett ramverk för webbaserade applikationer och ger deltagarna en första inblick i hur man jobbar med agila utvecklingsmetoder med fokus på Behavior Driven Development. SlowFood Challenge handlar även om designmönstret Model-View-Controller, relationsdatabaser och funktioner för användarregistrering, autentisering och auktorisering. Vid veckans slut är vi redo att gå live med SlowFood Online och vi publicerar vårt system med hjälp av Heroku. För att underlätta och automatisera vår deploy-process använder tekniker som Continuous Integration och Continuous Deployment.

#### English
**Pair Programming and User-Oriented Development**

This week we begin to lay the foundation for an online system that allows users to order food online. We introduce Ruby on Rails,  a popular and in-demand framework that allows programmers to build complex, exciting web applications, and give you your first insight into Agile practices, focusing on Behavior Driven Development. The Slow Food Challenge is also about thinking more deeply about how the pieces of an application fit together, using advanced techniques such as user registration, authentication and authorization. At the end of the week, we are ready to go live with the Slow Food Online application and we deploy our system using Heroku. To facilitate and automate our deploy process we use techniques such as Continuous Integration and Continuous Deployment.


### Learning objectives
This is a group challenge and the students are supposed to work as a team.
* Learn about basic Agile principles
  - self organizing teams
  - the importance of planning your work
* Learn about Ruby on Rails
  - understand the concept of ORM's vs SQL (ActiveRecord)
  - understand the MVC structure
    - controllers
    - routes
    - models
    - relation between models
    - concept of `params` (See: https://www.youtube.com/watch?v=y57OnWV6dRE)
* Learn about User Authentication using Warden
* Learn about the hardships that will occur if we can't read documentation for libraries we use in our projects (gems).
* Basics of Test- and Behavior Driven Development or Acceptance - Unit Test cycle.
* Really embrace and understand the benefits of Pair Programming && collaboration using Git and GitHub
* Learn about deployment to Heroku and the benefits of services like Heroku, DigitalOcean and AWS

### Weekend challenge
SlowFood (Rails) (User Interface/UX) - Note: group challenge
The weekend is devoted to focus on the User experience of the app. Here we start looking at the styling. We want them to notice that the planning they did in the initial stage was not detailed enough and that they missed to focus on the user.
### Learning objectives
* All of the above
* Also learn about:
  - the importance of focusing on what the end-user sees on the site.
  - the true benefit of working with Lo-Fi's as a way to foresee what the user will experience when using the app and how much that helps in our development process.
* Front-end technologies
  - CSS frameworks
  - CDN's vs Gems vs Manually including the CSS framework code (repetition)

### Head Coach: Thomas

### Guide
- **Monday:**
    - [ ] Morning: Brief overview of where things are in Rails (recap focus on MVC, config). - Faraz

    - Basic application structure
    - Rails doctrine, etc...
    - Boilerplate (https://github.com/CraftAcademy/boilerplate)
  - [ ] Morning: Introduce the Acceptance-Unit Test Cycle in Rails (Slow Food) - Thomas
  - [ ] Students work on AUT Exercise
- **Tuesday:**
  - [ ] Morning: Params, sanitation - Thomas
  - [ ] Morning: Introduce Slowfood Challenge - Thomas
  - [ ] Morning: Do a basic overview of a Design Sprint. - Faraz
  - [ ] Afternoon: Do a overview of Relational Databases (the concept, SQL, ORM's, etc..) - Raoul
- **Wednesday:**
  - [ ] Morning: Rails demo: Advanced Routing (plus resources, nested routes, associations) (use the AUT app and extend it with commenting on articles functionality. See the weekend challenge)- Raoul
  - [ ] Morning: Rails demo: Active Record (migrations, associations, CRUD functions) - Raoul

- **Thursday:**
    - [ ] Talk about the midcourse project - Thomas

- **Friday:**
  - [ ] Introduce the Weekend Challenge - Faraz
  - [ ] AUT demo using Sails - Oliver
  - [ ] Tech interview training - All coaches
