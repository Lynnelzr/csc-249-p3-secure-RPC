1. **Overview of Application**  
   This document describes the message format and communication protocol used between the client and VPN server in a simulated secure VPN environment. The application simulates core aspects of secure communication, including TLS handshake, encryption, and certificate validation. The system is designed for learning purposes and illustrates how secure data exchange is implemented over a network.

2. **Format of an Unsigned Certificate**  
   An unsigned certificate in this simulation contains the following fields:  
- Subject Name: A string representing the entity's name (e.g., "Client").  
- Public Key: A generated RSA public key for encryption.  
- Issuer Name: Set to \`None\` for unsigned certificates.  
- Serial Number: A unique identifier for the certificate.

3. **Example Output**  
   Input:  "Hello, Secure Server\!"  
   Output: 'revreS eruceS ,olleH'

4. **Walkthrough of TLS Handshake Steps**  
   1\. Client Hello:  
      \- The client initiates the connection by sending its supported ciphers and hash algorithms to the server.  
      \- Purpose: Allows the server to select a mutually compatible cipher suite.  
   2\. Server Certificate:

  	 \- The server sends its signed certificate to the client.  
\- Purpose: Enables the client to verify the server's identity using the Certificate Authority's public key.  
3\. Key Exchange\*\*:  
  	 \- The client generates a symmetric session key and encrypts it with the server's public key before sending it to the server.  
  	 \- Purpose: Ensures that only the server can decrypt the symmetric key.  
4\. Session Key Confirmation:  
   	\- The server decrypts the session key and acknowledges by encrypting a confirmation message using the same key.  
  	 \- Purpose: Establishes mutual agreement on the session key.  
5\. Secure Communication:  
  	 \- Subsequent messages are encrypted and HMAC'd using the established session key.  
   	\- Purpose: Provides confidentiality and integrity of the data in transit.

5. **Security Limitations**

1\. Asymmetric Key Generation Scheme  
\- Limitation: The RSA key pairs are generated with fixed or predictable parameters in this simulation.  
\- \*\*Exploit\*\*: An attacker could reverse-engineer the key generation process to discover the private key.  
2\. Certificate Authority's Public Key Distribution  
\- Limitation: The CA's public key is not securely pre-shared with clients.  
\- Exploit: A man-in-the-middle (MITM) attacker could replace the CA's public key with their own, enabling them to impersonate the server.  
3\. Use of \`eval()\` in Python Code  
\- Limitation: The \`eval()\` function may be used for parsing or executing commands.  
\- Exploit: If unvalidated input is passed to \`eval()\`, an attacker could inject malicious code, compromising the entire system.

6. **Acknowledgement**  
   Quinn He helped me with finding the reason why my code was not returning the message after the client and server started. She also helped me with understanding the sequence of transforming messages between client, VPN, and server from the code side.

