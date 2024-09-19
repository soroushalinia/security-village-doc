# Authentication Protocol

This CMS use JWT Bearer Authentication.
During each login two tokens are generated, refresh and access token.
Access tokens are expired every 10 minutes and new access token can be
obtained using refresh token. 

There is also logout functionality which blacklist refresh token, requiring
new login to obtain a new token pair.