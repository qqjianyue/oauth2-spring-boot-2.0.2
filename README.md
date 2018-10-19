OAuth2 Server demo back by Spring Boot2, Spring Security and H2 DB

https://medium.com/@akourtim.ahmed/oauth-2-centralized-authorization-with-spring-boot-2-0-2-and-spring-security-5-and-jdbc-token-store-8dbc063bd5d4

Not high performance production level ready, but a very good starter to learn and start production level customization


Start authorization_server and test different grant types by browser and curl command
If web page logon need, please logon with account(oauth_admin) and password(user)

1. authorization_code flow
Browser GET request to get a authorization_code:
http://localhost:9080/oauth/authorize?response_type=code&client_id=curl_client&redirect_uri=http%3a%2f%2flocalhost%3a9080&scope=read&state=mystate

POST request to get the access_token, replace xxxxxx with actual code from previous step
curl -s --location --include -X POST "http://localhost:9080/oauth/token?client_id=curl_client&client_secret=user&redirect_uri=http%3a%2f%2flocalhost%3a9080&scope=read&state=mystate&grant_type=authorization_code&code=xxxxxx"

2. implicit flow
Browser GET request to get access_token directly
http://localhost:9080/oauth/authorize?response_type=token&client_id=curl_client&redirect_uri=http%3a%2f%2flocalhost%3a9080

3. client_credentials
POST request to get access_token directly
curl -s -X POST --location --include -u curl_client:user "http://localhost:9080/oauth/token?grant_type=client_credentials"


4. user password
curl -s -X POST --location --include -u curl_client:user "http://localhost:9080/oauth/token?grant_type=password&username=product_admin&password=user"
#or
curl -s -X POST --location --include "http://localhost:9080/oauth/token?grant_type=password&username=product_admin&password=user&client_id=curl_client&client_secret=user"


5. refresh_token
#replace xxxxxx with actual refresh token from previous step
curl -s -X POST --location --include -u curl_client:user "http://localhost:9080/oauth/token?grant_type=refresh_token&refresh_token=xxxxxx"
