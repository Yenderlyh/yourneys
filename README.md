# Project Name
YOURNEYS

## Description

Yourneys is a platform for travelers to discover cities through customized journeys created by locals.
 
## User Stories

- **404** - As a user I want to see a nice 404 page when I go to a page that doesn’t exist so that I know it was my fault 
- **500** - As a user I want to see a nice error page when the super team screws it up so that I know that is not my fault
- **start-page** - As a user I want to be able to access the homepage so that I see what the app is about and login or signup
- **sign up** - As a user I want to sign up on the webpage so that I can see all the Yourney or create a new Yourney
- **login** - As a user I want to be able to log in on the webpage so that I can get back to my account
- **logout** - As a user I want to be able to log out from the webpage in case other user wants to log in
- **Homepage** - As I user I want to be able to start searching Yourneys for a city right away, see some suggestions for the most visited cities to inspire my next trip, access my profile page and navegate easily among sections (explore, search, add yourney, favorites and go back to home)
- **profile-tab** - As I user I want to be able to edit my personal info, access messages and log out
- **profile** - As I user I want to be able to see my profile details, my upcoming yourneys (and delete them), the ones I've done and the ones I've created
- **explore** - As I user I want to be able to see suggestions to inspire me, like the last added yourneys and the top rated yourneys
- **search** - As I user I want to be able to filter yourneys in a city, with different criteria (date, interest...)
- **create-yourney** - As I user I want to be able to create and edit yourneys for other users (and delete them)
- **favorites** - As I user I want to be able to see yourneys I've marked as favorites

## MVP

- Homepage
- Create profile, edit it
- Create Yourney
- Add Yourney
- Search for Yourneys

## Backlog

User profile:
- upload my profile picture
- see other users profile
- list of upcoming yourneys
- list of yourneys I've done
- list of created yourneys
- checkbox to update from upcoming yourney to done
- messages (view and notifications)

Geo Location:
- add geolocation to yourneys when creating
- show yourneys route in a map in the yourney detail page

Explore
- filter latest/new yourneys
- display top rated yourneys

Search
- add filters for interest...

Create
- upload images
- add routes in map

Favorites
- add yourneys to favorites and identify them with an icon
- remove yourneys from favorites

Messages
- create, send, and receive messages from other users
- receive notifications

Settings
- change password
- change email
- activate/ deactivate notifications

Yourneys details
- user view of added yourney with checkboxes to mark what the user have accomplished


## ROUTES:

- GET /auth/signup
  - redirects to / if user logged in
  - renders the signup form (with flash msg)

- POST /auth/signup
  - redirects to / if user logged in
  - body:
    - email
    - password
  - validation
    - fields not empty
    - user does not exist
  - create user with encrypted password
  - store user in session
  - redirect to /

- GET /auth/login
  - redirects to / if user logged in
  - renders the login form (with flash msg)

- POST /auth/login
  - redirects to / if user logged in
  - body:
    - username or email
    - password
  - validation
    - fields not empty
    - user exists
    - passdword matches
  - store user in session
  - redirect to /

- POST /auth/logout
  - body: (empty)
  - redirect to /auth/login

- GET / 
  - renders the homepage
  - redirects to /auth/login if user logged out

- GET /profile
  - renders the profile details

- GET /profile/edit
  - renders the profile details + create form

- POST /profile/edit
  - renders the profile details + create form
  - body:
    - profile pic
    - username
    - description

- GET /yourney/create
  - renders the create form

- POST /yourney/create
  - redirects to /auth/login if user is anonymous
  - body: 
    - name
    - description
    - location
    - date
    - days
    - tags
  - validation
    - check required fields 
    - if data is valid = create a new yourney and redirect to /yourney/:id
    - if data is invalid = create an error message and redirect to /yourney/create

- GET /yourney/:id
  - redirects to /auth/login if user is anonymous
  - renders the yourney detail page
  - validation
    - id is !valid (next to 404)
    - id !exists (next to 404)
  - renders the event detail page


- GET /yourney/:id/edit
  - redirects to /auth/login if user is anonymous
  - redirects to /yourney/:id if user is not owner
  - renders the yourney detail page + the create form

- POST /yourney/:id/edit
  - redirects to /auth/login if user is anonymous
  - body: 
    - name
    - description
    - location
    - date
    - days
    - tags
  - validation
    - check required fields 
    - if data is valid = create a new yourney and redirect to /yourney/:id
    - if data is invalid = create an error message and redirect to /yourney/:id/edit

- POST /yourney/:id/delete
  - redirects to /auth/login if user is anonymous
  - body: (empty)
  - validation
    - id is !valid (redirects to current page if user access from a yourneys list - or previous page if user access form /yourney/:id)
    - id !exists (redirects to current page if user access from a yourneys list - or previous page if user access form /yourney/:id) || (next to 404) ********
  - deletes the yourney
  - redirects to current page

- POST /yourney/:id/select
  - redirects to /auth/login if user is anonymous
  - body: (empty)
  - redirects to current page
  - validation
    - check if is already selected 
    - if selected = flash message "already in your list"
    - if !selected = add to user's list and flash message "yourney added"


- GET /search
  - redirects to /auth/login if user is anonymous
  - renders the search form

- POST /search
  - redirects to /auth/login if user is anonymous
  - body: 
    - location
    - date
    - days
    - interests
  - redirects to /yourneys/results
  - validation
    - check required fields 
    - if data is valid = redirect to /yourneys and show filtered yourneys
    - if data is invalid = create an error message and redirect to /search


## Models

User model
 
```
user: String // backlog
email: String (required)
password: String (required)

```

Yourney model

```
name: String (required)
description: String (required)
location: String (required)
date: Date
days: Number (required)
tags: String (enum: food, party, adventure, cultural, wandering, sports, shopping, music) (required)

``` 

Search model

```

location: String (required)
date: Date
days: Number
interests: String (enum: food, party, adventure, cultural, wandering, sports, shopping, music)

``` 

## Links

### Trello

[Link to your trello board](https://trello.com) or picture of your physical board

### Git

The url to your repository and to your deployed project

[Repository Link](https://github.com/MJHRhacker/yourneys)

[Deploy Link](http://heroku.com)

### Slides

The url to your presentation slides

[Slides Link](http://slides.com)


## Wireframes
 
![Yourneys wireframes][wireframes]

[wireframes]: https://github.com/MJHRhacker/yourneys/blob/master/YOURNEYS%20wireframes%20Overview.png
