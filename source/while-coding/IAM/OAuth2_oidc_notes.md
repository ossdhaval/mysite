# OAuth 2.0 and OpenID Connect


- [OAuth 2](#oauth-2)
- [OpenID connect](#openid-connect)
- [all flows](#all-flows)
- [Important terms](#important-terms)

## OAuth 2 

([RFC6749](https://datatracker.ietf.org/doc/html/rfc6749))


### Grant types:

What is `Grant` in `grant type` : Basically, these are different ways of getting Granted an access token. All grant types has only one aim: to get access token. Because of different types of clients (confidential(backend) vs Public(SPA, mobile phone and desktop based native apps)) have different capabilities of protecting access tokens, there are different grant types.

1) Authorization code
  - Uses an authorization server
  - benefit: protects access code by not sharing it with user agent and uses authorization code to do that
  - benefit: also authenticates client when it requests access code using authorization code
  - downside: more round trips than implicit flow
  - Authorization code -> access code -> 
  
2) Implicit (this is now deprecated and replaced by Authorization code with PKCE)
  - used by client application that are built in scripting languages
  - it doesn't use authorization code and directly gives out access token to user-agent
  - benefit: more efficient than `authorization code` grant type as there are less roundtrips
  - downside: less secure as access code is shared with user-agent
  
3) Password credentials (deprecated - only used for if client app is trusted app. use auth code grant with pkce)
  - resource owner gives user-id/password credentials to client application once and client app uses these 
    credentials to get a long-lived access token
  - client doesn't store resource owner credentials once it has an access token or refresh token
  - benefit: simplified workflown when dealing with a trusted client
  - downside: very insecure as client gets the credentials
  
4) Client credentials
  - client acts on its own to access resources from resource server which are owned by client 
    itself. i.e. when client is the resource owner
  
5) Refresh token:
  - This grant type is used when request is sent to token endpoint, with request parameter `grant_type=refresh_token` and refresh token, to get a new access token. 
    refer: https://www.oauth.com/oauth2-servers/making-authenticated-requests/refreshing-an-access-token/#:~:text=To%20use%20the%20refresh%20token,the%20client%20credentials%20if%20required.
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


## Client Registration

### What is `client` in OAuth Vs OIDC
- `client` in OAuth is not the same as in OIDC. 
  - In OIDC, `client` is a server(called relying party) that wants to protect resources on resource server (RS) using authentication
  - In OAuth, `client` is a third party app server which wants to access resources in RP/RS


## Dynamic Client Registration ([RFC 7591](https://datatracker.ietf.org/doc/html/rfc7591)) notes:

Registration requests send with a set of desired client metadata values to the authorization
   server.  The resulting registration responses return a client
   identifier to use at the authorization server and the client metadata
   values registered for the client.
   
   There are two separate SPECs for dynamic client registration. One from [OAuth](https://datatracker.ietf.org/doc/html/rfc7591) and another from [openid connect](https://openid.net/specs/openid-connect-registration-1_0.html). Both must be complimenting  each other somehow.
   
## other references
- https://github.com/zmartzone/mod_auth_openidc/blob/master/auth_openidc.conf
- https://curity.io/resources/learn/openid-connect-understanding-dcr/
- https://curity.io/resources/learn/using-dynamic-client-registration/
- https://www.youtube.com/watch?v=AsCL8kMU1iY
- https://www.youtube.com/watch?v=WnI32e4eEuY
- https://connect2id.com/products/server/docs/api/client-registration#initial-access
- Very good link to understand issueing of tokens https://darutk.medium.com/diagrams-of-all-the-openid-connect-flows-6968e3990660

### about client registration in OAuth and OIDC
- `client` registration is done by different partys
  - `client` is a third party which wants to resources in RP. So, this client has to register with OP
  - In OIDC, `client` is `relying party`(which may be a reverse proxy that is trying secure the RS)


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

