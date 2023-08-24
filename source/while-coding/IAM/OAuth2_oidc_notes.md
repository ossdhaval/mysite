# OAuth 2.0 and OpenID Connect


<!-- TOC -->
* [OAuth 2.0 and OpenID Connect](#oauth-20-and-openid-connect)
  * [OAuth 2/2.1](#oauth-221)
    * [Grant types:](#grant-types-)
    * [Flows:](#flows-)
      * [Authorization Code Flow](#authorization-code-flow)
      * [Authorization Code Flow with PKCE](#authorization-code-flow-with-pkce)
      * [Implicit Flow with Form Post](#implicit-flow-with-form-post)
      * [Hybrid Flow](#hybrid-flow)
      * [Client Credentials Flow](#client-credentials-flow)
      * [Device Authorization Flow](#device-authorization-flow)
    * [access token](#access-token)
    * [Refresh token](#refresh-token)
    * [HTTP redirection:](#http-redirection-)
  * [OAuth 2.0 Rich Authorization Requests (draft RFC)](#oauth-20-rich-authorization-requests--draft-rfc-)
    * [Shortforms:](#shortforms-)
  * [Notes from : https://www.udemy.com/course/enterprise-oauth-for-developers](#notes-from--httpswwwudemycomcourseenterprise-oauth-for-developers)
      * [Usecases:](#usecases-)
  * [16,17. Token](#1617-token)
    * [OAuth quick data sheet (](#oauth-quick-data-sheet-)
    * [OpenID Connect data sheet](#openid-connect-data-sheet)
  * [OpenID Connect](#openid-connect)
    * [OpenID Connect uses scopes differently](#openid-connect-uses-scopes-differently)
    * [Using keycloak to protect an app with angular frontend and Java backend](#using-keycloak-to-protect-an-app-with-angular-frontend-and-java-backend)
  * [OAuth and OpenId Connect](#oauth-and-openid-connect)
  * [Client Registration](#client-registration)
    * [What is the purpose of `client` in OAuth Vs OIDC](#what-is-the-purpose-of-client-in-oauth-vs-oidc)
    * [Client authentication](#client-authentication)
      * [Shared secret](#shared-secret)
        * [client_secret_basic](#clientsecretbasic)
      * [client_secret_post](#clientsecretpost)
      * [client_secret_jwt](#clientsecretjwt)
      * [private_key_jwt](#privatekeyjwt)
      * [Few more](#few-more)
      * [Considerations for FAPI](#considerations-for-fapi)
    * [Subject type](#subject-type)
    * [Sector identifier uri](#sector-identifier-uri)
    * [Grant](#grant)
    * [Response types](#response-types)
    * [suppress authorization](#suppress-authorization)
    * [Redirect URIs](#redirect-uris)
    * [Redirect regex](#redirect-regex)
    * [Scopes](#scopes)
    * [access token type](#access-token-type)
    * [include claims in id_token](#include-claims-in-idtoken)
    * [run introspection script before JWT access token creation](#run-introspection-script-before-jwt-access-token-creation)
    * [token binding confirmation method for id_token](#token-binding-confirmation-method-for-idtoken)
    * [access token additional audiences](#access-token-additional-audiences)
    * [access token lifetime](#access-token-lifetime)
    * [refresh token lifetime](#refresh-token-lifetime)
    * [Default max auth age](#default-max-auth-age)
    * [Front channel logout uri](#front-channel-logout-uri)
    * [post logout redirect uris](#post-logout-redirect-uris)
    * [Back channel logout uri](#back-channel-logout-uri)
    * [Front channel logout session required](#front-channel-logout-session-required)
    * [Back channel logout session required](#back-channel-logout-session-required)
    * [contacts](#contacts)
    * [authorized JS origins](#authorized-js-origins)
    * [software id](#software-id)
    * [software version](#software-version)
    * [software statement](#software-statement)
    * [ciba](#ciba)
      * [token delivery method](#token-delivery-method)
      * [client notification endpoint](#client-notification-endpoint)
      * [require user code param](#require-user-code-param)
    * [PAR](#par)
      * [Request lifetime: zero default](#request-lifetime--zero-default)
      * [request PAR : check box](#request-par--check-box)
    * [UMA](#uma)
      * [PRT token type](#prt-token-type)
      * [claim redirect URI: text box](#claim-redirect-uri--text-box)
      * [RPT modification script: text box](#rpt-modification-script--text-box)
  * [Encryption/signing](#encryptionsigning)
    * [client jwks uri: text](#client-jwks-uri--text)
    * [client jwks: text](#client-jwks--text)
    * [other settings for algo: select](#other-settings-for-algo--select)
  * [advance client properties](#advance-client-properties)
    * [Default prompt login: checkbox](#default-prompt-login--checkbox)
    * [persist authorizations: checkbox](#persist-authorizations--checkbox)
    * [Allow spontaneous scopes: checkbox](#allow-spontaneous-scopes--checkbox)
    * [spontaneous scope validation regex: text](#spontaneous-scope-validation-regex--text)
    * [initial login URI](#initial-login-uri)
    * [request URIs: text](#request-uris--text)
    * [Default acr: text](#default-acr--text)
    * [allowed acr: text](#allowed-acr--text)
    * [TLS subject DN: text](#tls-subject-dn--text)
    * [Client expiration date: select](#client-expiration-date--select)
  * [client scripts](#client-scripts)
    * [Spontaneous scopes: text](#spontaneous-scopes--text)
    * [Update token: text](#update-token--text)
    * [post authn: text](#post-authn--text)
    * [instrospection: text](#instrospection--text)
    * [password grant: text](#password-grant--text)
    * [oauth consent: text](#oauth-consent--text)
    * [Data collected during registration](#data-collected-during-registration)
      * [Mandatory](#mandatory)
      * [Mandatory with Default Values](#mandatory-with-default-values)
      * [optional](#optional)
  * [Dynamic Client Registration (RFC 7591) notes:](#dynamic-client-registration--rfc-7591--notes-)
  * [other references](#other-references)
  * [Assertion](#assertion)
  * [Software Statement](#software-statement-1)
    * [In Authenticating Client](#in-authenticating-client)
    * [In Dynamic Client Registration](#in-dynamic-client-registration)
  * [Software Statement Assertions (SSA)](#software-statement-assertions--ssa-)
  * [JWT usecases](#jwt-usecases)
    * [in authorization grant](#in-authorization-grant)
    * [in client authentication](#in-client-authentication)
    * [in dynamic client registration](#in-dynamic-client-registration-1)
    * [what is special about software statement](#what-is-special-about-software-statement)
* [All flows](#all-flows)
    * [Device authorization Grant](#device-authorization-grant)
  * [Important Terms](#important-terms)
<!-- TOC -->

## OAuth 2/2.1

([oauth 2](https://datatracker.ietf.org/doc/html/rfc6749)) and [oauth 2.1](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-07)


### Grant types:

What is `Grant` in `grant type` : Basically, these are different ways of getting Granted an access token. All grant types has only one aim: to get access token. Because of different types of clients (confidential(backend) vs Public(SPA, mobile phone and desktop based native apps)) have different capabilities of protecting access tokens, there are different grant types.

Grant types become part of request to token endpoint, with parameter, `grant_type` and 

1) Authorization code
  - Uses an authorization server
  - benefit: protects access token by not sharing it with user agent and uses authorization code to do that
  - benefit: also authenticates client when it requests access token using authorization code
  - downside: more round trips than implicit flow
  - Authorization code -> access token -> 

2) Client credentials
  - client acts on its own to access resources from resource server which are owned by client 
    itself. i.e. when client is the resource owner
  
3) Refresh token:
  - This grant type is used when request is sent to token endpoint, with request parameter `grant_type=refresh_token` and refresh token, to get a new access token. 
    refer: https://www.oauth.com/oauth2-servers/making-authenticated-requests/refreshing-an-access-token/#:~:text=To%20use%20the%20refresh%20token,the%20client%20credentials%20if%20required.
  
4) Implicit : 
   
   Note: Though pure implicit grant is discouraged and [removed in oauth 2.1](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-07#name-removal-of-the-oauth-20-imp). You can safely use variant like [Implicit Flow with Form Post](https://auth0.com/docs/get-started/authentication-and-authorization-flow/implicit-flow-with-form-post) when you just want an ID token and don't want to get an access token to access resources later. If your usecases also need to request access token as well then use Authorization code with PKCE
   
  - used by client application that are built in scripting languages
  - it doesn't use authorization code and directly gives out access token to user-agent
  - benefit: more efficient than `authorization code` grant type as there are less roundtrips
  - downside: less secure as access code is shared with user-agent
  
5) Password credentials ([removed in oAuth 2.1](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-07#name-differences-from-oauth-20) - only used for if client app is trusted app. use auth code grant with pkce)
  - resource owner gives user-id/password credentials to client application once and client app uses these 
    credentials to get a long-lived access token
  - client doesn't store resource owner credentials once it has an access token or refresh token
  - benefit: simplified workflown when dealing with a trusted client
  - downside: very insecure as client gets the credentials
  
6) Extension Grants
As defined in: https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-07#section-4.4

Auth server can define and many other RFCs have created their own standard extension grants. For example, [here](https://www.rfc-editor.org/rfc/rfc8628.html#section-3.4) the device code grant RFC defines it's own grant (extension grant) `urn:ietf:params:oauth:grant-type:device_code`.

### Flows:

Ref for below content: https://auth0.com/docs/get-started/authentication-and-authorization-flow

- There are two things that decide what flow are you using
  - `response_type=` param in request to `authorize` endpoint
  - `grant_type=` param in request to `token` endpoint

| flow                              | response type         | grant                                          | other imp params                                   | comments                                                                                                                                   |
|-----------------------------------|-----------------------|------------------------------------------------|----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| Authorization Code Flow           | `code`                | `authorization_code`                           | `scope`                                            | Suitable when you have a `confidential` client that can safely store client credentials, like an app running on server                     |
| Authorization Code Flow with PKCE | `code`                | `authorization_code`                           | `code_challenge`, `code_challenge_method`, `scope` | Use this grant type for applications that cannot store a client secret, such as native or single-page apps                                 |
| Implicit Flow with Form Post      | `id_token token`      | -                                              | -                                                  | Suitable when application just needs user details(id_token) and doesn't need to request access token from token endpoint to make API calls |
| Hybrid Flow                       | `code id_token token` | `authorization_code`                           | -                                                  | comments                                                                                                                                   |
| Client Credentials Flow           | -                     | `client_credentials`                           | other imp params                                   | comments                                                                                                                                   |
| Device Authorization Flow         | -                     | `urn:ietf:params:oauth:grant-type:device_code` | other imp params                                   | comments                                                                                                                                   |
| Resource Owner Password Flow      | -                     | `password`                                     | other imp params                                   | comments                                                                                                                                   |

Usually, type of grant is the also the flow that you are using. But there can be flows that use combination of grants. Like [hybrid](https://auth0.com/docs/get-started/authentication-and-authorization-flow/hybrid-flow) flow.

#### [Authorization Code Flow](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-07#name-authorization-code-grant)

- Request to get the code from authorize endpoint
  
  ```json
    https://{yourDomain}/authorize?
    response_type=code&
    client_id={yourClientId}&
    redirect_uri={https://yourApp/callback}&
    scope=openid%20profile&
    state=xyzABC123"
   ```
   
- Response should be similar to 

  ```
    HTTP/1.1 302 Found
    Location: {https://yourApp/callback}?code={authorizationCode}&state=xyzABC123
  ```

- Request token to token endpoint

  ```json
  curl --request POST \
  --url 'https://{yourDomain}/oauth/token' \
  --header 'content-type: application/x-www-form-urlencoded' \
  --data grant_type=authorization_code \
  --data 'client_id={yourClientId}' \
  --data 'client_secret={yourClientSecret}' \
  --data 'code=yourAuthorizationCode}' \
  --data 'redirect_uri={https://yourApp/callback}'
  ```

- Response from token endpoint

  ```json
  {
  "access_token": "eyJz93a...k4laUWw",
  "refresh_token": "GEbRxBN...edjnXbL",
  "id_token": "eyJ0XAi...4faeEoQ",
  "token_type": "Bearer"
  }
  ```

#### [Authorization Code Flow with PKCE](https://www.rfc-editor.org/rfc/rfc7636)


- Request to get the code from authorize endpoint

  ```json
  https://{yourDomain}/authorize?
  response_type=code&
  code_challenge=E9Melhoa2OwvFrEMTJguCHaoeK1t8URWbuGJSstw-cM&
  code_challenge_method=S256&
  client_id={yourClientId}&
  redirect_uri={yourCallbackUrl}&
  scope=openid%20profile&
  state=xyzABC123
   ```

- Response should be similar to

  ```
  HTTP/1.1 302 Found
  Location: {yourCallbackUrl}?code={authorizationCode}&state=xyzABC123
  ```

- Request token to token endpoint

  ```json
  curl --request POST \
  --url 'https://{yourDomain}/oauth/token' \
  --header 'content-type: application/x-www-form-urlencoded' \
  --data grant_type=authorization_code \
  --data 'client_id={yourClientId}' \
  --data 'code_verifier={yourGeneratedCodeVerifier}' \
  --data 'code={yourAuthorizationCode}' \
  --data 'redirect_uri={https://yourApp/callback}'
  ```

- Response from token endpoint

  ```json
  https://{yourDomain}/authorize?
  response_type=code&
  code_challenge=E9Melhoa2OwvFrEMTJguCHaoeK1t8URWbuGJSstw-cM&
  code_challenge_method=S256&
  client_id={yourClientId}&
  redirect_uri={yourCallbackUrl}&
  scope=openid%20profile&
  state=xyzABC123
  ```

#### Implicit Flow with Form Post
 

- Request to get the code from authorize endpoint

  ```json
  https://{yourDomain}/authorize?
  response_type=id_token token&
  response_mode=form_post&
  client_id={yourClientId}&
  redirect_uri={https://yourApp/callback}&
  scope=read:tests&
  state=xyzABC123&
  nonce=eq...hPmz
   ```

- Response should be similar to

  ```
  HTTP/1.1 302 Found
    Content-Type: application/x-www-form-urlencoded
    id_token=eyJ...acA&
    state=xyzABC123
  ```

#### [Hybrid Flow](https://openid.net/specs/openid-connect-core-1_0.html#HybridFlowAuth)

- Request to get the code from authorize endpoint

  ```json
  https://{yourDomain}/authorize?
  response_type=code id_token token&
  client_id={yourClientId}&
  redirect_uri={https://yourApp/callback}&  
  scope=appointments%20contacts&
  audience=appointments:api&
  state=xyzABC123&
  nonce=eq...hPmz
   ```

- Response should be similar to

  ```
    HTTP/1.1 302 Found
    Content-Type: application/x-www-form-urlencoded
    code=AUTHORIZATION_CODE&
    access_token=ey...MhPw
    &expires_in=7200
    &token_type=Bearer
    id_token=eyJ...acA&
    state=xyzABC123
  ```

  - Request token to token endpoint

    ```json
    curl --request POST \
    --url 'https://{yourDomain}/oauth/token' \
    --header 'content-type: application/x-www-form-urlencoded' \
    --data grant_type=authorization_code \
    --data 'client_id={yourClientId}' \
    --data 'client_secret={yourClientSecret}' \
    --data 'code=yourAuthorizationCode}' \
    --data 'redirect_uri={https://yourApp/callback}'
    ```

- Response from token endpoint

  ```json
  {
  "access_token": "eyJz93a...k4laUWw",
  "refresh_token": "GEbRxBN...edjnXbL",
  "id_token": "eyJ0XAi...4faeEoQ",
  "token_type": "Bearer"
  }
  ```

#### [Client Credentials Flow](https://www.rfc-editor.org/rfc/rfc6749#section-4.4)


- Request token to token endpoint

  ```json
  curl --request POST \
  --url 'https://{yourDomain}/oauth/token' \
  --header 'content-type: application/x-www-form-urlencoded' \
  --data grant_type=client_credentials \
  --data client_id=YOUR_CLIENT_ID \
  --data client_secret=YOUR_CLIENT_SECRET \
  --data audience=YOUR_API_IDENTIFIER
  ```

- Response from token endpoint

  ```json
  {
  "access_token":"eyJz93a...k4laUWw",
  "token_type":"Bearer",
  "expires_in":86400
  }
  ```

#### [Device Authorization Flow](https://www.rfc-editor.org/rfc/rfc8628)

- Request from the device to device code endpoint to get device code 

  ```json
  curl --request POST \
  --url 'https://{yourDomain}/oauth/device/code' \
  --header 'content-type: application/x-www-form-urlencoded' \
  --data 'client_id={yourClientId}' \
  --data 'scope={scope}' \
  --data 'audience={audience}'
   ```

- Response should be similar to

  ```
  {
  "device_code": "Ag_EE...ko1p",
  "user_code": "QTZL-MCBW",
  "verification_uri": "https://accounts.acmetest.org/activate",
  "verification_uri_complete": "https://accounts.acmetest.org/activate?user_code=QTZL-MCBW",
  "expires_in": 900,
  "interval": 5
  }
  ```

- Polling request from the device to token endpoint to get the token  

  ```json
  curl --request POST \
  --url 'https://{yourDomain}/oauth/token' \
  --header 'content-type: application/x-www-form-urlencoded' \
  --data grant_type=urn:ietf:params:oauth:grant-type:device_code \
  --data 'device_code={yourDeviceCode}' \
  --data 'client_id={yourClientId}'
  ```

- response should be similar to 

  ```
  {
  "error": "authorization_pending",
  "error_description": "..."
  }
  ```

  "error" values can be `slow_down`, `access_denied`, `expired_token`

  or when user successfully authorizes via browser, the next polling request from device gets below response

  ```json
  {
  "access_token":"eyJz93a...k4laUWw",
  "refresh_token":"GEbRxBN...edjnXbL",
  "id_token": "eyJ0XAi...4faeEoQ",
  "token_type":"Bearer",
  "expires_in":86400
 }
  ```

#### [Resource Owner Password Flow](https://www.rfc-editor.org/rfc/rfc6749#section-4.3)

- Request token to token endpoint

  ```json
  curl --request POST \
  --url 'https://{yourDomain}/oauth/token' \
  --header 'content-type: application/x-www-form-urlencoded' \
  --data grant_type=password \
  --data 'username={username}' \
  --data 'password={password}' \
  --data 'audience={yourApiIdentifier}' \
  --data scope=read:sample \
  --data 'client_id={yourClientId}' \
  --data 'client_secret={yourClientSecret}'
  ```

- Response from token endpoint

  ```json
  {
  "access_token": "eyJz93a...k4laUWw",
  "refresh_token": "GEbRxBN...edjnXbL",
  "id_token": "eyJ0XAi...4faeEoQ",
  "token_type": "Bearer",
  "expires_in": 36000
  }
  ```

### access token

  - Access token is created by authorization server, given to client to access resources on resource server.
  - Access token can be opaque or structured token.
  - Authorization server creates an access token. It also specifies a life time duration for token when 
    creating it. A background process on authorization server keeps on checking tokens and expires them as their lifetime ends.
  - Janssen supports one token type which is bearer token as 
    described in this [RFC6750](https://datatracker.ietf.org/doc/html/rfc6750)

### Refresh token

  - refresh token is issued by authorization server at the time of issueing access token but this is not mendatory.
  - once access token expires, the client can present refresh token to authorization server(AS) to get a new access token.
  - client can also present refresh token to AS to get more access tokens with same or less priviledges
  
### HTTP redirection:

  - This specification makes extensive use of HTTP redirections, in which the client or the 
    authorization server directs the resource owner's user-agent to another destination. While the 
    examples in this specification show the use of the HTTP 302 status code, any other method available via the 
    user-agent to accomplish this redirection is allowed and is considered to be an implementation detail.

## DPoP

spec: https://www.ietf.org/archive/id/draft-ietf-oauth-dpop-16.html

DPoP is used when MTLS can't be used. I.e in single page applications. Purpose of both DPoP and MTLS is to ensure that the access token in the request is being used by the client to which it was originally issued and not by someone who stole it. This is called `sender-constrained` token. DPoP is a method of creating such sender
constrained access tokens.

```
The main data structure introduced by this specification is a DPoP proof JWT, described in detail below, which is sent as a header in an HTTP request. A client uses a DPoP proof JWT to prove the possession of a private key corresponding to a certain public key.

Roughly speaking, a DPoP proof is a signature over some data of the HTTP request to which it is attached, a timestamp, a unique identifier, an optional server-provided nonce, and a hash of the associated access token when an access token is present within the request.
```

Using DPoP means, client sending DPoP proof when requesting a new access token, plus client sendig DPoP proof along with access token to access the protected resources. The DPoP proof is sent as value of request header `DPoP`. DPoP proofs(JWT) used in both steps are generated by client using a slightly different methods. The payload differs in both cases. In the first case (while requesting a new access token), the dpop proof JWT payload doesn't have hash created from access token. In the second case (while requesting a protected resource), the DPoP proof has the hash of the access token in it's payload. 

So, DPoP proof can be generated by client, and it is a JWT. (this JWT is created by HTTP request data (API that client want to access), timestamp, a unique id and optionally a server nonce, plus access token hash if request is also having the `Bearer` header with access token. And sign all these data elements using private key to create a JWT.







## OAuth 2.0 Rich Authorization Requests ([draft RFC](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-rar))

   Interpretation of the value of the "type" parameter, and the object
   elements that the "type" parameter allows, is under the control of
   the AS.

change areas:

- Authorization requests as specified in [RFC6749],
- Device Authorization Request as specified in [RFC8628],
- Backchannel Authentication Requests as defined in [OpenID.CIBA].

### Shortforms:

`RP`: Relying Party (client)
`OP`: OpenID provider


Notes from : https://www.udemy.com/course/enterprise-oauth-for-developers
----

#### Usecases:
1. Introduction
  - Websites asking you to login using facebook/google login
  - email clients like outlook on your windows desktop that wants to aggregate emails from gmail, yahoo, etc
  - TV that gives you a code to enter into a mobile app in order to log into tv app
  - sites that aggregate hotel data and in order to show you cheapest rentals
  - finance apps taht show your finances at one place

2. Security basics (Authentication and Authorization)
  - Service provider: This is the target application that is being protected. Authorization is responsibility of service provider
  - Identity provider: takes care of authentication. Like active directory, LDAP etc
  - service provider and identity provider could be in different data-centers. Like in enterprise app deployed in public cloud where user authentication is performed by on-prem cloud application of security reasons.

6.
  - Sending username-password to service provider is not good practice rather it should be sent directly to Identity provider

7. SAML
  - SAML addresses two issues
    - LDAP has to be in the same data-center
    - User has to enter credentials manually
  - SAML flow depends on browser redirects, so only browser based users can be authenticated
  - SAML uses xml to send data in request and response
  - SAML uses encrypted tokens so SAML identity provider and application Service provider need to have each others certificates in order to decrypt tokens

9. Enterprise problem usecases
  - Securing the REST APIs. One way is to send SAML token in every request but this is not feasible as token is too large plus the REST API will have to store SAML metadata.
  - Plus, when a process (lick cron job) is calling REST API, how can cron job get a SAML token?
  - SAML is great for implementing SSO in enterprise, but it can't hadle rest APIs authentication in an enterprise. 

15. Client registration
  - client registration is first step that any app has to perform in order to integrate an oauth flow
  - In this process, client registers with oauth authorization server by furnishing various details and most importantly redirect urls. Details required for registration can change from oauth provider to provider. Like, okta might have different ask from authO.
  - in response to registration, the client app gets two things client id and client secret. 
  - This ID and secret are required to be sent to authorization server by client everytime client send resource owner's request for authorization 

16. Tokens
  - Tokens are of two types: Opaque and Structured
    - Opaque tokens are a randomly generated alpha-numeric string. It can be utilised by authorization server as access token. It is opaque as it doesn't contain any information about token itself. Like expiry time, who is the subject, scopes for which it was authorized etc. When client sends request to (by putting token in `Authorization: bearer <token>` request header) resource server to access resources with a opaque token, the resource server has to call authorization server to get details about token. This adds to performance problems. 
    - Structured token: This is second type of token that can be used as access token by autho server. This token, has jwt format and describes itself. On decoding it, resource server can get all the information like expiry, scopes etc. without needing to go to autho server. This token is signed by autho server using it's private key and resource server can varify this using public key. This token is also sent to resource server by client by putting token in `Authorization: bearer <token>` request header
    
16,17. Token
  - 


### OAuth quick data sheet (
- response_type : `code`, `token`
- grant_type : `authorization_code`, `refresh_token`, `ropc`, `client_credentials`
- scope : no specific values
- token : `access_token`, `refresh_token`
- No identifiers from resource_owners(users)
- No resource enpoints


### OpenID Connect data sheet

- response_type : `code`, `token`, `id_token` and any combination of these three for example `code id_token` or all three `code id_token token`. Note: as `implicite flow` is discouraged, try not to use any flow that involves `token` response type in authorization request.
- grant_type : `authorization_code`, `refresh_token`, OIDC has removed `ropc`, `client_credentials` scopes. 
- scope : `openid` (this acts like a signal for auth server that this request is OIDC request and all other things like scopes and grant types should be processed with reference to OIDC. Without this scope, the request is treated as OAuth2 request), `profile`, `email`, `phone`, `address`
- token : `access_token`, `refresh_token`, `id_token`(JWT)
- identifiers from resource_owners(users) : can get it through `id_token`
- resource enpoints : /userinfo

Reference:
- very good understanding of OIDC with respect to OAuth: 

  https://www.youtube.com/watch?v=VI3G4Quzsb8

## OpenID Connect

OpenID Connect is `authentication` layer on top of OAuth 2. Why 'on top of'? that is because OIDC adds one more token and few scopes within Oauth flows.

OIDC has three flows:


OIDC adds more scopes:
- `openid`: requests `id token` from auth server. ID token is just a JSON token which contains basic information about user
- `email`: requests auth server to add email information to `id token`

OIDC adds `id token`
- ID token is just a JSON token which contains basic information about user
- so if you have mentioned `openid` scope, then in auth-code flow, when you request access token from auth server using auth-code, auth server will send you id token along with access token.
- 


### OpenID Connect uses scopes differently

https://openid.net/specs/openid-connect-core-1_0.html#ScopeClaims

Scopes are used to control what information about user should be returned by the userinfo endpoint. As scopes are associated with access token, the OP can look at token, find out the scopes and release information accordingly from userinfo endpoint response.

profile: OPTIONAL. This scope value requests access to the End-User's default profile Claims, which are: name, family_name, given_name, middle_name, nickname, preferred_username, profile, picture, website, gender, birthdate, zoneinfo, locale, and updated_at.

email: OPTIONAL. This scope value requests access to the email and email_verified Claims.

address: OPTIONAL. This scope value requests access to the address Claim.

phone: OPTIONAL. This scope value requests access to the phone_number and phone_number_verified Claims.

### Using keycloak to protect an app with angular frontend and Java backend

- Here you can use it in two ways, one is to use standard `authorization code` flow and other is to use `authorization code flow wit PKCE`



## OAuth and OpenId Connect

- Since openid connect is built on top of oauth, there can not be an implementation of OIDC only. All the servers are 
    oauth first and then OIDC is developed on top of that. So, every OP(OpenId Connect Provider) is also an oauth provider.
- similarly, there can not be a client that is only oidc client. Rather, OIDC spec doesn't have definition of OIDC client. 
    An oauth client that requires users to be authenticated is called an RP (relying party). Hence there are no two flavors
    of clients at the time of registration.
- When in Oauth context, refer to server as AS(Authorization Server) and client as client. When talking about OIDC,
    refer to server as OP (OIDC provider) and client as RP (relying party)

## Client Registration

### What is the purpose of `client` in OAuth Vs OIDC
  - In OIDC, `client` is a server(called relying party) that wants to protect resources on resource server (RS) using authentication
  - In OAuth, `client` is a third party app server which wants to access resources in RP/RS

Major aspects of client registration is mentioned in the [OAuth spec](https://datatracker.ietf.org/doc/html/rfc6749#section-2). 
Important points are as below:

- Before initiating the protocol, the client registers with the authorization server.
- If the client registers as `confidential` client, it has to authenticate itself everytime it requests for an access token 
    at the token endpoint

### Client authentication

(In Jans, this defaults to `client_secret_basic`)

Ref:
    -   https://darutk.medium.com/oauth-2-0-client-authentication-4b5f929305d4
    -   https://connect2id.com/products/server/docs/guides/oauth-client-authentication#credential-types

OAuth spec does not details out how client authenticates with authz server , but [mentions few](https://datatracker.ietf.org/doc/html/rfc6749#section-2.3)
methods as guidelines.

[OIDC](https://openid.net/specs/openid-connect-core-1_0.html#ClientAuthentication) spec gives more details.
Janssen supports all four authentication methods(client_secret_basic(default), client_secret_post,
client_secret_jwt,  as per )

Authn methods can be broadly classified in Two types:
-   Shared secret (client_secret_basic(default), client_secret_post, client_secret_jwt)
-   Private key (private_key_jwt)

#### Shared secret

##### client_secret_basic

[Refer 1.4 in this](https://darutk.medium.com/oauth-2-0-client-authentication-4b5f929305d4)

#### client_secret_post

[Refer 1.3 in this](https://darutk.medium.com/oauth-2-0-client-authentication-4b5f929305d4)

#### client_secret_jwt

[Refer 1.5 in this](https://darutk.medium.com/oauth-2-0-client-authentication-4b5f929305d4)

#### private_key_jwt

[Refer 1.6 in this](https://darutk.medium.com/oauth-2-0-client-authentication-4b5f929305d4)

#### Few more

[Refer 1.7 and 1.8 in this](https://darutk.medium.com/oauth-2-0-client-authentication-4b5f929305d4)

#### Considerations for FAPI

[Refer 3. in this](https://darutk.medium.com/oauth-2-0-client-authentication-4b5f929305d4)

### Subject type
(Jans default: public)
Defined by OIDC [REF](https://openid.net/specs/openid-connect-core-1_0.html#SubjectIDTypes) 

### Sector identifier uri
(jans defaul: blank)
Defined by OIDC section 8.1 [REF](https://openid.net/specs/openid-connect-core-1_0.html#SubjectIDTypes)
 
### Grant

Jans Default selected on TUI: None 

Jans supports:  

"authorization_code", "refresh_token", "client_credentials", "urn:openid:params:grant-type:ciba", "urn:ietf:params:oauth:grant-type:uma-ticket", "implicit", "password", "urn:ietf:params:oauth:grant-type:token-exchange", "urn:ietf:params:oauth:grant-type:device_code"

[Relationship between Grant Types and Response Types](https://www.rfc-editor.org/rfc/rfc7591#section-2.1)

### Response types

Jans Default selected on TUI: None

Jans supports: all combinations of `code`, `token` and `id_token`

"id_token", "token", "code", "id_token token code", "token code", "id_token token", "id_token code"

[Relationship between Grant Types and Response Types](https://www.rfc-editor.org/rfc/rfc7591#section-2.1)

[Relation between response types and response modes](https://openid.net/specs/oauth-v2-multiple-response-types-1_0.html)



### suppress authorization

??

### Redirect URIs

### Redirect regex

### Scopes

------------ items below are in token category in tui --------

### access token type

Jans Default selected on TUI: JWT

Jans supports `JWT` or `Reference` types. 

### include claims in id_token

Jans Default selected on TUI: blank checkbox

### run introspection script before JWT access token creation

Jans Default selected on TUI: blank checkbox

### token binding confirmation method for id_token

Jans Default selected on TUI: blank checkbox

RFCs for token binding:

https://www.rfc-editor.org/rfc/rfc8471

https://www.rfc-editor.org/rfc/rfc8473

https://openid.net/specs/openid-connect-token-bound-authentication-1_0.html

for quick understanding of what token binding is, read the first few paragraphs in below:

https://medium.facilelogin.com/oauth-2-0-token-binding-e84cbb2e60

### access token additional audiences

- see why access token needs audience: https://openid.net/specs/openid-connect-core-1_0.html#AccessTokenRedirect
- what is audience: https://www.youtube.com/watch?v=LdyeC9Il3Cs

Jans Default selected on TUI: blank

### access token lifetime

### refresh token lifetime

### Default max auth age


------------ items below are in Logout category in tui --------

Logout is OIDC thing. Not OAuth.

To understand logout, understanding session management [(spec)](https://openid.net/specs/openid-connect-session-1_0.html) is important.

```shell
This specification complements the OpenID Connect Core 1.0 [OpenID.Core] specification by defining how to monitor 
the End-User's login status at the OpenID Provider on an ongoing basis so that the Relying Party can log out an 
End-User who has logged out of the OpenID Provider.

Both this specification and the OpenID Connect Front-Channel Logout 1.0 [OpenID.FrontChannel] specification use 
front-channel communication, which communicate logout requests from the OP to RPs via the User Agent. 
In contrast, the OpenID Connect Back-Channel Logout 1.0 [OpenID.BackChannel] specification uses direct back-channel communication 
between the OP and RPs being logged out. The OpenID Connect RP-Initiated Logout 1.0 [OpenID.RPInitiated] specification 
complements these specifications by defining a mechanism for a Relying Party to request that an OpenID Provider log out 
the End-User. This specification can be used separately from or in combination with these other three specifications.
```

The front and back channel logout specs complement core OpenID Connect with mechanisms for notifying concerned relying parties that an end-user has been logged out of the identity provider:

- The front-channel logout mechanism[(spec)](https://openid.net/specs/openid-connect-frontchannel-1_0.html) notifies the relying party by calling a URL via a hidden browser iframe.

- The back-channel logout mechanism[(spec)] submits the notification as a special logout token (JWT) that is posted directly to the relying party

The relying party must be registered to receive front or back-channel notifications. Those will be delivered only for sessions into which the relying party previously logged in a user (received an ID token)

for more understanding : 
https://betterprogramming.pub/managing-user-sessions-and-openid-connect-logout-eb886facd321
https://medium.com/@robert.broeckelmann/openid-connect-logout-eccc73df758f
https://curity.io/resources/learn/openid-connect-logout/

Specifications:

https://openid.net/specs/openid-connect-session-1_0.html
https://openid.net/specs/openid-connect-rpinitiated-1_0.html
https://openid.net/specs/openid-connect-frontchannel-1_0.html
https://openid.net/specs/openid-connect-backchannel-1_0.html#BCSupport

### Front channel logout uri

### post logout redirect uris

### Back channel logout uri

### Front channel logout session required

### Back channel logout session required

------------ items below are in sofware info category in tui --------

### contacts
### authorized JS origins
### software id
### software version
### software statement

------------ items below are in ciba/par/uma category in tui --------

### ciba

#### token delivery method 
- poll (default)
- push
- ping

#### client notification endpoint 
#### require user code param

### PAR

#### Request lifetime: zero default
#### request PAR : check box

### UMA

#### PRT token type     
- jwt
- reference (default)

#### claim redirect URI: text box

#### RPT modification script: text box 

------------ items below are in Cryptograph/signing category in tui --------

remember: as per [section 10](https://openid.net/specs/openid-connect-core-1_0.html#SigEnc) the jwks and keys used for signing and encryption
are used across all places where encryption and signing is required. See the excerpt below:

```
Depending on the transport through which the messages are sent, the integrity of the message might not be guaranteed and the originator of the message might not be authenticated. To mitigate these risks, ID Token, UserInfo Response, Request Object, and Client Authentication JWT values can utilize
```

## Encryption/signing

### client jwks uri: text
### client jwks: text
### other settings for algo: select

------------ items below are in advance client properties category in tui --------

## advance client properties

### Default prompt login: checkbox
### persist authorizations: checkbox
### Allow spontaneous scopes: checkbox
### spontaneous scope validation regex: text
### initial login URI
### request URIs: text
### Default acr: text
### allowed acr: text
### TLS subject DN: text
### Client expiration date: select

------------ items below are in client scripts category in tui --------

## client scripts

### Spontaneous scopes: text
### Update token: text
### post authn: text
### instrospection: text
### password grant: text
### oauth consent: text



### Data collected during registration

#### Mandatory

#### Mandatory with Default Values

#### optional



## Dynamic Client Registration notes:

SPECS (in the dependency order) :
- [OpenId Connect DCR SPEC](https://openid.net/specs/openid-connect-registration-1_0.html)
- [OAuth dynamic client management(CRUD) - RFC 7592](https://www.rfc-editor.org/rfc/rfc7592)
- [OAuth DCR - RFC 7591](https://www.rfc-editor.org/rfc/rfc7591)


Traditionally, registration of a client with an authorization server
   is performed manually.  The mechanisms defined in this specification
   can be used either for a client to dynamically register itself with
   authorization servers or for a client developer to programmatically
   register the client with authorization servers.

   
The OAuth DCR SPEC generalizes the
   registration mechanisms defined by "OpenID Connect Dynamic Client
   Registration 1.0" [OpenID.Registration] and used by "User Managed
   Access (UMA) Profile of OAuth 2.0" [UMA-Core] in a way that is
   compatible with both, while being applicable to a wider set of OAuth
   2.0 use cases.
   
   
**Usecases**: very useful for understanding and choices: https://www.rfc-editor.org/rfc/rfc7591#appendix-A
   
## other references
- https://github.com/zmartzone/mod_auth_openidc/blob/master/auth_openidc.conf
- https://curity.io/resources/learn/openid-connect-understanding-dcr/
- https://curity.io/resources/learn/using-dynamic-client-registration/
- https://www.youtube.com/watch?v=AsCL8kMU1iY
- https://www.youtube.com/watch?v=WnI32e4eEuY
- https://connect2id.com/products/server/docs/api/client-registration#initial-access
- Very good link to understand issueing of tokens https://darutk.medium.com/diagrams-of-all-the-openid-connect-flows-6968e3990660

Notes:

- sometimes people use DCR acronym to refer to `dynamic client request` and sometimes DCR means `dynamic client registration`. Dynamic client request is the request
made to register the client dynamically. For example, in statement `In OpenBanking case DCR (Dynamic Client Request) is signed and must contain SSA (Software Statement Assertion) inside it.` DCR means the request.
- the OIDC DCR SPEC
  - 

## Assertion

As defined in [OAuth Assertion Framework]([https://www.rfc-editor.org/rfc/rfc7521#section-1](https://www.rfc-editor.org/rfc/rfc7521#section-3))

```
An assertion is a package of information that allows identity and
security information to be shared across security domains.  An
assertion typically contains information about a subject or
principal, information about the party that issued the assertion and
when was it issued, and the conditions under which the assertion is
to be considered valid, such as when and where it can be used.

The entity that creates and signs or integrity-protects the assertion
is typically known as the "Issuer", and the entity that consumes the
assertion and relies on its information is typically known as the
"Relying Party".  In the context of this document, the authorization
server acts as a relying party.

```

- assertions MUST be signed or signed+encrypted
- there are two common patterns by which client can obtain 
  - issued by third party (also called `security token service`, `token service`) ( see, now at this point, `assertion` is being called `token`. This is the reason behind token often being called assertion in general.)
  - client creates assertions locally (using shared secret or private-public key pair). Although assertions are usually used to convey identity and     security information, self-issued assertions can also serve a different purpose.  They can be used to demonstrate knowledge of some secret, such as a client secret, without actually communicating the secret directly in the transaction.

From the perspective of what must be done by the entity presenting the assertion, there are two general types of assertions:

- **Bearer Assertions**: (Note: this is the origin of `bearer` token). Any entity in possession of a bearer assertion (the bearer) can use it to get access to the associated resources (without demonstrating possession of a cryptographic key).  To prevent misuse, bearer assertions need to be protected from disclosure in storage and in transport.  Secure communication channels are required between all entities to avoid leaking the assertion to unauthorized parties.

- **Holder-of-Key Assertions**: To access the associated resources, the entity presenting the assertion must demonstrate possession of additional cryptographic material.  The token service thereby binds a key identifier to the assertion, and the client has to demonstrate to the relying party that it knows the key corresponding to that identifier when presenting the assertion.

- Assertion framework itself doesn't specify format(like JSON etc) but it [points](https://www.rfc-editor.org/rfc/rfc7521#section-7) to SAML and JWT specs for implementation details. JWT, as we know, is the more prefered and widely used. So this is how assertions, tokens and JWT are connected to each other via OAuth Assertion Framework.

This spec details two usages of assertions (read JWT) in two ways when communicating to `token endpoint`:
- Using Assertions as Authorization Grants
- Using Assertions for Client Authentication (from here the client authn methods of `client_secret_jwt` and `private_key_jwt` originates)

## Software Statement

- Defining Software statements: Under https://datatracker.ietf.org/doc/html/rfc7591#section-1.2

  ```
  A digitally signed or MACed JSON Web Token (JWT) [RFC7519] that
  asserts metadata values about the client software.  In some cases,
  a software statement will be issued directly by the client
  developer.  In other cases, a software statement will be issued by
  a third-party organization for use by the client developer.  In
  both cases, the trust relationship the authorization server has
  with the issuer of the software statement is intended to be used
  as an input to the evaluation of whether the registration request
  is accepted.  A software statement can be presented to an
  authorization server as part of a client registration request.
  ```
  
- Software statement can be signed by organization that is developing the client or a third party.
- [this section](https://datatracker.ietf.org/doc/html/rfc7591#section-2.3) also says:

  ```
  In some cases, authorization servers MAY choose to accept a software
  statement value directly as a client identifier in an authorization
  request, without a prior dynamic client registration having been
  performed.
  ```

Usage:
- In authenticating client
- In registering client (DCR)

### In Authenticating Client

### In Dynamic Client Registration
- When presented to the authorization server as part of a client registration request, the software statement MUST contain an "iss" (issuer) claim denoting the party attesting to the claims in the software statement.

- Can be controlled using feature flag
- Relevent config properties:
  -  softwareStatementValidationType
  -  dcrSignatureValidationSoftwareStatementJwksURIClaim
  -  dcrSignatureValidationSoftwareStatementJwksClaim

- Very little material is available around software statements and SSA. Below is a list
  
  - How to create software statement, SSA and perform DCR in Openbanking: https://www.youtube.com/playlist?list=PLB4KVrA_iiEHiTHd0ZGLcPUkEuslABfdJ
  - Good videos which show how software statements are used in Open banking. Good for understanding: https://www.youtube.com/watch?v=YeviOSq1jjU&t=173s


## Software Statement Assertions (SSA)

- It is defined here: https://openbankinguk.github.io/dcr-docs-pub/v3.3/dynamic-client-registration.html#software-statement

- Software statement Vs Software Statement Assertions (SSA), are these two different?

  Yes, Excerpt from [here](https://docs.jans.io/v1.0.6/admin/auth-server/endpoints/client-registration/#5-special-mention-about-fapi)
  
  ```
  In case of a typical client registration request in FAPI implementation, the request object which is a signed JWT (as seen in point 3) is also called     an SSA (Software statement Assertion) or DCR payload. This SSA can contain the software_statement inside it which is also a signed JWT. Each of the       JWTs, the outer JWT called the SSA and the inner JWT called the software_statement are signed by different entities - the TPP and OBIE respectively.
  ```

## JWT usecases

### in authorization grant

see [this](https://www.rfc-editor.org/rfc/rfc7523#section-2.1)

### in client authentication

see [this](https://www.rfc-editor.org/rfc/rfc7523#section-2.2)

### in dynamic client registration

### what is special about software statement


## Understanding ACR

`ACR` is `Authentication Context Class Reference`. It is a value that denotes what is the level of authentication that this user has or should gone through. ACR values are custom to each implementation. To understand ACR more, we have to understand `Authentication Context` and `Authentication Context class`.

**Authentication Context**:

Definition as per OIDC core:
Information that the Relying Party can require before it makes an entitlement decision with respect to an authentication response. Such context can include, but is not limited to, the actual authentication method used or level of assurance such as ISO/IEC 29115 [ISO29115] entity authentication assurance level

So basically, it is the context which the RP uses to understand how this person has been authenticated. And may be based on that it gives entitlements to that person(i.e session)

**Authentication Context Class**:

Definition as per OIDC core:
Set of authentication methods or procedures that are considered to be equivalent to each other in a particular context.

Going by the definition, it looks like there can be more than one method or procedures that pertain to the same class.

**ACR**: is a way to refer to the Authentication Context Class

Basically, in jans, acr value -> script has one to one relation. And every script has a level.

Jans server:

`default_acr`

`Internal ACR`

An Authentication method is offered by the AS if its ACR value i.e. its corresponding custom script is enabled.

Level (rank) of an Authentication mechanism: 

Each authentication mechanism (script) has a "Level" assigned to it which describes how secure and reliable it is. The higher the "Level", higher is the reliability represented by the script. Though several mechanisms can be enabled at the same Janssen server instance at the same time, for any specific user's session only one of them can be set as the current one (and will be returned as acr claim of id_token for them). If initial session is created and then later a new authorization request from a RP comes in specifying another authentication method, its "Level" will be compared to that of the method currently associated with this session. If requested method's "Level" is lower or equal to it, nothing is changed and the usual SSO behavior is observed. If it's higher (i.e. a more secure method is requested), it's not possible to serve such request using the existing session's context, and user must re-authenticate themselves to continue. If they succeed, a new session becomes associated with that requested mechanism instead.

Client level:

`default_acr_values`

`acr_values`

`acr` claim of id_token

# All flows

### Device authorization Grant

https://datatracker.ietf.org/doc/html/rfc8628

      +----------+                                +----------------+
      |          |>---(A)-- Client Identifier --->|                |
      |          |                                |                |
      |          |<---(B)-- Device Code,      ---<|                |
      |          |          User Code,            |                |
      |  Device  |          & Verification URI    |                |
      |  Client  |                                |                |
      |          |  [polling]                     |                |
      |          |>---(E)-- Device Code       --->|                |
      |          |          & Client Identifier   |                |
      |          |                                |  Authorization |
      |          |<---(F)-- Access Token      ---<|     Server     |
      +----------+   (& Optional Refresh Token)   |                |
            v                                     |                |
            :                                     |                |
           (C) User Code & Verification URI       |                |
            :                                     |                |
            v                                     |                |
      +----------+                                |                |
      | End User |                                |                |
      |    at    |<---(D)-- End user reviews  --->|                |
      |  Browser |          authorization request |                |
      +----------+                                +----------------+

                    Figure 1: Device Authorization Flow


## Important Terms

| Term                                         | definition                                                                                                                                                                                                                                                                                                             | source                                                                               | example |
|----------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|---------|
| Identity                                     | Set of attributes related to an Entity                                                                                                                                                                                                                                                                                 | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| Entity                                       | Something that has a separate and distinct existence and that can be identified in a context. An End-User is one example of an Entity.                                                                                                                                                                                 | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| Authentication                               | Process used to achieve sufficient confidence in the binding between the Entity and the presented Identity                                                                                                                                                                                                             | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| Claim                                        | Piece of information asserted about an Entity                                                                                                                                                                                                                                                                          | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| Claims Provider                              | Server that can return Claims about an Entity                                                                                                                                                                                                                                                                          | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| Essential Claim                              | Claim specified by the Client as being necessary to ensure a smooth authorization experience for the specific task requested by the End-User                                                                                                                                                                           | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| Voluntary Claim                              | Claim specified by the Client as being useful but not Essential for the specific task requested by the End-User                                                                                                                                                                                                        | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| Issuer                                       | Entity that issues a set of Claims                                                                                                                                                                                                                                                                                     | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| OpenID Provider (OP)                         | OAuth 2.0 Authorization Server that is capable of Authenticating the End-User and providing Claims to a Relying Party about the Authentication event and the End-User                                                                                                                                                  | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| Request Object                               | JWT that contains a set of request parameters as its Claims                                                                                                                                                                                                                                                            | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| Relying Party (RP)                           | OAuth 2.0 Client application requiring End-User Authentication and Claims from an OpenID Provider                                                                                                                                                                                                                      | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| Subject Identifier                           | Locally unique and never reassigned identifier within the Issuer for the End-User, which is intended to be consumed by the Client                                                                                                                                                                                      | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| Authentication Context                       | Information that the Relying Party can require before it makes an entitlement decision with respect to an authentication response. Such context can include, but is not limited to, the actual authentication method used or level of assurance such as ISO/IEC 29115 [ISO29115] entity authentication assurance level | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| Authentication Context Class                 | Set of authentication methods or procedures that are considered to be equivalent to each other in a particular context                                                                                                                                                                                                 | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| Authentication Context Class Reference (acr) | Identifier for an Authentication Context Class                                                                                                                                                                                                                                                                         | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
|                                              |                                                                                                                                                                                                                                                                                                                        | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
|                                              |                                                                                                                                                                                                                                                                                                                        | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
|                                              |                                                                                                                                                                                                                                                                                                                        | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
|                                              |                                                                                                                                                                                                                                                                                                                        | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
|                                              |                                                                                                                                                                                                                                                                                                                        | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
|                                              |                                                                                                                                                                                                                                                                                                                        | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |


## OpenID Connect Native SSO for Mobile Apps [draft](https://openid.net/specs/openid-connect-native-sso-1_0.html)

#### Main flow:

- applies to `authorization code` flow of OAuth.
- a new scope `device_sso` is added. So, when an mobile-app-1(the client) uses a system browser to send authorization code request to `/authorize` endpoint, the request contains the `device_sso` scope.
- In response to this, the `/authorize` endpoint returns a code. AS on the backend knows what scopes are attached to this code.
- When the mobile-app-1 presents the `code` to the token endpoint, the AS looks at attached scopes and notices the `device_sso` scope attached. It sends back an `device_secret` token along with an access token back to the mobile-app-1. From this point onwards, the AS knows that this token has `device_sso` scope attached and an `device_secret` has also been issued, so it expects a `device_secret` to be passed in all future token requests.
- mobile-app-1 stores this `device_secret` in the local mobile storage which can be accessed only by other apps of the same company (e.g: facebook and instagram can access the same storage). So, if there is a mobile-app-2 on the mobile from the same vendor, then mobile-app-2 doesn't have to again to `/authorize` endpoint and reauthenticate the user. Instead, mobile-app-2 can take the client-id, device_secret and id_token and send it to token endpoint to receive an access token and refresh token directly.

  ##### Notes

  - a new `device_secret` is generated by token endpoint when it receives a token request with refresh token and client has `device_sso` scope and an `device_secret` had been issued earlier.
  - Important point from spec:
    ```
    The device secret contains relevant data to the device and the current users authenticated with the device. The device secret is completely opaque to the client and as such the AS MUST adequately protect the value such as using a JWE if the AS is not maintaining state on the backend.
    ```
  - Important point from spec:
    ```
    The exact construction of the device_secret is out of scope for this specification.
    ```
    So how to create `device_secret` is implementation-specific.
  - Important point from spec:
    ```
    If a mobile app requests a device secret via the device_sso scope and a device_secret exists, then the client MUST provide the device_secret on the request to the /token endpoint to exchange code for tokens.
    ```
  - Device secret rotation
    ```
    The client SHOULD provide the device_secret to the /token endpoint during refresh token requests so that the AS may rotate the device_secret as necessary.
    ```
  - Important point from spec
    ```
    If no device_secret is specified and the refresh_token contains the device_sso scope, a new device_secret will be generated.
    ```
  - two values added to the id_token: `ds_hash` and `sid`
  - device_secret validity
    ```
    When the authorization server receives the device_secret it must validate the token. If the token is invalid it must be discarded and the request processed as if no device_secret was specified.
    ```
  - how device_secret is received
    ```
    The device_secret is returned in the device_token claim of the returned JSON data.
    ```
  - In the request to token endpoint:
    ```
    If no devices_secret is specified, then the AS MUST generate the token. If a device_secret is specified and is valid, the AS MAY update the device_secret as necessary. Regardless a device_secret must be returned in the response.
    ```
  - Cross device SSO
  - ID token validation changes
    ```
    Use of the id_token in this specification takes some liberties with id_token validation.
    ```
