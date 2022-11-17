# TS_client

### To run it:

In source directory:

  `cd TS_client`

  `npm install`
  
  `npm run dev`


## Composition

The main components of this project are:

### src/App.vue

Contains the components of the application.

### src/components/DisplayTable.vue

  - Shows the current content of the user database inside a table
  - Delete a row
  - Edit a username with the name specified in the text box above the 'table'.

### src/components/RegistrationPost.vue

Fields to create/register or log into an account.

#

- When a user logs in the TOKEN is stored in the localStorage.
- None of this components enforce any restriction on data sent or read (this includes empty fields).
- They don't use the error responses to notify the user that something went wrong or what it was.
- The POST methods to "register" and "login" don't update the view of the table on their own (unlike the GET, DELETE or PUT methods) and refresh of the page is required (not implemented a 'force refresh' of the page because it's not the way to go).
