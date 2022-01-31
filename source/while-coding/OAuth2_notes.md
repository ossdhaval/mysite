## OAuth 2.0 ([RFC6749](https://datatracker.ietf.org/doc/html/rfc6749))


### Grant types:
1) Authorization code
  - Uses an authorization server
  - benefit: protects access code by not sharing it with user agent and uses authorization code to do that
  - benefit: also authenticates client when it requests access code using authorization code
  - downside: more round trips than implicit flow
  - Authorization code -> access code -> 
2) Implicit
  - used by client application that are built in scripting languages
  - it doesn't use authorization code and directly gives out access token to user-agent
  - benefit: more efficient than `authorization code` grant type as there are less roundtrips
  - downside: less secure as access code is shared with user-agent
3) Password credentials
  - resource owner gives user-id/password credentials to client application once and client app uses these 
    credentials to get a long-lived access token
  - client doesn't store resource owner credentials once it has an access token or refresh token
  - benefit: simplified workflown when dealing with a trusted client
  - downside: very insecure as client gets the credentials
4) Client credentials
  - client acts on its own to access resources from resource server which are owned by client 
    itself. i.e. when client is the resource owner
  
### access token

  - Access token is created by authorization server, given to client to access resources on resource server.
  - Access token is opaque to client.
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
