## Week 4 Advanced React and Rails API
### Introduction to this week

#### Swedish
Den här veckan introducerar vi Ruby on Rails och det är första gången som studenterna ska bygga sin egen API. 
Även denna veckan är delad i två utmaningar där den första utmaningen är en individuell utmaning där studenterna ska bygga Crafty News, en API som hanterar alla CRUD actions för artiklar. Den här utmaningen kommer även ligga som grund för helgutmaningen. 
Den andra utmaningen är en grupp utmaning och bygger på legacy kod. Utmaningen är att testa den existerande kodbasen samt utveckla eventuella funktioner på ett bättre sätt. Vi introducerar Pivotal Tracker och studenterna förväntas skriva user stories för de funktioner i applikationen som de ska testa. 
Vi börjar jobba på ett mer agilt sätt där vi kopplar sambandet mellan user story och funktionalitet. Det är även studenternas första grupputmaning och det ställer nya krav på version control kunskaperna, att ha ett fungerande flow i en större grupp och inte bara ett par.  

#### English
This week we are introducing Ruby on Rails and the students will build their own API for the first time. 
This week is also splitted into two challenges where the first one is an individual challenge. In the first challenge the students will build Crafty News, an API that handles all CRUD actions for articles. The weekend challenge will also be based on this first challenge. 
The second challenge is a group assignment that is about legacy code. The challenge is to test the existing code base and potentionally develop and refactor the existing features. We introduce Pivotal Tracker and the students are expected to write user stories for the features that they will test. 
Vi start to work in a more Agile way where we connect the user story to a feature. This is the students first group assignment and that also requires practise of version controll and keeping a good flow in a bigger group than just a pair. 


### Teachable Course
[Building API's in Ruby on Rails](https://learn.craftacademy.co/admin/courses/771096/information)

### Week lab
The students are introduced to Ruby on Rails this week. We are exposing them to the 'magic' of Rails AND how to build and maintain an API.

The Legacy Code Challenge aims at allowing students to write both acceptance tests and unit tests for a ready made api.
1. AUT cycle as intro to Rails (individual assigment)
2. Legacy code challenge (pairing assignment)

### Learning objectives
* How to build API only Rails applications
* How to test API endpoints using request specs
* Test React SPA


### Weekend Challenge
* Adding devise token auth to the rails intro api and restrict the edit and create action to only authenticated users. 

### Head Coach: Emma 
### Assistant coaches: Thomas
Let's be strict with the support protocol AND who is giving support. Communicate who is in charge in morning scrum AND on Slack. We need to make sure the understand the importance of component testing with jest/enzyme!

### Guide
- **Monday:** 
  - [ ] Morning: Pair up students
  
  - [ ] Morning: Introduce Rails & AUT Part 1 - Emma 
    - [ ] [Slides to introduce Rails](https://docs.google.com/presentation/d/1UwauQbrLjKBh24UH622aWi5q5F0OB3HTSQRGRmt8Fj4/edit#slide=id.g4b12024eb7_0_21)
    - [ ] [Code Guide](https://github.com/CraftAcademyLabs/coach-guides/blob/master/coding_demo_guides/aut-rails.md)
    - [ ] This is the begining of the **Crafty News** project for this cohort
    
  - [ ] Afternoon: Introduce Rails & AUT Part 2 - Emma
    - [ ] Intro to Articles challenge, FactoryBot, Fixtures
    
  - [ ] Afternoon: Introduction to web architecture (MVC) - Thomas 
    - [ ] [Slides](https://docs.google.com/presentation/d/14Z4aPjdDTgeuQdup2MoiZrmUSSDce7R3I5dcotg7uyc/edit?usp=sharing)
    
- **Tuesday:**  
 
  - [ ] Morning: Deploy to Heroku, Setting up Semaphore and Coveralls for Crafty News - Emma 
    - [ ] [Slides](https://docs.google.com/presentation/d/1JX1To6mtAqn0qMhVQiE88BHATevYcOdr2QST5pq88zo/edit#slide=id.g5c96494016_0_350)
    - [ ] Set up Heroku, Coveralls and Semaphore for the project
    
  - [ ] Afternoon: Introduce the Legacy Code Challenge - Emma 
    - [ ] [Slides](https://docs.google.com/presentation/d/1S2Nn_hOhm_slruGTPFVoRGBh9G-NiKExENRHhUd-8As/edit#slide=id.g56b04e896f_0_0)
  
  - [ ] Afternoon: RESTFUL API’s part 2 - Thomas
    - [ ] [Slides](https://docs.google.com/presentation/d/1j4SkChg57gX2SB2wklTmA7-B0wbxxstOfEOk6JmZwdg/edit#slide=id.g35ed75ccf_022)


- **Wednesday:**  

  - [ ] Morning: Validations in Rails and instance methods - Emma 
    - [ ] [Slides](https://docs.google.com/presentation/d/1uZJTsWZE43_ANHEcpqWbH15rd8w2BidR1Ap305q8VXE/edit?usp=sharing)

  - [ ] Afternoon: Rails demo: Active Record Basics - Emma 
    - [ ] [Slides](https://docs.google.com/presentation/d/11EhVRW4JckFUEBTclTMT8B0-OOga8l7Pim4PlQLKy_M/edit?usp=sharing)    
    
- **Thursday:**  

  - [ ] Morning: Rails demo: routing (plus resources) - Emma
    - [ ] [Slides](https://docs.google.com/presentation/d/1R-aZYu6C8Y1kdsJy_iXUorDL7mTstjKVk9VFYmWJC3Q/edit#slide=id.g4b12024eb7_0_21) 
    
  - [ ] Afternoon 14:00 : The simple truths - Thomas 
    - [ ] [Slides](https://docs.google.com/presentation/d/1kvzG_b3zoQ6grCMuPiT59_wMikSWd1qgarVK8qUuSFc/edit#slide=id.g497fb264d8_0_0)

- **Friday:**
  - [ ] Morning: Intro to token authorization & the weekend challenge - Emma 
    - [ ] Go over baics with res resp
    - [ ] "You authenticate with the API with every request"
    - [ ] [Slides, needs to be updated](https://docs.google.com/presentation/d/1loqHoN9zTkCXisi5PQjfNxL9oCl7_hJpOPLAgH0hCFE/edit#slide=id.p6)

  - [ ] Retro - All coaches

  
## Please complete this checklist
 - [ ] Are all slides decks up to date?
   - [ ] Check one by one
 - [ ] Do the slides have talking points added if another coach needs to take over the talk/demo?
 - [ ] Do we have any talks/demos that will take more than 45 minutes to complete?
	 - [ ] Have we scheduled the longer talks/demo so that there are no conflicts with another demo?
 - [ ] Are all the appropriate slides added to the drive, and in the right folder?
 - [ ] Do we have any conflict in the schedule with the talks?
	 - [ ] meetings
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
