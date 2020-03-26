# Week 7 - 8 - 9 News Room
### Introduction to this week

#### Swedish
**Avancerad Rails, API'er och Agila utvecklingsmetoder**

Allt handlar om att plocka på sig erfarenhet och kompetens (som vi definierar kunskap omsatt i praktik). Under tre veckor bygger vi en avancerad marketplace-applikation som en fortsättning på vår News Room utmaning. Vi fördjupar oss i konceptet med API'r som hjälper oss att öppna upp vårt system för andra utvecklare, jobbar med mer avancerade planeringsverktyg, följer de agila arbetsmetoderna och sjösäter en fullvärdig lösning.

#### English
**Advanced Rails, APIs and Agile development methods**

Welcome to the News Room Challenge. These weeks strengthen and deepen your competence and experience with a large project that tests the knowledge you have gained thus far. During these three weeks, you'll build a complex and detailed application. This time, you will add multiple layers of complexity, and work in Rails as News Room becomes a fully featured news and editorial platform with several user types and roles. We will practice Agile workflow, pushing you to work efficiently. At the end of these weeks, you will have a large, complex, and impressive project to add to your portfolio.

- add section about React
- add section about client server

### Teachable Course
[Advanced React and Rails](https://learn.craftacademy.co/admin/courses/682110/information)

## Week Lab
News Room Challenge

## Learning objectives

- Build a system
- Practice project collaboration - planning, organizing ideas and tasks, capturing requirements 
- Onboarding new team members, joining a new team
- Learn more about Agile practices (Scrum + XP - Software Craftsmanship)
- Practice more on CI & CD, ~Devops (set up a VPS with DB, application server - Digital Ocean)~
- Practice Cloud Storage - Active Storage in Rails

- API only Rails App for the entire logic and storage
  - Serialization - OK
  - Testing Serializers - 
- React Client
- No coding - just CONFIGURATION and SETUP (the chores), during the first 3 days of the challenge
- By wednesday night we need the following:
  - Rails API-only app (with test framework - RSpec) - Pings controller + endpoint
  - React app (with test framework - Cypress & Jest/Enzyme) - connect to back-end and display "Pong"
  - CI & CD
  - Both app deployed (Rails on Heroku, React on Netlify) 
- Figure out (and document) OAuth on React


## Weekend challenge

No challenge - just work on the News Room Challenge

### Head Coach: Thomas
### Supporting Coaches: Oliver


## Guide

### Week 7
- **Monday:**
  - [ ] Morning: Introduction to News Room Challenge - Thomas & Oliver give them PT and strict requirements from the client
    - [ ] Oliver sets up new PT board
  - [ ] Morning: Students start the First Sprint(Desing Phase) 
  - [ ] Workshop on story prioritization, voting and Epics - Thomas & Oliver (Tell them about including lo-fi/mock up in PT but also to the PR once they have worked on it)
  - [ ] Start with scrum master meeting every afternoon

- **Tuesday:**
  - [ ] Morning: Product owner intro (Recorded video for students to watch) - Recording (Prepare students for presenting their project plans on wednesday) [Agile Product Ownership in a Nutshell](https://youtu.be/502ILHjX9EE)
  - [ ] Afternoon: Introduction to various ways of building JSON responses in Rails (`render json:`, JBuilder, Serializers) - Thomas (coding demo)
  
- **Wednesday:**
  - [ ] Morning: Teams present their project plans (PT, lo-fi's and Mock Up's) - Shift teams
  - [ ] Authentication in Rails-React-Redux using a package - Oliver (Resource: https://github.com/Eth3rnit3/j-tockauth)
 
- **Thursday:**
  - [ ] Morning: File attachements (Active Storage) - Oliver (RAILS mobsession)
  - [ ] Afternoon: Workshop on [Scrum](http://www.scrumguides.org/) (release quiz on CraftEd 2.0) - Thomas (Oliver will support)
  - [ ] Coach meeting: Discuss what each coach should bring up with their students during the assessment on friday

- **Friday:**
  - [ ] Tech interview (Twitter challenge, maybe do assessment after tech interview is finished)
  - [ ] Assessment of the students (one on one)
  - [ ] WEEKEND CHALLENGE: Inform the students about client meeting on Monday. Show them the [GlocalNews client meeting recording](https://www.youtube.com/watch?v=Vhuc9NVkAEI). The challenge is to prepare for that meeting. 


### Week 8
- **Monday:**
   - [ ] Morning: Instead of morning scrum: Sprint Review for each team - Oliver and Thomas
   - [ ] Afternoon: File attachements using Cloud storage (AWS S3) - Oliver (mobsession Rails + React) 

- **Tuesday:**
   - [ ] Afternoon: Geocoding (Rails and React) - determine what edition the user is served - Thomas 
      - Resource: https://drive.google.com/file/d/1knQRoUF7GvdxrIlpVioIMbiPAlQXcpKK/view?usp=sharing

- **Wednesday:**
  - [ ] THE Shuffle Change teams - Maybe
     - [ ] Teams onboard new members - No coach support
  - [ ] Revisiting Stripe with stripe elements (subscriptions, recurring payments, styling ) - Thomas and Oliver (mobsession - coding)

- **Thursday:**
  - [ ] Afternoon: Internationalization (i18n) in React - Thomas (with Oliver)
https://github.com/CraftAcademyLabs/ca_course/blob/master/week8/18n-react.md

- **Friday:**  
 

### Week 9
Extending News Room with Mobile Client

- **Monday:**
  - [ ] Morning: Sprint Review for each team, entire cohort - Faraz & Oliver 
  - [ ] Morning: Start designing for the mobile client - Faraz
    - [ ] [Slidedeck - Add talking points](https://docs.google.com/presentation/d/1_vKD1ArJN3XKa0rAF0jS3VRN0pWmBdb2Gpvhov_LxaQ/edit#slide=id.g4c8a2ae7e1_0_0)
    - [ ] [Recording](https://drive.google.com/file/d/1m0XKFFzPTiw1aTwMw4yoX7XVg9X728Ww/view?usp=sharing)
  - [ ] Morning: Introduce Ionic/React - Faraz 
    - [Slidedeck - TBA]()
  - [ ] Afternoon: Hello World in Ionic/Reactn - Faraz 
  - [ ] 16:00 Scrum master follow up
  
- **Tuesday:**
  - [ ] 14:00 Q&A sessions, make use of [retrospective app](https://retrospected.com/) to gather ideas from students
  - [ ] 16:00 Scrum master follow up

- **Wednesday:**
  - [ ] 14:00 Q&A sessions, make use of [retrospective app](https://retrospected.com/) to gather ideas from students
  - [ ] 16:00 Scrum master follow up

- **Thursday:**
  - [ ] 14:00 Q&A sessions, make use of [retrospective app](https://retrospected.com/) to gather ideas from students
  - [ ] 16:00 Scrum master follow up

- **Friday:**
  - [ ] 10:00 Pepp talk before Final Project - All coaches
    - [ ]  [Slidedeck - TBA]()
  - [ ] 13:30 Tech interview training - Unter [Setting up a project](../miscellaneous/assessments/assessment_6.md) - Go over Unter
  - [ ] 16:00 Scrum master follow up

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
- [x] Are there any outstanding PRs towards the coach guides that need to be reviewed/merged?
- [ ] Is Teachable up to date?
- [ ] When will we enroll the students in the week challenge?
- [ ] Who will enroll the students in the course?
- [ ] Are the slides added to Teachable?
- [ ] **Have we gone through this checklist thoroughly or rushed through it?**
    - [x] thoroughly
    - [ ] rushed (Please add reason)
