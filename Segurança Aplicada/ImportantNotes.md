# Important Notes



# Phases IEEE 802.11i

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
  5. Now both send messages to one another staring with the AP then station confirming they have the correct key
- Outside of this the AP will create a GTK(Group Temporal Key) which it will send to the station with a MIC, using the KEK (Key Encryption Key)
- The station will respond to acknowledge the GTK 

Sending Data

Connection termination

# TKIP

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