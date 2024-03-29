# CPS_350_RSACrypto
Devin, Brandon, Sydney, and Paul's RSA Cryptosystem
How to generate public and private keys?

An RSA public-key/private-key pair can be generated by the following steps:

1. Generate a pair of large, random primes p and q.
2. Compute the modulus n as n = p*q.
3. Select an odd public exponent e between 3 and n-1 that is relatively prime to p-1 and q-1.
4. Compute the private exponent d such that (e*d) mod ((p-1)*(q-1)) = 1.
5. Output (n,e) as the public key and (n,d) as the private key.

We show an example here. Assume that we choose p = 37, q = 41, although they should be much larger in practice. Then n can be computed as n = p*q = 37*41 = 1517, and we also have that (p-1)*(q-1) = 1440. In order to satisfy the equation in Step 4, we may simply find two numbers 11 and 131 for e and d respectively such that e*d = 1441, and hence the public key is (11,1517) and the private key is (131,1517). 


How to encrypt a message?

Firstly, a text message is translated to a big nonnegative integer number. For example, the message "Hello!" can be encode to the number 72101108108111033 (see below). We may use every 3 digits to represent the code of a character. You may use the Java method String.codePointAt to obtain the code of a character in a string.

 

When we have a public key (11,1517) as well as the corresponding private key (131,1517), and a message encoded as M = 1376, the encrypted message C is generated in the following way such that it can only be recovered by the private key.

 

Then C will be delivered to the receiver who is the only one who knows the private key.
When the receiver gets the encrypted message C, she can use the following formula to decrypt the message.
 

Implementation task
In this project, you are required to write a Java class defining a communication channel using RSA public-key cryptosystem. It provides the following operations.
•	Creating a communication channel with a provided pair of prime numbers.
           // p, q can be provided by the user. You may also manually select e and then compute d.
     // The generated public and private keys should be kept in the object.
     Channel channel = new Channel(p, q);
•	Encrypting a message to the channel.
     // both of m and c are big numbers
     c = channel.encrypt(m);
•	Decrypting a message from the channel.
     // both of m and c are big numbers
     m = channel.decrypt(c);

You may implement a queue to simulate the message exchange of two people. The sender can enqueue a message encoded by the channel, and the receiver can dequeue an encrypted message and decrypt it using the channel. Additionally, if you know how to program multi threads in Java, you may even create two threads, one is used to simulate the sender and the other one is to simulate the receiver.
