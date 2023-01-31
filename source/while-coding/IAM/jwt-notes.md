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
  - So, the party on the other side, should be able to derive the same signature if it has the secret key. If the other party can do it successfully,
    is sure about one thing.
    - No body has tempered with the data
  - the secret key can be a shared secret between client and the server, or it can be done using private key/public key pair. 
  - In the key pair scenario, 
    - one party can give the public key to the other party
    - then use private key to create signature and create JWT with it
    - other party can use the public key to generate the same signature using public key
  - Remember, the signature is not for hiding the data (encryption), or authentication mechanism. It is for checking integrity of the data. i.e If someone steals JWT from my request, that person can easily impersonate me.
- Three parts of JWT are separated by periods
- Use [debugger at jwt.io](jwt.io) to see what is in the JWT

## Notes:

- JWT is not an authentication mechanism, it comes into picture after trust has been established (may be via authentication or in some other way)
- Relation between `pem` and `jwks`: https://community.auth0.com/t/jwk-vs-pem-what-is-the-difference/61927

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

