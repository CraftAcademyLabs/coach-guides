# Week 8 - 9 News Room
### Introduction to this week

#### Swedish
**Avancerad Rails, API'er och Agila utvecklingsmetoder**

Allt handlar om att plocka på sig erfarenhet och kompetens (som vi definierar kunskap omsatt i praktik). Under tre veckor bygger vi en avancerad marketplace-applikation som en fortsättning på vår News Room utmaning. Vi fördjupar oss i konceptet med API'r som hjälper oss att öppna upp vårt system för andra utvecklare, jobbar med mer avancerade planeringsverktyg, följer de agila arbetsmetoderna och sjösäter en fullvärdig lösning.

#### English
**Advanced Rails, APIs and Agile development methods**

Welcome to the News Room Challenge. These weeks strengthen and deepen your competence and experience with a large project that tests the knowledge you have gained thus far. During these three weeks, you'll build a complex and detailed application. This time, you will add multiple layers of complexity, and work in Rails as News Room becomes a fully featured news and editorial platform with several user types and roles. We will practice Agile workflow, pushing you to work efficiently. At the end of these weeks, you will have a large, complex, and impressive project to add to your portfolio.

## Week Lab
News Room Challenge

## Learning objectives

- Build a system
- Practice project collaboration - planning, organizing ideas and tasks, capturing requirements 
- Onboarding new team members, joining a new team
- Learn more about Agile practices (Scrum + XP - Software Craftsmanship)
- Practice more on CI & CD, Devops (set up a VPS with DB, application server - Digital Ocean)
- Practice Cloud Storage - Active Storage in Rails
(- Alternatives to Rails & Active Record - Sails (Node based framework) & Waterline - Thomas and Oliver will discuss this

- API only Rails App for the entire logic and storage
  - Serialization - OK
  - Testing Serializers - 
- ReactJs Client
- No coding - just CONFIGURATION and SETUP (the chores), during the firs 3 days of the challenge
- By wednesday night we need the following:
  - Rails API-only app (with test framework - RSpec) - Pings controller + endpoint
  - ReactJS app (with test framework - Cypress & Jest/Enzyme) - connect to back-end and display "Pong"
  - CI & CD
  - Both app deployed (Rails on Heroku, React on Netlify) 
- Figure out (and document) OAuth on React


## Weekend challenge

No challenge - just work on the News Room Challenge

### Head Coach: Thomas
### Supporting Coaches: Faraz and Magnus


## Guide

### Week 8
- **Monday:**
  - [ ] Morning: Introduction to News Room Challenge - Faraz & Oliver give them PT but sell that idea
    - [ ] Oliver sets up new PT board
  - [ ] Morning: Students start the Design Sprint - Recap of the Design Sprint and intro to Epics (introduce prioritization and voting, tasks = AC) - Faraz (Tell them about including lo-fi/mock up in PT but also to the PR once they have worked on it)

- **Tuesday:**
  - [ ] Morning: Product owner intro (Recorded video for students to watch) - Recording (Have them watch it during staff meeting?)
  - [ ] Afternoon: Agile Methodologies Intro - Thomas (Agile Mindset slides) **Crafting an MVP slides on drive/Agile**
  - [ ] Afternoon: Workshop on story prioritization and voting - Faraz & Oliver


- **Wednesday:**
  ~~- [ ] Morning: Multiple OAuth providers - Oliver - Code review demo~~
  
  - [ ] Afternoon: Teams present their project plans (PT, lo-fi's and Mock Up's) - Shift teams (Ultra and Faraz)
  
- **Thursday:**
   - [ ] Authentication in Rails-React-Redux using a package (pick Greg's brain and then Thomas) - Oliver
   - [ ] Afternoon: Workshop on [Scrum](http://www.scrumguides.org/) (release quiz on CraftEd) - Thomas (Oliver will support)


- **Friday:**
  - [ ] Student retro

### Week 9
- **Monday:**
  ~~- [ ] Morning: Intro to Scrum & XP - Thomas (slides demo)~~ **This cohort already had this talk**
   - [ ] Morning: instead of morning scrum: Sprint Review - Facilitated by Faraz + All Coaches (Ship some code, Simulation (Faraz CEO and Thomas CTO)
   - [ ] Morning: File attachements (Active Storage) - Oliver (mobsession - coding(Students need to code with coach))
   - [ ] Afternoon: File attachements using Cloud storage (AWS S3, Use Encrypted Credentials Rails 5.2) - Oliver (mobsession - coding(Students need to code with coach))


- **Tuesday:**
 
   - [ ] Morning: Geocoding (Rails and React) - determine what edition the user is served - Thomas Resource: [https://youtu.be/DJ7SCFwMPho](https://youtu.be/DJ7SCFwMPho)
 ~~- - [ ] Afternoon: Introduce local based events (crimes from Brottsplatskartan API?) (mobsession - coding) - Thomas & Faraz~~-
  - [ ] Afternoon: Introduction to various ways of building JSON responses in Rails (`render json:`, JBuilder, Serializers, Presenters?) - Thomas & Oliver & Faraz & ultra?? (slides + coding demo) Thomas will look into this. 
  [resource for serializer testing](https://github.com/CraftAcademy/we_meet/tree/development/spec/serializers)
  - [ ] Dry Run Advanced Stripe All coaches 

- **Wednesday:**
  - [ ] Revisiting Stripe with stripe elements (subscriptions, recurring payments, styling ) - Thomas and Faraz (mobsession - coding)  10am
 ~~- - [ ] Morning: The Shuffle! Hide in Edx - Faraz
  - [ ] Teams onboard new members - No coach support~~

~~- **Thursday:**~~
  - [ ] Afternoon: Internationalization (i18n) - Faraz [Part 1](https://youtu.be/eBwjN5drg-Q) | [Part 2]     (https://youtu.be/0Nen6z0cIbo) https://medium.freecodecamp.org/setting-up-internationalization-in-react-from-start-to-finish-6cb94a7af725

- **Friday:**
  - [ ] Morning: Software Craftsmanship talk - Thomas? (slides demo) **Slides available on drive/ Agile**
  https://docs.google.com/presentation/d/1lo8EFDeQr6kCayHWYtAsPYhm3ONkjRirJW2_U504wrY/edit port slide deck to new style. 
  - [ ] Tech interview training - Unter [Setting up a project](../miscellaneous/assessments/assessment_6.md) - Go over Unter 
  - [ ] (Start a designsprint for the mobile client (Objectives: Showing all articles, showing articles in categories, Show specific articles, authentication, payment flow) - Oliver )
  - [ ] (Weekend assignment - Download Android Studio (Linux) and XCode (OsX))

### Week 10

Remember juniors are starting this week

Extending News Room with API and Mobile Client

- **Monday:**
  - [ ] Morning: Getting React Native up and Running on Linux and Mac - Group session with students based on OS version.
  - [ ] Morning: Instead of morning scrum: Sprint Review for each team - Thomas & Magnus (The teams need to call this meeting)
  - [ ] React Native (Create slidedeck)- Magnus - Thomas creates a first version. 
    
- **Tuesday:**
  - [ ] Morning: In depth Active Model Serializers usage - Thomas (slides + coding demo)
  - [ ] Afternoon: DevOps with Magnus - Part 1 (Set-up droplet, add db, add Passenger, etc rbenv)
  
- **Wednesday:**
   - [ ] Morning Demo: Part 1 Setup Devise Token auth on an existing Rails app with Devise already present - Oliver (slides + coding demo)
   - [ ] Afternoon: DevOps with Magnus - Part 2 Ansible for deployment
  
- **Thursday:**
  - [ ] Morning: Part 2 User Authentication using tokens - API only - ( new app with RSpec )   - Oliver 
  - [ ] Afternoon: OAuth Demo on mobile (FB) - Oliver (mobsession - coding on backend - use the api only code you created on Wednesday and grab an Ionic app we have and implement OAuth)????????

- **Friday:**
- [ ] Present Newsroom challenge to audience (Dry run for final project/ book big room & test recording equipment. )
  - [ ] Pepp talk before Final Project - All coaches
  - [ ] Retro - All coaches

