- GET /profile/edit
  - renders the profile details + create form

- POST /profile/edit
  - renders the profile details + create form
  - body:
    - profile pic
    - username
    - description

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