
How to handle the login?  
  
1. Click Login on the website  
2. This opens Unity AGX (deep link)  
3. Click on authorize agx, which will then open a page in the browser  
  
localhost:5432/confirm-login/TOKEN  
  
You are now logged in! Redirecting you...  
localhost:5432/players/Aldé  
  
This will store the Token and Access token  
  
Note that we would need to have a custom deep linking. Also note that this requires the user to have the game running. On windows it's very complex.  
  
  
How to actually easily handle the login?  
  
Try to catch the request sent to PlayId and compare it to one send by the http client.  
  
Implement the authentication logic from the website.  
  
We must obtain the IdToken (access) from PlayId, then validate it (see JWT.cs, to be renamed PlayIdTokenValidator), then get or create a user, assign tokens, and save them in the client..  
  
  
  
  
---  
  
var cookieOptions = new CookieOptions  
{  
HttpOnly = true,  
Secure = true,  
SameSite = SameSiteMode.Strict,  
Expires = DateTime.UtcNow.AddDays(7)  
};  
  
Response.Cookies.Append("refreshToken", refreshToken, cookieOptions);  
  
---  
  
  
Tokens don't need to be stored in the browser.  
  
After login :  
HttpContext.Session.SetString("AccessToken", accessToken);  
  
Then you can later retrieve it :  
var token = HttpContext.Session.GetString("AccessToken");  
  
  
  
--  
  
Why Keep Your Website and API as Separate Projects?  
1. Separation of Concerns  
Your API handles data, logic, and authentication.  
  
Your frontend (Blazor, React, Vue, etc.) handles UI/UX.  
  
But with Blazor Server side rendering, the server is the website is the API.  
  
---  
  
Follow tutorial by God guy on YouTuve for TailwindCSS and Blazor.  
  
- Better login screen / logout / user profile  
- Add rate limiter to API controllers  
- look into SignalR  
-  
  
  
  
  
  
  
Is server side rendering a good thing?  
  
Yes.