# Apps-Script-GSApp-Library
Google Service Account Library for Apps Script

This is an improved version of my Google service account library for Google Apps Script. This makes use of the new Utilities.computeRsaSha256Signature(value, key).  I've added the ability to batch request tokens for users in your domain. If you need to request a token for your server itself add the client_email as a user.  You can add the library with the project Id: `MJ5317VIFJyKpi9HCkXOfS0MLm9v2IJHf` or add from GSApp.gs found in this repo. 

You can cotact me on google+ at:  
[Spencer Easton](https://plus.google.com/+SpencerEastonCCS)  

#### Using this Library  
##### Create a Service Account
1) Create a new API Project in your developers console, or use one associated with your script.   
2) Select APIs and Auth -> Credentials  
3) Click 'Create New Client Id'  
4) Select Service Account and Generate new JSON key  
5) Click 'Create Client Id'. The JSON key will autodownload.  
6) Click APIs in left menu  
7) Enable any APIs you need this service account to access  

##### Prepare your Service Account Key  
1) Copy the contents of the JSON key and paste it into your scripts properties. Name the property as desired. In the example case I use `jsonKey`.    
2) When you need access, use the following command:  

    var jsonKey = JSON.parse(PropertiesService.getScriptProperties().getProperty("jsonKey"));  
    var privateKey = jsonKey.private_key;
    var serviceAccountEmail = jsonKey.client_email; 


  
##### Authorize the service account for your google domain  
 1) Launch admin.google.com as a domain admin  
 2) Open Security settings  
 3) Choose advanced settings  
 4) Choose Manage API client access  
 5) Add you service account client Id in the 'Client Name' box  
 6) Add the OAuth2 scopes to the APIs you enabled for this service account 'One or More API scopes' box  
   
   
##### Adding the Library  
You can either either use the code from this repo directly in your project or include the library `MJ5317VIFJyKpi9HCkXOfS0MLm9v2IJHf`
  
    
    /*  
    * Constructor for the GSApp Library. Use this to initialize a GSApp object.   
    * @param {String} rsaKey Your private RSA key in PEM64  
    * @param {Array} Scopes An Array of scopes you want to authenticate    
    * @param {String} saEmail The service account Email  
    * @return {object} self for chaining  
    */  
    function init(string RSAKey, array Scopes, string ServiceAccountEmail)   
    
      
    /*  
    * Adds a user to GSApp.  
    * @param {String} userEmail The Email account of the user for whom you are requesting the token  
    * @return {object} self for chaining  
    *\  
    function addUser(string userEmail)   
    
    /*  
    * Adds an array of users to GSApp.  
    * @param {[string]} userEmails Array of emails to be added.  
    * @return {object} self for chaining  
    *\  
    function addUsers([userEmails])
    
    /*  
    * Removes a user from GSApp.    
    * @param {String} userEmail The Email account of the user for whom you are requesting the token  
    * @return {object} self for chaining  
    *\  
    function removeUser(string userEmail)   
    
    /*  
    * Removes all users from  GSApp
    * @return {object} self for chaining  
    *\  
    function removeUsers()   
    
    /*  
    * Requests an Oauth token for each user added.
    * @return {object} self for chaining  
    *\  
    function requestToken()   
      
    /*  
    * Gets the Oauth token for the specified user. You must call requestToken() before this function.  
    * @param {String} userEmail The email account of the user you want  
    * @return {object} {token,expire}  
    *\  
    function getToken(string userEmail)  
      
    /*  
    * Gets all the tokens generated by requestToken(). You must call requestToken() before this function.  
    * @return {object} {user:{token,expire} , user:{token:expire} , ... }   
    *\  
    function getTokens()  
  
  
