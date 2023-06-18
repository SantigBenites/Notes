# Consider the various cryptographic algorithms that you studied:

## Imagine an implementation of an encryption algorithm that uses 64-bit keys. Since this key size is considered insecure against brute force attacks, it was decided that messages should be encrypted twice with (two) distinct keys. Discuss the advantages and limitations of this approach. By how much was security improved with this solution?

Obvisously some level of security is added with this step, taken that into consideration the level.

This type of approach can be seen in usage in some older algorithm like DoubleDES and TripleDES.

Taking this into account, while the level of security is higher by using two distinct keys, it would be better if we just made the size of the original key 128 or even 256 bits, while this approach would have effects on efficiency, the security provided by longer keys is better then the security provided by doubling the number of encryption steps.

Taken this into consideration 2 encryption steps could also have an influence in efficiency given, depending on the hardware, encryption could be computationally taxing.

## As you know, the Diffie-Hellman (DH) key exchange algorithm is vulnerable to man-in-the-middle attacks. Explain how this attack works, and then present an enhancement to the algorithm to prevent this sort of attack

In a MITM attack the attacker positions it self between the client and the server trying to execute the DH algorithm.

The attacker goal will be to establish a DH key with both sides of the connection will pretending to the other side.

Its goal will be to decrypt the messages sent from the client with the key it established with the client and the proxy them to the server, and do the same thing the other way around.

To this effect, given the attacker will have the messages sent by the client in plaintext it can not only violate confidentiality but also integrity.

A good method to prevent this type of attack would be to sign messages sent from both the client and the server with their public keys giving DH the authentication property.

Another approach would be to use an algorithm like Elgamal or Ephemeral Diffie Hellman, that while doesn't prevent the MITM completely protects some parts of the connection mostly previous messages that could be using the same key in a normal DH.

# You are the person responsible for the authentication service of your company

## Imagine that all machines have their clocks approximately synchronized and that users/services have their own private/public keys. Can you present an authentication mechanism that takes advantage of these characteristics? Discuss if your solution prevents replay attacks.

We could use timestamps given we have all our clocks approximately synchronized, and given we have private/public keys for our services/users we can use them to sign these timestamps therefore protecting them from tampering. To assure authentication, give we are using private/public keys the authentication property is self evident given only the person with the correct private key will be able to "decrypt" our signature.

This approach can defend against replay attack, but a fast enough attacker can take advantage of a misconfigured timeout on our timestamps to execute a replay attack. Therefore proper configuration of our timestamps timeout would be required.

## In some sense, Kerberos V4 also explores some of the characteristics of the previous question. Start by explaining generically how Kerberos V4 works (main components and message exchanges), and then describe two fundamental aspects where Kerberos is different from your solution

The Kerberos system is composed of 3 members other than the user.

The authentication service:

The authentication service receives from the user a message requesting access to the server, it will send the ID of the Ticket granting Service a nonce and a timestamp.

The server will respond with, a ticket for access to the Ticket Granting Service (which will contain the ID of the server inside encrypted, a timestamp, and the key for communication between the TGS and user), the IP of the ticket granting service 

The Ticket Granting service

The Ticket Granting service receives from the user, the ticket given to him by the authentication service, the ID of the server, the timestamp, a nonce and an authenticator

The Ticket Granting service will respond with a Ticket for the server (which will contain the key for the communication between the Server and user, a nonce, a timestamp and the ID of server)

The server

The server will receive from the user the ticket given to him by the TGS and the authenticator

An receive a key for communication, a timestamp and a sequence number

As we can see both systems make usage of encrypted/signed timestamps in their communication. 

The main difference stands from 2 factors, Kerberos uses symmetric encryption while our system would use public/private key.

And kerberos makes usage of 2 more entities than we used in our example, given that in the original case we didn't have usage (or it was over-engineering to use) for either the Ticket Granting service or the authentication service.

# Imagine that some company embeds a RFID tags in each box of pens that it produces. These tags are passive, and carry an identifier plus a symmetric key in read-only memory, plus some writable memory space. The symmetric key is the same for all boxes. When the box arrives to a store, some optional exchange occurs between the box and the reader system. While in the store, the box periodically exchanges information with the reader system, for instance to detect if it has been stolen. When the box is bought by someone, there is another optional exchange with the reader system for example to update the inventory of the store.

## Different organizations have raised several concerns about the use of RFID tags in consumer goods, like a box o pens. Discuss a potential attack against privacy that could occur with someone that buys a box of pens in the scenario presented above.

Given the nature of RFID in this situation, we are only informed that when a box of pens is bought the RFID tag is only used to update the stock of the store.

With this in mind we can assume that no effort is made to clear the data in the RFID tag, that being said anyone with a reader can send a signal which will be picked up by the RFID tag and get access to the information in the tag.

Therefore an attack against security could be made, where an attacker could use a reader to access the RFID tag and know information stored inside the tag, this information can go from menial like the type of pen the box contains to sensitive if the credit card number is put on the tag post purchase.

Another attack could consist in using the information in the tag to create customer profiles against the users consent by a less ethical shop, given that it could use the reader to detect what kind of purchases an individual has previously made and targe the customer accordingly.

Either way their privacy would be compromised.

## Propose a protocol for the exchange between the box and reader system, which prevents the privacy problem from the previous question. Explain why your solution solves the problem.

A way to prevent an external attacker from exploiting the RFID tag in the box by using a protocol to encrypt the data in the tag. This would prevent future readers from being able to exploit it given the data inside it can't be accessed without knowledge of the key.

With this in mind, this doesn't prevent the second attack given that by encrypting the data we effectively created a new identifier that only the reader that create the encryption knows.

A way to defend against the second attack would be to remove the RFID tag or its data entirely post purchase.

# Consider a scenario where an outside host wants to communicate securely with a machine inside a private network. The private network is protected at the perimeter with a firewall/router. All machines implement the IPsec protocol.

## The IPsec protocol defines a Security Policy Database (SPD). Explain the role of the SPD, and give as example of one possible way to setup this database at the Firewall (taking into consideration the scenario above).

The SPD is used in combination with SAD (Secure Association Database) to define the protocol for a certain Secure Association.

The SPD will define a certain protocol for a certain type of packet from coming from sourceAddress:sourcePort to destinationAddress:destinationPort. This will define if for said connection we will be using either AH or ESP.

A possible way to define a firewall in this situation would to define that packets of type HTTP coming from outside host to inside host need to have protocol ESP + AH.

This would then be used by the SAD to define an association for receiver Inside host.

## IPsec can be employed in different ways to secure the communication flows between the machine inside the private network and the outside host. Two possible solutions are: (i) transport adjacency end to end, with AH followed by ESP; and (ii) transport AH end to end, followed by an ESP tunnel between the outside host and the firewall. Assuming that attackers are in the exterior of the private network, compare in detail the two alternatives (e.g., in relation to security and performance impact). Justify your conclusions.

The main difference in this situation would be the usage of a tunnel in the ESP step.

With this in mind we must understand the difference between using transport mode and tunnel mode.

In transport mode, we are encrypting the packet data above the IP layer, while in tunnel we protect the whole IP packet.

To this effect given we know that the attack is located outside the private network we must understand whether or not we want to defend the entire packet.

Given the attacker can use the IP layers data as part of the attack vector we should probably use the tunnel mode and protect all the data given to us at the IP level.

With this in mind, we must understand that it is possible to attack ESP in tunnel mode by injecting traffic to create specific ICMP errors, and use the time and order of the processing of the headers of IP dataGrams to guess the fields. 

#  Imagine that your organization uses SSL to protect the communication to the email server. The email server has a RSA certificate. 1) Explain how the client authenticates the server. 2) Is this authentication enough to ensure the security of the email service? Justify.

1

Given we have a RSA certificate we can assume we have a pair public/private key.

So if we want to communicate the message from the email server to the client, we can use the private key of the server to sign the message, this will allow the client to use the public key to verify the signature and in so verify the message trully came from the server.

Guarantying authentication.

2

Authentication is not enough to guarantee security in this situation, it would be possible for anyone in the previous situation to have access to the information in the message given the public key is accessible by anyone.

With this in mind a more robust protocol, would be to send the contents of the message encrypted with the public key of the recipient, therefore only allowing the holder of the private key to decrypt the message which we know would only be the recipient. And in order to verify confirm authenticity we should send a hash of the message signed with the private key of the sender, this allowing us to verify the message we are receiving came from the expected sender.

With all of this we prevent the attack referenced above, and more over can confirm the integrity property by adding an hash that the receiver can confirm to be correct.

# One of the important advantages of S/MIME is that it can be integrated with existing standards like SMTP and MIME. Explain how this integration was accomplished, and describe the way S/MIME ensures the non-repudiation of the sender.

S/MIME is used to allow a user to assert it is the sender of a certain message.

It allows us to ensure the non-repudiation property, given that when we allow a sender to take ownership over a message we can confirm its origin.
And moreover we have a way to confirm to a third party that the sender transmitted said message.
