## Week 4
### Introduction to this week

#### Swedish
**Parprogrammering och Användarorienterad utveckling**

Vi inleder denna vecka med att lägga grunden för ett onlinesystem som låter användarna beställa mat online (SlowFood Challenge). Vi introducerar ett ramverk för webbaserade applikationer ([Sinatra](http://www.sinatrarb.com/)) och ger deltagarna en första inblick i hur man jobbar med agila utvecklingsmetoder med fokus på Behavior Driven Development. SlowFood Challenge handlar även om designmönstret Model-View-Controller, relationsdatabaser och funktioner för användarregistrering, autentisering och auktorisering. Vid veckans slut är vi redo att gå live med SlowFood Online och vi publicerar vårt system med hjälp av Heroku. För att underlätta och automatisera vår deploy-process använder tekniker som Continuous Integration och Continuous Deployment.

#### English
**Pair Programming and User-Oriented Development**

This week we begin to lay the foundation for an online system that allows users to order food online. We introduce Sinatra, a framework for web based applications, and give you your first insight into Agile practices, focusing on Behavior Driven Development. The Slow Food Challenge is also about thinking more deeply about how the pieces of an application fit together, using advanced techniques such as user registration, authentication and authorization. At the end of the week, we are ready to go live with the Slow Food Online application and we deploy our system using Heroku. To facilitate and automate our deploy process we use techniques such as Continuous Integration and Continuous Deployment.

### Week Lab
[SlowFood (Sinatra)](https://craftacademy.gitbooks.io/coding-as-a-craft/content/slow_food/slow_food.html)

### Learning objectives
This is a group challenge and the students are supposed to work as a team.
* Learn about basic Agile principles
  - self organizing teams
  - the importance of planning your work
* Learn about Sinatra
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
SlowFood (Sinatra) (User Interface/UX) - Note: group challenge
The weekend is devoted to focus on the User experience of the app. Here we start looking at the styling. We want them to notice that the planning they did in the initial stage was not detailed enough and that they missed to focus on the user.
### Learning objectives
* All of the above
* Also learn about:
  - the importance of focusing on what the end-user sees on the site.
  - the true benefit of working with Lo-Fi's as a way to foresee what the user will experience when using the app and how much that helps in our development process.
* Front-end technologies
  - CSS frameworks
  - jQuery
  - CDN's vs Gems vs Manually including the CSS framework code (repetition)

### Head Coach: Thomas

### Guide
- **Monday:**
  - [ ] Morning: Three tier Architecture - Raoul
  - [ ] Morning: Introduce the week lab - Thomas
  - [ ] Afternoon: Introduce Sinatra - the important parts and what they do - Faraz (talk from MVC perspective restaurant   example)
  - [ ] Afternoon: Do a basic overview of a Design Sprint. - Faraz (provide a checklist for the system EdX)
- **Tuesday:**
  - [ ] Morning: Do a overview of Relational Databases (the concept, SQL, ORM's, etc..) - Raoul
  - [ ] Afternoon: Associations - Raoul
- **Wednesday:**
  - [ ] Morning: An Acceptance-Unit test demo - Thomas (Create a view to display dishes, create association and create a Product model)
  - [ ] Morning: Review of Pair Programming concepts and Git & GitHub - Thomas & Faraz [Demo] -- Not really needed for this cohort
  - [ ] Afternoon: CodeWars Hour - Raoul
- **Thursday:**
  - [ ] Morning: Introduce Heroku, walkthrough of how to deploy - Raoul
  - [ ] Afternoon: Do a brief introduction to frameworks (Sinatra, Rails, Node, JS based frameworks, etc). - Thomas
- **Friday:**
  - [ ] Introduce the Weekend Challenge - Faraz (UX of the slowfood challenge)
  - [ ] Tech Interview Training - with https://github.com/CraftAcademy/week3-assessment
  - [ ] Retro - Faraz + Hanna
