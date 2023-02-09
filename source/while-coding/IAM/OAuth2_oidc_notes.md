# OAuth 2.0 and OpenID Connect


- [OAuth 2](#oauth-2)
- [OpenID connect](#openid-connect)
- [OAuth and OpenId Connect]
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

for more understanding : https://medium.com/@robert.broeckelmann/openid-connect-logout-eccc73df758f

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



## Dynamic Client Registration ([RFC 7591](https://datatracker.ietf.org/doc/html/rfc7591)) notes:

Registration requests send with a set of desired client metadata values to the authorization
   server.  The resulting registration responses return a client
   identifier to use at the authorization server and the client metadata
   values registered for the client.
   
   There are two separate SPECs for dynamic client registration. One from [OAuth](https://datatracker.ietf.org/doc/html/rfc7591) and another from [openid connect](https://openid.net/specs/openid-connect-registration-1_0.html). Both must be complimenting  each other somehow.
   
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

## Software Statement

- Defining Software statements: https://www.rfc-editor.org/rfc/rfc7591#section-2.3
- Software statement can be signed by organization that is developing the client or a third party.

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

- Software statement Vs Software Statement Assertions (SSA), are these to different?

  Yes, Excerpt from [here](https://docs.jans.io/v1.0.6/admin/auth-server/endpoints/client-registration/#5-special-mention-about-fapi)
  
  ```
  In case of a typical client registration request in FAPI implementation, the request object which is a signed JWT (as seen in point 3) is also called     an SSA (Software statement Assertion) or DCR payload. This SSA can contain the software_statement inside it which is also a signed JWT. Each of the       JWTs, the outer JWT called the SSA and the inner JWT called the software_statement are signed by different entities - the TPP and OBIE respectively.
  ```

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

| Term                 | definition                                                                                                                                                            | source                                                                               | example |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|---------|
| Identity             | Set of attributes related to an Entity                                                                                                                                | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| Entity               | Something that has a separate and distinct existence and that can be identified in a context. An End-User is one example of an Entity.                                | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| Authentication       | Process used to achieve sufficient confidence in the binding between the Entity and the presented Identity                                                            | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| Claim                | Piece of information asserted about an Entity                                                                                                                         | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| Claims Provider      | Server that can return Claims about an Entity                                                                                                                         | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| Essential Claim      | Claim specified by the Client as being necessary to ensure a smooth authorization experience for the specific task requested by the End-User                          | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| Voluntary Claim      | Claim specified by the Client as being useful but not Essential for the specific task requested by the End-User                                                       | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| Issuer               | Entity that issues a set of Claims                                                                                                                                    | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| OpenID Provider (OP) | OAuth 2.0 Authorization Server that is capable of Authenticating the End-User and providing Claims to a Relying Party about the Authentication event and the End-User | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| Request Object       | JWT that contains a set of request parameters as its Claims                                                                                                           | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| Relying Party (RP)   | OAuth 2.0 Client application requiring End-User Authentication and Claims from an OpenID Provider                                                                     | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
| Subject Identifier   | Locally unique and never reassigned identifier within the Issuer for the End-User, which is intended to be consumed by the Client                                     | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
|                      |                                                                                                                                                                       | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
|                      |                                                                                                                                                                       | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
|                      |                                                                                                                                                                       | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
|                      |                                                                                                                                                                       | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
|                      |                                                                                                                                                                       | [OIDC Spec terms](https://openid.net/specs/openid-connect-core-1_0.html#Terminology) |         |
