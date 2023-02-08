# JWT Notes

- JSON + sign = JWT
- JWT is value token (as opposed to session tokens which are reference tokens)
- 

## Structure

- has 3 parts `part1.part2.part3`
- `part1` is header
  - this is base64 encoded
  - Base64 encoding is just to make data easier to transport over the web. Without any special characters etc.
  - header contains info like type (`typ`) of token and algorithm(`alg`) used for signature
- `part2` is payload 
  - is the actual data that is base64 encoded. And it can be easily decoded to get actual data without any key etc
- `part3` is signature
  - signature = Algo(encoded header, encoded payload, secret key)
  - So the signature is not just a simple hash of encoded header and encoded payload. It is a hash done with a secret key. Hence, if the header or the payload has changed or if you don't have the same secret key (or private-public key), they same signature can not be generated.
- Three parts of JWT are separated by periods
- Usage: 
  - Message integrity: JWT signature verification ensures that data in the header and payload has not been tempered with.
  - Authentication: 
    - You can ensure that the JWT was actually signed by you yourself. For example, JWT access token was indeed issued by itself because it can varify the signature using the same secret it has.
    - You can ensure that JWT is coming from an trusted party. For example, a client can share JWKS(i.e public keys) with server during registration, then send JWT by signing it using its private key. When server receives JWT, it can verify signature using public keys and be sure that JWT was indeed sent by the intended client.
- Use [debugger at jwt.io](jwt.io) to see what is in the JWT

## Notes:

- JWT is not an authentication mechanism, it comes into picture after trust has been established (may be via authentication or in some other way)
- Relation between `pem` and `jwks`: https://community.auth0.com/t/jwk-vs-pem-what-is-the-difference/61927
- Good article: https://www.pingidentity.com/en/resources/blog/post/jwt-security-nobody-talks-about.html

## Creating JWT using command-line

- Create a private key

    ```shell
    openssl genrsa -out private-key.pem 2048
    ```

- Extract public key from private key

    ```shell
    openssl rsa -in private-key.pem -pubout -outform PEM -out public-key.pem
    ```

    During the client registration or via client configuration settings, the public key generated above should be attached
    to the client on authorization server.

- Create header payload. For example,

    ```json
    {
    "alg": "RS256",
    "typ": "JWT"
    }
    ```

    To create JWT we need header in base64 encoded format. Use commands below and to convert header in base64 encoded string:
  
    ```shell
    echo -n 'header-json' | base64 | sed s/\+/-/ | sed -E s/=+$//
    ```

- Create your JWT payload. For example,

    ```json
    {
    "jti":"myJWTId001",
    "sub":"38174623762",
    "iss":"38174623762",
    "aud":"http://localhost:4000/api/auth/token/direct/24523138205",
    "exp":1536165540,
    "iat":1536132708
    }
    ```

    To create JWT we need the payload in base64 encoded format. Use commands below and to convert the payload in base64 
    encoded string:
  
    ```shell
    echo -n 'payload-json' | base64 | sed s/\+/-/ | sed -E s/=+$//
    ```

- Use the encoded header and payload to create the signature. The signature would be in form of an encoded string.

    ```shell
    echo -n "encoded-header.encoded-payload" | openssl dgst -sha256 -binary -sign jwtRSA256-private.pem  | openssl enc -base64 | tr -d '\n=' | tr -- '+/' '-_'
    ```

- Put together encoded strings for header, payload and signature in format below to completely form JWT.

    ```json
    encoded-header.encoded-payload.encoded-signature
    ```

- Use this JWT in request to the server. As mentioned earlier, the server must have public key registered as part of 
  the client registration process in order to verify the JWT in the request.

## JWT JWS and JWE

JWS and JWE are types or methods of creating JWTs. All of them have different specifications: [JWT](https://www.rfc-editor.org/rfc/rfc7519), [JWS](https://www.rfc-editor.org/rfc/rfc7515), [JWE](https://www.rfc-editor.org/rfc/rfc7516).

JWT can be of three types (there is nothing like plain vanila JWT). Unsecured, JWS or JWE

- Unsecured JWT. Structure here, there are two dots but third part is missing:
  
  ```
  h3k4h5345k34j.34k5j3k4jrlkafi.
  ```
  
- JWS 
  - `JWS Compact Serialization`: Structure has two dots and all three parts, as specified [here](https://www.rfc-editor.org/rfc/rfc7515#section-3.1). The most widely used representation of JWT.
    
    ```
    h3k4h5345k34j.34k5j3k4jrlkafi.k43jkj34jdfhw
    ```
  - `JWS JSON Serialization`: Structure here is like a JSON. As specified [here](https://www.rfc-editor.org/rfc/rfc7515#section-7.2.1). And it looks like:
  
    ```
    {
      "payload":"<payload contents>",
      "signatures":[
       {"protected":"<integrity-protected header 1 contents>",
        "header":<non-integrity-protected header 1 contents>,
        "signature":"<signature 1 contents>"},
       ...
       {"protected":"<integrity-protected header N contents>",
        "header":<non-integrity-protected header N contents>,
        "signature":"<signature N contents>"}]
    }
    ```
  - `Flattened JWS JSON Serialization`: Structure here is like a JSON. As specified [here](https://www.rfc-editor.org/rfc/rfc7515#section-7.2.2). And it looks like:
  
    ```
    {
      "payload":"<payload contents>",
      "protected":"<integrity-protected header contents>",
      "header":<non-integrity-protected header contents>,
      "signature":"<signature contents>"
     }
    ```
    
- JWE
   
   **TBD**
