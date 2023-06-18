# Important Notes

# Symmetric Encryption

4 types of transformation
- Substitution
- Transposition
- Product
- Feistel Cipher

AES Modes
- ECB - Electronic CodeBook (penguin)
- CBC - Cipher Block Chaining
- CFB - Cipher FeedBack
- OFB - Output FeedBack
- CTR - Counter

Random Number Generator

Types:
- True RNG
- PseudoRandom RNG
- PseudoRandom Function

Requirements:
- Uniformity
- Scalability
- Consistency
- Forwards Unpredictability
- Backwards Unpredictability


# Asymmetric Encryption and Hash Functions

Diffie Hellman Key Exchange:
- Global Vars
  1. Prime number p
  2. Primitive root a
- User A
  1. Generate $X_A<p$
  2. Calculate $Y_A = a^{X_A}mod\;p$
  3. Send $Y_A$ to the other side
- User B
  1. Generate $X_B<p$
  2. Calculate $Y_B = a^{X_B}mod\;p$
  3. Calculate $K = Y_A^{X_B}mod\;p$
  4. Send $Y_B$
- User A
  1. Calculate $K = Y_B^{X_A}mod\;p$


SHA512:
- Message with padding is divided into N blocks
- Each of the blocks then passes through a Function F
- Then the output is XORed with the previous block, and the first is XORed with an IV
- The output will be the result of the last block with 512 bits 


The purpose of MAC's is to ensure that a certain message comes from the correct sender, has not been tampered and the data is not harmful.

HMAC 
- Compute once
  - Key+ = key + 0's until a size b
  - SI = Key+ XOR ipad
  - n bits2 = SI + IV
  - SI = Key+ XOR opad
  - n bits1 = SI + IV
- Compute for each message
  - HASH(message,n bits1)
  - pad to b bits
  - HASH(b bits,n bits2)
  - pad to b bits
  - Output = HMAC(message, key)

The probability of attack in HMAC is the same as embedded hash function:
- The attacker guess a result for a message even with random IV
- The attacker finds a collision for a message even with random IV

# Authentication and Key Distribution

Types of authentication
- Unilateral Authentication
  1. Use password
  2. Use machine address
- Unilateral Authentication with shared secret
  1. Use challenge, bob sends challenge for alice to encrypt
  2. Use challenge, bob sends challenge for alice to decrypt
  3. Use single message with encoded timestamp
  4. Use single message with name + timestamp + hash(sharedKey,timestamp)
- Mutual Authentication
  1. 5 message variation
  2. 3 message variation (vulnerable to reflection attack if challenge is the similar)
  3. Use timestamp as challenge
  4. Use public key instead of symmetric
- Mediated Authentication
  1. Ticket sent to Bob directly (Ticket=$E_{KB}(SessionKey, ID_A)$)
  2. Ticket sent to alice encrypted, for alice to send to bob

# Authentication Protocols

PFS (Perfect Forwards Secrecy) means an algorithm where even if an attacker is able to:
- Decrypt both parties long time secrets
- Record the entire conversation

It can't get access to the information in the conversation

It can be achieved by deriving the key from local information, and said key is forgotten periodically

DOS Protection can be achieved in 2 main ways
- Cookies - The protocol only continues after the user echos the cookie sent by the server
- Puzzles - The protocol only continues after the user responds with the solution to the puzzle

In both situations, we are defending the server by making the users need to do more computation to access our services

Identity Hiding, the objective will be to hide the identity of the two pears from an adversary we can do this with an anonymous diffie hellman, were we setup a key and after that we send our identity.

Live partner reassurance, the objective is to counter replay attack this can be done by requiring the partner to use a key based on a nonce created in server side.

Parallel computation, given that Diffie Hellman is slow we can use parallel computation to make both side calculate the key at the same time, and make it so that the client doesn't have to wait for the server to calculate the entire key before receiving $Y_B$

# Kerberos

Protocol:
- Client -> AS     : Request Ticket for TGT 
- AS -> Client     : Session key for TGS and Ticket for TGT
- Client -> TGT    : Request Ticket for Service
- TGT -> Client    : Session key for S and Ticket for S
- Client -> Server : Request Service
- Server -> Client : Authenticator

# IEEE

## Phases IEEE 802.11i

Discovery:
- Probe - Used to define security parameters
- Authentication Request - Used for backward compatibility with WEP
- Association Connection - Used to setup connection with AP with defined security parameters

Authentication:
- EAP (Extensible Authentication protocol) - Station <-> AP
- Access Request - AP <-> Authentication Station
- EAP success - Station <- AP

Key Management:
- Creates Keys for the station
- Both sides have 4 things
  1. PMK (Pair Wise Master Key)
  2. ANonce (Authentication nonce)
  3. SNonce 
  4. Both Mac Addresses
- Uses 4 way handshake
  1. AP sends ANonce
  2. With ANonce, the AP Mac and PMK the station can derive a PTK
  3. User sends SNonce with MIC (Message Integrity Code) using the PTK
  4. Now the AP can derive the PTK and verify it with the MIC
  5. Now both send messages to one another starting with the AP then station confirming they have the correct key
- Outside of this the AP will create a GTK(Group Temporal Key) which it will send to the station with a MIC, using the KEK (Key Encryption Key)
- The station will respond to acknowledge the GTK 

Sending Data

Connection termination

## TKIP

Combines 2 things to convert plain text into ciphertext:
- Fragment Frame which is result of:
  1. Integrity Algorithm which is made of:
   - MIC key
   - Station MAC + Destination MAC + priority bits
   - Sequence Counter
  2. Plaintext
- RC4 encryption of Temporal key mixing which is made of:
  1. Temporal Key (PTK)
  2. Station MAC
  3. Sequence Counter

These 2 are XORed to compose the ciphertext, with an IV coming from RC4.


# RFID

Types:
- Active
- Passive
- Battery powered passive

Protocols:

Zero Knowledge:
- Reader->Tag : Counter, (SessionKey XOR HASH(Counter,SharedSecret)),Hash(SessionKey,SharedSecret)
- Tag->Reader : HASH(SessionKey,SharedSecret,Counter)

Basic Access Control Protocol
- Reader->Tag: Get Challenge
- Tag->Reader: Generate N1 and send
- Reader->Tag: Generate K2 and N2, sends $E_{KE}$(N1,N2,K2),$MAC_{KM}$
- Tag->Reader: Generate K1, sends $E_{KE}$(N2,N1,K1),$MAC_{KM}$
- Both get K = K1 XOR K2

# IPSec

Modes:
- Transport - Secures data from protocols above IP
- Tunnel - Secures the whole IP packet

Services:  
1. Authentication Header
2. Encapsulating Security Payload Header
3. Encapsulating Security Payload Header with Authentication 

Security Association Database as Security Associations which are defined:
- Security Parameter Index: 32bit meaning the receiver
- Destination IP address
- Security Protocol Identifier

SA Database stores:
- Sequence counter
- used algorithms for encryption and authentication
- SA lifetime
- protocol mode

Security Policy Database defines what SA needs to be used for a certain packet defined by:
- Destination IP address
- Source IP address
- Transport protocol
- username for OS
- source and dest ports

Advantages of IKE over DH:
- Uses cookies to counter DOS
- Uses nonces to counter replay attacks
- Uses authenticated messages to counter MITM attack


# SSL/TLS

Certificate Format:
- Serial Number
- Issuer Name
- Subject Name
- Issuer Identifier
- Extensions
- Digital Signature

TLS provides secure channel if communication is reliable and can be in-order.
It assures: 
- C(Confidentiality) - Data encryption + padding
- I(Integrity) - Changes to data are detected
- A(Authentication) - Server always authenticated, client is optional

These properties should be true even if an attacker has full control of the network

## TLS1.3

2 protocols:
- Handshake
- Record

Record protocol is used to fragment messages, uses AEAD to encrypt fragments and transmits the result

Handshake protocol
- Phase 1 Key exchange - Both sides say hello and send version, random and cipher suite. In addition can send key material if it has been established before
- Phase 2 Server Parameters - Both messages sent from Server to Client
  1. Encrypted Extensions - Further parameters not sent in the Client hello
  2. Certificate Request - If the client wants to authenticate it requests his certificates
- Phase 3 Authentication - Both sides send 3 messages
  1. Certificate - Sends the 500X certificate
  2. Certificate Verify - Sends the signature over all the messages sent during the entire handshake
  3. Finished - Sends the MAC of all the messages sent during the entire handshake

2 Additional operation modes:
- Resumption - The server can send a PSK identity which the client can use in future handshakes to negotiate the handshake
- 0-RTT data - Allows the client to send data in first flight before the handshake is completed, it is only possible when a PSK already exists.

# Secure Email

Email services are composed of:
- MUA - Mail User Agent
- MTA - Mail Transport Agent
- MSA - Mail Submission Agent
- MDA - Mail Delivery Agent

Mail goes: MUA -> MSA -> MTA -> MTA -> MDA -> MUA

We need to guarantee:
- Confidentiality - 
  1. Locally we use message encryption with symmetric or public key
  2. Remote we need to have multiple keys between list and users (if using public key), the other way is simple
- Authentication - 
  - Locally
   1. Using public key create a hash of the message and encrypt with private key of sender
   2. Using symmetric key create a hash of the message with shared key
  - Remote
   1. Simple with public key, uses the same as locally
   2. Using symmetric we need to have a key with each receiver 
- Integrity - 
  1. Symmetric key - It is hard or impossible to do
  2. Public key - We can use hashes to assure we are getting the correct message, we ned to be careful with the hash and the message being substituted

## MIME

MIME solves some problems with RFC 5322(successor to SMTP):
- More characters like latin
- Messages with more types
- No more servers truncating sizes

SPF - Reduce fishing and spamming

DKIM - Allows domain to take responsibility over email by signing them

DMARC - More feedback mechanism, allows users to know what to do in case of attack

STARTLS - Allows usage of TLS for the connections in the email service

SMIME main goal is to allow users to assert they are the sender of an email

4 methods are allowed:
- Envelope message
- Sign message
- Clear sign message
- Envelope and sign message

To decide on a cryptographic algorithm the sender:
- Receives a list of algorithms in an order
- If no list is received but some messages were already sent, then it should continue with the same algorithm
- If both above are false, then use Triple DES 