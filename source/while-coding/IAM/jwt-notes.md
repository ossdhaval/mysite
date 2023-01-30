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
    is sure about two things.
    - No body has tempered with the data
    - the sender is the actual trusted user
  - the secret key can be a shared secret between client and the server, or it can be done using private key/public key pair. 
  - In the key pair scenario, 
    - one party can give the public key to the other party
    - then use private key to create signature and create JWT with it
    - other party can use the public key to generate the same signature using public key
  - Remember, the signature is not for hiding the data (encryption), rather it is for authenticity of data and the sending party
- they are separated by periods
- Use [debugger at jwt.io](jwt.io) to see what is in the JWT
- 
