## Week 5
### Introduction to this week

#### Swedish
**Parprogrammering och Användarorienterad utveckling**

Vi inleder denna vecka med att lägga grunden för ett onlinesystem som låter användarna beställa mat online (SlowFood Challenge). Vi introducerar Ruby on Rails, ett ramverk för webbaserade applikationer och ger deltagarna en första inblick i hur man jobbar med agila utvecklingsmetoder med fokus på Behavior Driven Development. SlowFood Challenge handlar även om designmönstret Model-View-Controller, relationsdatabaser och funktioner för användarregistrering, autentisering och auktorisering. Vid veckans slut är vi redo att gå live med SlowFood Online och vi publicerar vårt system med hjälp av Heroku. För att underlätta och automatisera vår deploy-process använder tekniker som Continuous Integration och Continuous Deployment.

#### English
**Pair Programming and User-Oriented Development**

This week we begin to lay the foundation for an online system that allows users to order food online. We dive deeper into Ruby on Rails,  a popular and in-demand framework that allows programmers to build complex, exciting web applications, and give you your first insight into Agile practices, focusing on Behavior Driven Development. The Slow Food Challenge is also about thinking more deeply about how the pieces of an application fit together, using advanced techniques such as user registration, authentication and authorization. At the end of the week, we are ready to go live with the Slow Food Online application and we deploy our system using Heroku. To facilitate and automate our deploy process we use techniques such as Continuous Integration and Continuous Deployment.

### Teachable Course
[Software as a Service with Ruby on Rails](https://learn.craftacademy.co/admin/courses/667059/information)

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
    - relations between models
    - concept of `params` (See: https://www.youtube.com/watch?v=y57OnWV6dRE)
* Learn more about User Authentication
* Learn about the hardships that will occur if we can't read documentation for libraries (gems) we use in our projects.
* Learn more about Test- and Behavior Driven Development or Acceptance - Unit Test cycle.
* Really embrace and understand the benefits of Pair Programming & collaboration using Git and GitHub
* Learn about deployment to Heroku and the benefits of services like Heroku, DigitalOcean and AWS.

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

### Head Coach: Oliver
### Support coach: Thomas & Faraz
### Guide
- **Monday:**
  - [ ] Morning: Introduce Slowfood Challenge - Thomas [slides](https://docs.google.com/presentation/d/153hI_aRf88-7FBvmBcq7FOxMoLEzbi8VuugVygonY3E/edit?usp=sharing)
    - Use Rails 6
    - Release old video of Extracting info from user stories
    - Point to set up rails guide in course documentation (boilerplate)
  - [ ] Morning: Do a Overview of a Design Sprint - Faraz [slides](https://docs.google.com/presentation/d/1tXXZd1pl2Q3Rg9R85k_xmoZNBRKcQaPYKezCXglxXQ8/edit?usp=sharing)
  - [ ] Students go through stories and create lofis - From PT board
  - [ ] Afternoon: Setting up Semaphore and Continious deployment Also talk about coveralls - Oliver [CI and CD slides](https://docs.google.com/presentation/d/1Y0YBeRV9Da9exfEQXZFyJob0d6pbBKofPj3fjHp_yMQ/edit#slide=id.p9) Release guide
  
- **Tuesday:**
  - [ ] Morning: Brief overview of where things are in Rails (recap focus on MVC, config). - Faraz 
      - Basic application structure
      - Rails doctrine, etc...
  - [ ] Afternoon: Checkout mob-session part 1
  - [ ] Afternoon: Checkout mob-session part 2
  
- **Wednesday:** 
  - [ ] Morning: Checkout mob-session part 3
  - [ ] Afternoon: Rails demo: Active Record (migrations, associations, CRUD functions) - Oliver [slides](https://docs.google.com/presentation/d/11EhVRW4JckFUEBTclTMT8B0-OOga8l7Pim4PlQLKy_M/edit?usp=sharing)
  - [ ] Afternoon: Do a overview of Relational Databases (the concept, SQL, ORM's, etc..) - Faraz [slides](https://docs.google.com/presentation/d/1FuaqKjjdlQKCFZmbwdqS_-TKsRH4zSH4U-zFju8CekA/edit?usp=sharing)

- **Thursday:**
    - [ ] Morning: Checkout mob-session part 4
    - [ ] Afternoon: Talk about the midcourse project - Coaches

- **Friday:**
  - [ ] Morning: Introduce the Weekend Challenge (Comments challenge) - Oliver
  - [ ] Afternoon: Tech interview training - Second part of the RPS Challenge

## Please complete this checklist
 - [ ] Are all slides decks up to date?
   - [ ] Check one by one
 - [ ] Do the slides have talking points added if another coach needs to take over the talk/demo?
 - [ ] Do we have any talks/demos that will take more than 45 minutes to complete?
	 - [ ] Have we scheduled the longer talks/demo so that there are no conflicts with another demo?
 - [ ] Are all the appropriate slides added to the drive, and in the right folder?
 - [ ] Do we have any conflict in the schedule with the talks?
	 - [ ]  meetings
	 - [ ] double booking
	 - [ ] Bank Holidays
   - [ ] Coaches missing (CA labs sprint/vacation)
- [ ] Have all coaches done a dry run of the project?
- [ ] Do we need to update packages/gems/dependencies?
- [ ] Do we have recordings from previous talks available in the drive?
	- [ ] Are the talks named appropriately so that they are easily found? 
	- [ ] Are the recordings in the right folder?
- [ ] When was the last check made for typos etc?
	- [ ] Have you run the text through Grammarly?
- [ ] Are there any outstanding PRs towards the coach guides that need to be reviewed/merged?
- [ ] Is Teachable up to date?
- [ ] When will we enroll the students in the week challenge?
- [ ] Who will enroll the students in the course?
- [ ] Are the slides added to Teachable?
- [ ] **Have we gone through this checklist thoroughly or rushed through it?**
    - [ ] thoroughly
    - [ ] rushed (Please add reason)
