
# Product Backlog - TV Catalog

## EPIC 1: TV Show Management

### US-01: TV Show Management

**As a** user
**I want to** add, edit, and delete TV shows
**In order to** keep the catalog up to date.

```gherkin
Scenario: Add a TV show
  Given that the user is in the catalog
  When they add a new TV show with all the required data
  Then the TV show is saved correctly

Scenario: Edit a TV show
  Given that a registered TV show exists
  When the user modifies its information
  Then the changes are saved correctly

Scenario: US-01.3 - Delete a TV show
  Given that a registered TV show exists
  When the user deletes it
  Then the TV show disappears from the catalog
```

## EPIC 2: TV Show Search
### US-02: TV Show Search
**As a**  user
**I want to** search for a TV show by its name
**In order to** find it quickly.
```gherkin
Scenario: US-02.1 - Search for a TV show by name
  Given that registered TV shows exist
  When the user types the name of a TV show
  Then the system displays the matching results
```
## Epic 3: Classification by Genre
### US-03: Classification by Genre
**As a** user
**I want to** filter TV shows by genre
**In order to** find content that interests me.

```gherkin
Scenario: US-03.1 - Display available genres
  Given that the user is in the TV show catalog
  When they open the genre filter
  Then the system displays the available genres

Scenario: US-03.2 - Filter TV shows by genre
  Given that TV shows of different genres exist
  When the user selects a genre
  Then the system only displays the TV shows belonging to that genre
```
## EPIC 4: Ratings
### US-04: Ratings
**As a** user
**I want to** rate a TV show from 1 to 5 stars
**In order to** share my opinion.

```gherkin
Scenario: US-04.1 - Register rating
  Given that the user has selected a TV show
  When they assign a rating from 1 to 5 stars
  Then the system saves the rating correctly

Scenario: US-04.2 - Display average rating
  Given that a TV show has registered ratings
  When the system calculates the average
  Then it displays the updated average rating of the TV show
```

## EPIC 5: Favorites
### HU-05: Favorites

**As a** user
**I want to** save my favorite TV shows
**In order to** access them easily..

```gherkin
Scenario: US-05.1 - Add a TV show to favorites
  Given that the user has logged in
  When they select the "Add to favorites" option
  Then the TV show is added to the favorites list

Scenario: US-05.2 - Remove a TV show from favorites
  Given that the TV show is in favorites
  When the user selects "Remove from favorites"
  Then the TV show no longer appears on the list

Scenario: US-05.3 - Display favorites list
  Given that the user has TV shows saved as favorites
  When they access their favorites list
  Then the system displays all their favorite TV shows
```

## EPIC 6: User Registration
### HU-06: User Registration

**As a** new user
**I want to** register with my personal details
**In order to** access the TV show system.

```gherkin
Scenario: US-06.1 - Successful registration
  Given that the user is on the registration screen
  When they enter a valid name, an unregistered email, a password, and confirm it correctly
  Then the system creates the account and displays the message "Successful registration"

Scenario: US-06.2 - Email already registered
  Given that the email already exists in the system
  When the user tries to register with that email
  Then the system displays the message "The email is already registered"

Scenario: US-06.3 - Mismatched passwords
  Given that the user is filling out the registration form
  When the password and the confirmation do not match
  Then the system displays the message "Passwords do not match"
```

## EPIC 7: User Login
### HU-07: User Login

**As a** registered user
**I want to** log in with my email and password
**In order to** access my account.

```gherkin
Scenario: US-07.1 - Successful login
  Given that the user has a registered account
  When they enter a correct email and password
  Then the system grants access to the application

Scenario: US-07.2 - Incorrect password
  Given that the user is registered
  When they enter an incorrect password
  Then the system displays the message "Incorrect email or password"

Scenario: US-07.3 - Empty fields
  Given that the user is on the login screen
  When they attempt to log in without completing all the fields
  Then the system requests that they complete the required information

