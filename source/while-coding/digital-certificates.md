Digital certificates are used by browsers (or any client server communication) to enstablish trust on the other party and to make sure that data received is not tempered with.

So let's understand the basics first. 

🔐 What Is Digital Signing?
- Sender: Signature is basically hash of the message that is encrypted using private key of the signing party. Sender sends (message+signature) to receiver.
- Receiver: Signature verification is basically the process of decrypting the hash using public key of the sender(this means message is coming from the authentic source). 
- Receiver: Message verification is process of matching this hash with the locally derived hash of the message content. If the has match then the message has not been 
tempered with.
- Digital signing is the process of generating a unique proof (signature) that a specific person/entity created a message and that the message has not been altered.

In above, it is most important for the receiver to have the public key of the sender from a trusted source. In case of WEB, the web-browser(receiver) receives the
public key of the sender through the x.509 certificate that the sender shares. 

x.509 certificate is nothing but public key of the sender, with signature of the CA. Again, to ensure that the public key is authentic, and not tempered with,
the browser has to use CA authority's public key to decrypt the CA's signature in the x.509 certificate. 

Browsers come pre-populated with public keys of the world's most of the trusted CAs. So, browser already has the a public key of the CA. 

So here is the sequence.

- Sender creates it's own private and public key pair
- It keeps the private key with itself and gives public key along with other details (company name, domain name for which the cert is required, phone number etc)
  to the CA when requesting for an x.509 certificate
- CA does the background check to verify if the company and the domain are legitimate, and then issues an x.509 certificate. Most important part
  of the certificate is the public key of the sender and signature of CA. Certificate content looks similar
  to below.

  ```
  Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            04:93:2a:1e:bd:77:f3:b1:8c:15:d2:30:11:8c:0f:ac:cc:7b
    Signature Algorithm: sha256WithRSAEncryption
        Issuer: C = US, O = Let's Encrypt, CN = R3
        Validity
            Not Before: Jun  1 00:00:00 2024 GMT
            Not After : Aug 30 23:59:59 2024 GMT
        Subject: CN = www.example.com
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                RSA Public-Key: (2048 bit)
                Modulus:
                    00:b5:af:3b:dc:...:3f:7b
                Exponent: 65537 (0x10001)
        X509v3 extensions:
            X509v3 Basic Constraints:
                CA:FALSE
            X509v3 Key Usage:
                Digital Signature, Key Encipherment
            X509v3 Extended Key Usage:
                TLS Web Server Authentication
            X509v3 Subject Alternative Name:
                DNS:www.example.com, DNS:example.com
    Signature Algorithm: sha256WithRSAEncryption
         a4:5c:cd:3e:...:b6
  ```
  - Sender stores this certificate along with the corresponding private key of it's web server.
  - When any browser requests a web page over HTTPS, a TLS handshake occures before serving the page.
  - In TLS handshake,
    - Browser requests the x.509 certificate of the domain
    - server sends the certificate. Certificate has the name of the certificate issuer.
    - The browser looks up its pre-loaded CA database. If it finds the CAs public key there, then it uses the public key to
      verify the x.509's authenticity by decrypting the signature and obtaining the hash. Then it hashes the public key of the
      sender contained in the certificate to create the hash. If these two hashes match then the certificate is authentic and
      public key of the sender as mentioned in the certificate is also correct.  
    - Now, browser has the authentic public key of the server. Next, the browser creates a random number to be used as a session key. Encrypts it using
      the server's public key. Sends the encrypted session key to the server. Server uses it's the private key to decrypt the session key.
    - Session key is then used to encrypt all future communication between browser and server during that session.

======= more info ==========================================

🔄 The Two Main Steps
🖊️ 1. Signing (Done by Sender)
Input: Message + Private Key
Output: Digital Signature

Steps:

Take the message (e.g. a certificate or document).

Generate a hash of the message (e.g. using SHA-256).
👉 This is a fixed-length fingerprint of the content.

Encrypt the hash using the sender's private key.
👉 This encrypted hash is the digital signature.

Send both: message + digital signature.

Example:

```
Message: "I owe you ₹500"
Hash (SHA-256): abc123...
Signature = Encrypt(hash, Alice's Private Key)
```

✅ 2. Signature Verification (Done by Receiver)
Input: Message + Signature + Public Key
Goal: Verify the message’s origin and integrity

Steps:

Receiver takes the same message and computes the hash (e.g., SHA-256).

Decrypts the digital signature using the sender’s public key to get the original hash.

Compares both hashes:

If they match: ✅ message is authentic and unaltered.

If not: ❌ tampered or invalid signature.

🔍 Why it works:

Only the sender's private key could produce a signature that matches the public key.

Any change to the message changes the hash → verification fails.

### Above process With respect to x.509 CA certificates

- x.509 certificate is in short, your public key(in plain text) with signature of a CA. [here](https://ossdhaval.github.io/mysite/source/while-coding/ssl-ssh-notes.html?highlight=csr#generating-keypair---csr---cert)

Company company1 wants a certificate for their domain domain1 from ca1. 
- 
