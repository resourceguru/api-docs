## Authenticating with Resource Guru

Getting access to a user's Resource Guru account requires going through a step of
authentication. We offer OAuth2 as the standard way to authenticate with our API
as this offers a simple flow for users to allow app access without you having to store
their credentials.

### Considerations when Single Sign On is required

If your account is configured to require SSO for logins, API access through OAuth2
is only available when authenticating as the account owner. This restriction ensures
that users who have been removed from your SSO provider aren't able to carry on using
Resource Guru with unexpired API keys.

### Getting started

We recommend using an OAuth2 library for the platform you're working with, rather than
working from scratch. A fairly comprehensive list of libraries can be found [here](http://oauth.net/2/).

**1** - Register an app at [developers.resourceguruapp.com](https://developers.resourceguruapp.com).
Your app will be assigned a `client_id` and `client_secret` that will be used to identify your app
when users authenticate with the API. You'll need to provide a `redirect_uri` where we'll send the
verification code for authentication. Just use a fake URL like `http://localhost/oauth` if you haven't
got one yet. Any Redirect URI given must be secure (HTTPS) unless it redirects to localhost.

**2** - Configure your OAuth2 library to use the `client_id`, `client_secret` and `redirect_uri` for your app.
You'll need to configure these URLs as well:

- `https://api.resourceguruapp.com/oauth/authorize` to request authorization (must be requested with an HTTP GET request).
- `https://api.resourceguruapp.com/oauth/token` to retrieve tokens (must be requested with an HTTP POST request).


**3** - Authenticate with the API. We'll provide code samples using the [intridea/oauth2](https://github.com/intridea/oauth2) library in Ruby.

#### Quick start using user's login credentials

This method is only recommended for private apps, such as data imports and exports or internal business reporting.
It's useful to get started quickly without all of the overhead of OAuth2 though, which makes it great for exploration.
This should not be used for integrating 3rd party apps with Resource Guru as it requires knowing the user's private credentials.

We support the OAuth2 `password` grant type. To authenticate, make an HTTP `POST` to `/oauth/token` with the following:

``` json
{
  "grant_type"    : "password",
  "username"      : "user@example.com",
  "password"      : "secret",
  "client_id"     : "the_client_id",
  "client_secret" : "the_client_secret"
}
```

You'll receive the access token back in the response:

``` json
{
  "access_token": "the_oauth_access_token",
  "refresh_token": "the_oauth_refresh_token",
  "token_type": "bearer",
  "expires_in": 604800
}
```

To use this with the OAuth2 Ruby library is easy:
``` ruby
client = OAuth2::Client.new(client_id, client_secret, site: "https://api.resourceguruapp.com")
token = client.password.get_token("user@example.com", "secret")
token.get("/v1/example-corp/resources")
```

#### Recommended authentication method using an authorization code

The password grant method shown above is great for getting started quickly, but is impractical for apps that require
users to authenticate with Resource Guru as you would have to store the user's Resource Guru login credentials.

We support the standard auth code flow as well. Here is a code sample in Ruby of how to authenticate this way.

``` ruby
require 'oauth2'

client_id = ENV["CLIENT_ID"]
client_secret = ENV["CLIENT_SECRET"]
redirect_uri = ENV["REDIRECT_URI"]

client = OAuth2::Client.new(client_id, client_secret, site: 'https://api.resourceguruapp.com')

puts client.auth_code.authorize_url(redirect_uri: redirect_uri)
```

Go to the URL provided to authorize with the API. This is the URL you'll direct users to to allow
your app to access the API. When you've authorized with the API, the browser will be redirected to the
`redirect_uri` you provided and the authorization code will be sent as a parameter in the URL. For example
if your `redirect_uri` was `https://localhost/oauth/callback`, the user will be redirected to
`https://localhost/oauth/callback?code=<the code>`

Use this code to retrieve an access token and refresh token:

``` ruby
code = "code sent to the redirect_uri in the previous step"
access_token = client.auth_code.get_token(code, redirect_uri: redirect_uri)
access_token.get("/v1/example-corp/resources")
```

Save the values returned as `access_token.token`, `access_token.refresh_token` and `access_token.expires_at` for later usage.

To connect to the API with a known token:

``` ruby
client_id = ENV["CLIENT_ID"]
client_secret = ENV["CLIENT_SECRET"]
redirect_uri = ENV["REDIRECT_URI"]
oauth_token = ENV["OAUTH_TOKEN"]
refresh_token = ENV["REFRESH_TOKEN"]
expires_at = ENV["EXPIRY"]

client = OAuth2::Client.new(client_id, client_secret, site: 'https://api.resourceguruapp.com')
access_token = OAuth2::AccessToken.new(client, oauth_token, refresh_token: refresh_token, expires_at: expires_at)
access_token.get("/v1/example-corp/resources")
```

In the above example using the token expiry time stamp is optional, but the OAuth2 library will automatically handle
refreshing tokens if it is provided.

**4** - Tokens expire after 7 days and need to be refreshed. When authenticating, a refresh token and expiration
timestamp is provided. Use the refresh token to retrieve a new access token. Most OAuth2 client libraries will handle this automatically.

``` ruby
client_id = ENV["CLIENT_ID"]
client_secret = ENV["CLIENT_SECRET"]
redirect_uri = ENV["REDIRECT_URI"]
oauth_token = ENV["OAUTH_TOKEN"]
refresh_token = ENV["REFRESH_TOKEN"]
expires_at = ENV["EXPIRY"]

client = OAuth2::Client.new(client_id, client_secret, site: 'https://api.resourceguruapp.com')
access_token = OAuth2::AccessToken.new(client, oauth_token, refresh_token: refresh_token, expires_at: expires_at)
new_access_token = access_token.refresh
new_access_token.get("/v1/example-corp/bookings")
```

The old access token will be expired immediately and the new access token will have to be used from that point on. Make sure you
save the new access token, refresh token and expiration timestamps when doing this.

##### More Examples:

###### Python 3:

``` python
from urllib.parse import urlencode
import json
import requests

client_id     = 'APPLICATION_CLIENT_ID'
client_secret = 'APPLICATION_SECRET'
redirect_uri  = 'REDIRECT_URI'
authorize_url = "https://api.resourceguruapp.com/oauth/authorize?client_id=%(client_id)s&redirect_uri=%(redirect_uri)s&response_type=code" % locals()

# Visit the Auth URL -> authorize_url defined above
# Get code token after authorizing
returned_code = input("Enter the code from the authorization step: ")

parameters = {
  'client_id': client_id,
  'client_secret': client_secret,
  'code': returned_code,
  'grant_type': "authorization_code",
  'redirect_uri': redirect_uri
}

token_url = 'https://api.resourceguruapp.com/oauth/token'
token     = requests.post(token_url, urlencode(parameters)).json()
headers   = { "Authorization": "Bearer " + token['access_token'] }

resources = requests.get("https://api.resourceguruapp.com/v1/example-account-subdomain/resources", headers=headers).json()

# Now let's play in an interactive console
import code;code.interact(local=dict(globals(),**locals()))
```

###### Bash

``` bash
#!/bin/bash

client_id='APPLICATION_CLIENT_ID'
client_secret='APPLICATION_SECRET'
redirect_uri='REDIRECT_URI'
authorize_url="https://api.resourceguruapp.com/oauth/authorize?client_id=$client_id&redirect_uri=$redirect_uri&response_type=code"
token_url='https://api.resourceguruapp.com/oauth/token'

echo "Please follow the given link: $authorize_url"
echo "Please provide the given code, followed by [ENTER]:"

read code

token_data=`curl --data "grant_type=authorization_code" --data-urlencode "client_id=$client_id" --data-urlencode "client_secret=$client_secret" --data-urlencode "code=$code" --data-urlencode "redirect_uri=$redirect_uri" $token_url`
token=`echo $token_data | jsawk 'return this.access_token'`

resources_url="https://api.resourceguruapp.com/v1/example-account-subdomain/resources"

echo `curl -H "Authorization: Bearer $token" $resources_url`
```

###### Ruby

``` ruby
require "oauth2"

client_id = "APPLICATION_CLIENT_ID"
client_secret = "APPLICATION_SECRET"
redirect_uri = "REDIRECT_URI"

client = OAuth2::Client.new(client_id, client_secret, { site: { url: 'https://api.resourceguruapp.com'}})
authorize_url = client.auth_code.authorize_url(redirect_uri: redirect_uri)

# Visit the Auth URL -> authorize_url defined above to get the code
puts "Enter the code from the authorization step"
code = gets.strip

access_token = client.auth_code.get_token(code, redirect_uri: redirect_uri)

access_token.get("/v1/example-account-subdomain/resources")

# Now let's play in an interactive console
require "IRB"
IRB.start
```

