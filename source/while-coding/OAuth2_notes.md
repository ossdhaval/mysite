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