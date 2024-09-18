# FloorPlanMapperAPI
Import API for Floor Plan Mapper

Authentication
We use REST API for communication between the client and server, and HTTP Basic authentication based on tokens.

To authenticate your client, follow these three steps:

(Optional) Create a new user for your script on the page https://your-workspace-name-here.fpm.cloud/users.

Receive the auth token. To obtain a valid auth token, send a POST request to the URL https://your-workspace-name-here.fpm.local/api/v1/auth/login with the following JSON string payload in the request body: {"email": "username@example.com", "password": "user password"}

If you provide correct credentials, you will receive a response containing user information in JSON format. Here is the response schema:

{
  "user": {
    "id": 0,
    "name": "user name",
    "token": "auth_token",
    "token_expire_at": "2023-08-30 10:01:08+00",
    "email": "user@example.com",
    "refresh_token": "refresh token",
    "status": 10,
    "domain": "argel",
    "booking_enabled": true,
    "received_at": "2023-07-31 12:35:14.555614+00",
    "permissions": {
        // user permissions dict
    },
    "role": "current user role"
  }
}
Request example for PowerShell:

$session = New-Object Microsoft.PowerShell.Commands.WebRequestSession
Invoke-WebRequest -UseBasicParsing -Uri "https://your-workspace-name-here.fpm.cloud/api/v1/auth/login?_t=1690798064573" `
-Method "POST" `
-WebSession $session `
-Headers @{
"authority"="your-workspace-name-here.fpm.local"
  "method"="POST"
  "path"="/api/v1/auth/login"
  "scheme"="https"
  "accept"="application/json, text/plain, */*"
  "accept-encoding"="gzip, deflate, br"
  "cache-control"="no-cache"
  "origin"="https://your-workspace-name-here.fpm.cloud"
  "pragma"="no-cache"
} `
-ContentType "application/json;charset=UTF-8" `
-Body "{`"email`":`"YOUR_EMAIL_HERE",`"password`":`"YOUR_PASSWORD_HERE`"}"
Request example for Bash (cURL):

curl 'https://your-workspace-name-here.fpm.cloud/api/v1/auth/login' \
  -H 'authority: your-workspace-name-here.fpm.cloud' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json;charset=UTF-8' \
  -H 'origin: https://your-workspace-name-here.fpm.cloud' \
  -H 'pragma: no-cache' \
  --data-raw '{"email":"YOUR_EMAIL_HERE","password":"YOUR_PASSWORD_HERE"}' \
  --compressed \
  --insecure
To make valid request you should add Authorization HTTP-header to your request. Expected format is Authorization: Basic user_token where user_token is string concatenated from two parts token from step 2 and : encoded by base64. Javascript example how to get valid header value: Basic ${btoa(user.token + ':')}

[Floor Plan Mapper](https://floorplanmapper.com)
