## Why do we need security?
- Privacy - so that no one can read the data you send
- Integrity - so that no one can change the data you send (man-in-the-middle attack)
- Identification - so that you know who you're exchanging data with.  SSL certificates
## Encryption
### symmetric keys
1. Sender encrypts message with an encryption algorithm. The key is part of that algorithm.
2. Key is shared with recipient.
3. Recipient knows the algorithm and the key, making it easy to decode the message.
**Problem**: Anyone who has public key can decode message. How do I share the key with recipient safely? I can't encode it...

### asymmetric keys
1. Private key is used to generate public key using an algorithm. 
	- The algorithm is such that knowing the private key, the public key can be computed, but the reverse doesn't hold- knowing the public key doesn't help in computing the private key. 
	- Another mathematical quality of the algorithm is that messages encoded with the public key can be decoded only with the private key.
2. Public key can be widely shared as it won't decrypt any messages.
3. Sender encodes message with recipient's public key.
4. Recipient decodes it with their own private key. 

## SSL/TLS Handshake

```
CLIENT                         SERVER
  |                               |
  | ------- ClientHello --------> | C sends list of TSL versions and cipher suite
  |                               | 
  | <----- ServerHello  --------- | S sends: 
  |                               | - chosen encryption algorithm from the cipher 
  |                               | suite.
  |                               | - chosen TSL version
  |                               | - certificate with assymetric public key
  |                               |
  | ---- ClientKeyExchange -----> | C sends symmetric pre-master key encrypted 
  |                               | with S's public key
  |                               | 
  | ----------------------------> | C and S send each other Finished message     
  |         Finished              | encyrpted with symmetric session keys
  | <---------------------------- | generated from pre-master key. If both decrypt 
  |                               | it succesfully, connection is established. 
```

**NB**: SSL (Secure Sockets Layer) is the name of an older version of TLS (Transport Layer Security)

## Public Key Infrastructure
- **Root certificates** Every browser, operating system, email client etc. maintains a *root store* of certificates signed by trusted Certifying Authorities. Each CA self-signs their certificate with their private key and anyone can validate their signature using their public key. 
- **Intermediate certificates** CA's use their private key to also sign intermediate certificate. This links the intermediate certificate to the root one. 
- **end-entity (leaf) certificates** Intermediate certificate's private key is used to sign end-entity certificate. This links end-entity certificate to intermediate certificate.
- **chain of trust** the browser trusts the end-entity certificate because it is linked to an intermediate certificate. It trusts intermediate one because it is linked to root certificate. And website's root certificate is trusted because it is found in browser's own root store. 

**NB**: The usage of public and private keys is different to that in SSL/TSL handshake. In the handshake, each side encrypts the message with the other side's public key, so that only the other side can decrypt it (with their private key). In PKI, the certificate is not encrypted, but signed. The signing is done with issuer's private key, not receiver's public key. The signature can be validated by anyone with the issuer's public key, and not only by the receiver with their private key.
### Three kinds of certificates
- **Domain validation** - the CA asks the owner of the domain to confirm their ownership, e.g. by uploading something to the website. This does not include checking the owner's identity. The check simply establishes *whether the person who applied for the certificate is the person who in fact owns the website*. It offers some protection over a self-signed certificate but not much. 
- **Organisation validation** - the CA performs the same ownership check as in DV. In addition, they confirm: the organisation's existence by checking government business registry; their address by checking against business directories, official documents etc.; their telephone by calling them; and the identity of the requestor (e.g. Steve from IT) by confirming employment status.
- **Extended validation** - reserved for very high-trust organisations, e.g. financial institutions or e-commerce platforms. Checks the same things as OV, but in more stringent way. For example, in OV the CA may verify that the org is registered at the address they claim to be. In EV, the CA may check if the org actually operates from that address by checking utility bills and such. In addition, EV may check the org's incorporation status (e.g. an LLC) and it's standing with authorities (e.g. if it's been paying taxes).
