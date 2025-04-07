Web API endpoints  


  
V the only API endpoint that does not require authentication :  
[aliengarden.com/login](http://aliengarden.com/login) (play id token)  



aliengarden.com/api/servers/
    GET -> list serveur (accessible par tout le monde)
    POST -> ajouter un nouveau serveur (accessible par les AUTRES world server)

aliengarden.com/api/leaderboards/
aliengarden.com/api/players/{user}/characters/slots
aliengarden.com/api/players/{user}/vault/storage
aliengarden.com/api/players/{user}/vault/gifts
aliengarden.com/api/players/{user}/nameChange
aliengarden.com/api/players/{user}/purchase-verify

aliengarden.com/api/shop
aliengarden.com/api/market


[aliengarden.com/api/servers](http://aliengarden.com/api/servers)  
[aliengarden.com/api/status](http://aliengarden.com/api/status)  

[aliengarden.com/api/leaderboards](http://aliengarden.com/api/leaderboards)  

[aliengarden.com/api/players/search](http://aliengarden.com/api/players/search)  
[aliengarden.com/api/players/profile](http://aliengarden.com/api/players/profile)  
[aliengarden.com/api/players/pets](http://aliengarden.com/api/players/pets)  
[aliengarden.com/api/players/characters](http://aliengarden.com/api/players/characters)  

[aliengarden.com/api/guilds](http://aliengarden.com/api/guilds)  
  
[aliengarden.com/api/wiki/characters](http://aliengarden.com/api/wiki/characters)  
[aliengarden.com/api/wiki/items](http://aliengarden.com/api/wiki/items)  
[aliengarden.com/api/wiki/enemies/](http://aliengarden.com/api/wiki/enemies/)  
[aliengarden.com/api/wiki/plants](http://aliengarden.com/api/wiki/plants)  
[aliengarden.com/api/wiki/pets](http://aliengarden.com/api/wiki/pets)  
[aliengarden.com/api/wiki/dungeonsZ](http://aliengarden.com/api/wiki/dungeonsZ)  
  
  
[aliengarden.com/api/](http://aliengarden.com/api/)  
[aliengarden.com/api/](http://aliengarden.com/api/)  
  
  
Player profile :  
Picture  
Name  
Rank  
Bio  
  






  
CharactersListRequest  
CharactersCreateRequest  
GiftSendRequest  
GiftReceivedEvent  
  
  
  
  
Add Logging request dto with Google/Apple/PlayId :  
  
Hi, you can just navigate users to play id as the unity client does, and then use http redirect as custom uri scheme to return auth codes to your website back. Please create an issue on GitHub if you have any issues.  
  
Add user claims 'User', 'Admin' roles.  
  
ASP.Net core identity  
  
var roles = await _userManager.GetRolesAsync(user); // e.g. ["User"], or ["User","Admin"]  
var extraClaims = await _userManager.GetClaimsAsync(user); // any custom claims you’ve stored  
  
  
We can then authenticate on the backend, and return a JWT to our user with his claims.  
  
  
  
Guide :  
  
  
Store a short‑lived access token in memory.  
  
Store a long‑lived refresh token in an HttpOnly, Secure cookie.  
  
On page load or when the access token expires, call your /refresh endpoint. The browser sends the refresh cookie automatically, you get a new access token back in memory.  
  
  
  
------  
  
You can include the user's IP address as a custom claim when issuing the token:  
  
csharp  
Copy code  
new Claim("ip", userIpAddress)  
Then, every time the user makes a request with their token:  
  
Extract the JWT.  
  
Parse it and get the "ip" claim.  
  
Compare that to the actual HttpContext.Connection.RemoteIpAddress.----  
  
When does the client know it's time to refresh the token?  
  
Server might throw 401 unauthorized.  
  
1. Decode the token  
2. Check the expiration date ("exp", Unix timestamp format)  
3. Requests the server to refresh the JWT  
  
POST /refresh  
Authorization: Bearer <refresh_token>  
  
  
---  
  
  
Store the encrypted token in PlayerPrefs (using PlayerPrefsUtils)