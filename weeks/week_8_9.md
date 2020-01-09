# Week 8 - 9 News Room
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

### Week 8
- **Monday:**
  - [ ] Morning: Introduction to News Room Challenge - Thomas & Oliver give them PT and strict requirements from the client
    - [ ] Oliver sets up new PT board
  - [ ] Morning: Students start the First Sprint(Desing Phase) - Recap of the the First Sprint(Desing Phase) and intro to Epics (introduce prioritization and voting, tasks = AC) - Thomas (Tell them about including lo-fi/mock up in PT but also to the PR once they have worked on it)

- **Tuesday:**
  - [ ] Morning: Product owner intro (Recorded video for students to watch) - Recording (Have them watch it during staff meeting?)
  - [ ] Afternoon: Workshop on story prioritization and voting - Thomas & Oliver

- **Wednesday:**
  - [ ] Morning: Teams present their project plans (PT, lo-fi's and Mock Up's) - Shift teams
  - [ ] Afternoon: Introduction to various ways of building JSON responses in Rails (`render json:`, JBuilder, Serializers) - Thomas (coding demo) - partially done in restful api demo in week 7
  - [ ] Authentication in Rails-React-Redux using a package - Oliver
 
- **Thursday:**
  - [ ] Morning: Authentication in React using a package (Resource: https://github.com/Eth3rnit3/j-tockauth) - Oliver
  [resource for serializer testing](https://github.com/CraftAcademy/we_meet/tree/development/spec/serializers)
 - [ ] Afternoon: Workshop on [Scrum](http://www.scrumguides.org/) (release quiz on CraftEd 2.0) - Thomas (Oliver will support)

- **Friday:**
  - [ ] Morning: File attachements (Active Storage) - Oliver (RAILS mobsession - coding (Students need to code with coach))
  - [ ] Assessment of the students (one on one)
  - [ ] Student retro


### Week 9
- **Monday:**
  - [ ] Morning: Instead of morning scrum: Sprint Review - Facilitated by Faraz + All Coaches (Ship some code, Simulation (Faraz CEO and Thomas CTO)
   - [ ] Afternoon: File attachements using Cloud storage (AWS S3, Use Encrypted Credentials Rails 5.2) - Oliver (mobsession - coding Rails + React (Students need to code with coach)) 
   - [ ] Afternoon: Intro to Scrum & XP - Thomas (slides demo)

- **Tuesday:**
   - [ ] THE Shuffle Change teams
   
   - [ ] Teams onboard new members - No coach support
   - [ ] Afternoon: Geocoding (Rails and React) - determine what edition the user is served - Thomas 
      - Resource: https://drive.google.com/file/d/1knQRoUF7GvdxrIlpVioIMbiPAlQXcpKK/view?usp=sharing

- **Wednesday:**
  - [ ] Dry Run Advanced Stripe All coaches 
  - [ ] Revisiting Stripe with stripe elements (subscriptions, recurring payments, styling ) - Thomas, Faraz and Oliver (mobsession - coding)  10am

- **Thursday:**
  - [ ] Afternoon: Internationalization (i18n) in React - Faraz

- **Friday:** 
  - [ ] Tech interview training - Unter [Setting up a project](../miscellaneous/assessments/assessment_6.md) - Go over Unter 
  - [ ] Start a designsprint for the mobile client (Objectives: Showing all articles, showing articles in categories, Show specific articles, authentication, payment flow) - Oliver 
  - [ ] Weekend Challenge - Download Android Studio (Linux) and XCode (OsX))

### Week 10
Extending News Room with Mobile Client

- **Monday:**
  - [ ] Morning: Instead of morning scrum: Sprint Review for each team - Thomas & Faraz 
        - (The teams need to call this meeting)
  - [ ] React Native (Create slidedeck) - Faraz 
    
- **Tuesday:**
~~- [ ] Afternoon: DevOps with Oliver - Part 1 (Set-up droplet, add db, add Passenger, etc rbenv) or Amazon??~~
  
- **Wednesday:**
  ~~- [ ] Afternoon: DevOps with Oliver - Part 2 ( Ansible for deployment ) Amazon??~~
  
- **Thursday:**
  - [ ] Afternoon: OAuth Demo on Client (FB) - Oliver

- **Friday:**
  - [ ] Pepp talk before Final Project - All coaches
  - [ ] Retro - All coaches

