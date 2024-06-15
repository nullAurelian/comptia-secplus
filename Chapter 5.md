Cryptographic ciphers, modes of operation, use cases and weaknesses.
- Plaintext
- Ciphertext
- Cipher
- Cryptanalysis
<h1>Concepts</h1>
- Hashing : check before vs after of hash to detect compromise
- Ciphers: system of substitution or transposition of characters to hide the original text
	- Stream cipher: each bit is encrypted as it is seen (ie array or queue of data to cipher)
	- Block cipher: data is encrypted in blocks or chunks, padding if the data is less than the chunk size.
- Key: the specific method of cipher, method to reverse a cipher to get plaintext
	- Keyspace: range of possible values of a key (approx. 2^n where n is the size of the key). Longer keys are stronger.
- Symmetric encryption: a single key can be used for both encryption and decryption. Lightweight to set up, but more vulnerable to cracking
- Asymmetric encryption: the key for encryption is different than the key for decryption. 
	- Generally uses two keys - public and private
	- Public key is used to get the private key, private key is used to decrypt the message.
	- Can be used for proof-of-identity for security method because the initial public key must be given by the owner to any recipients.
	- Typically uses RSA algorithm
		- RSA is known as a trapdoor function - easy to perform encryption with the public key and difficult to reverse without the private key.
- Elliptic Curve Cryptography (ECC): another type of trapdoor function
<h2>Uses</h2>
- Digital Signatures take advantage of hashing to ensure that a document hasn't been tampered with.
	- I run hash, if it matches the expected hash document is genuine
	- Hashing can be used with a shared secret to create a message authentication code -  a password that indicates that no tampering has occurred.
- Key exchange/Digital envelopes is a system of encoding a symmetric key to protect a follow-up message.
	- Authenticity is proven in the envelope packet header
	- When using digital envelopes, parties must agree on a bulk encryption secret key. This encryption uses temporary or ephemeral session keys using Diffie-Hellman key agreements. Generated key uses math to generate a secret key from two publicly transmitted keys.
- The combined authentication and message encryption system uses multiple ciphers. This is known as a whole as a cipher suite.
	- Signature algorithm: confirms identify
	- Key exchange/agreement algorithm: used by all parties to derive same bulk encryption key.
	- Modes of operation:
		- Cipher Block Chaining Mode: encode the first data block, then use the resulting with then next block in an XOR operation to get the encoding of the next block. Repeat until the data is encoded. Relies on the initial data block to decode the rest of the data, hence Block Chain.
		- Counter Mode: Applies an initial value plus a counter to the key to get the encoding key for the data stream. The resulting key is XOR'd to the data in the plaintext data.
- To augment encryption, we add authentication methods. Without authentication ciphers are vulnerable to ciphertext attacks.
	- Message Authentication Code (MAC) works by hashing the message output and the secret key together. Authentication is related to the cipher suite used. 
	- Authenticated Encryption with Additional Data (AEAD) is an answer to Cipher Block Chaining weaknesses of adding padding to data packets to make up space. AEAD is a streamed encryption system that uses the header to ensure that the payload has not been replayed by another user already (not accessed previously, ergo cannot be modified).
- A single hash function or cipher is known as a **cryptographic primitive**. A complete system will have multiple primitives. AKA each step is a primitive
<h3>Limitations</h3>
- Cryptography has limititations
	- Speed - 
	- Time/Latency - low latency applications may restrict how much work can be done on a message before the compute times out the message usabiitiy
	- Size
	- Computation overhead - large, complex ciphers will use more compute time and more compute power and more power overall.
- Entropy is the noise or disorder in a message. Human-readable data is low-entropy; a good cryptographic system exhibits high-entropy.
	- When a key is weak it produces ciphertext that has lower than acceptable entropy.
- Predictable keys are a major weakness.
	- Nonce  is short for "number used once" with a scope. A good cryptographic system will only use keys once for communications.
	- Initialization vector is the starting key
	- Salt or salting is placing random or pseudo random values to obfuscate data against dictionary and brute-force styled attacks that look for relationships between values and outputted hash values.
		- Variation on salting is keystretching - a user's password and a salt value are repeatedly used to create a longer, more random key. While not necessarily more secure, the repeated rounds means it takes longer to decode the password.
```
(salt + password) * SHA = hash
```
- Data that is stored in any capacity outside the originator needs to be kept encrypted to protect user privacy. A good cipher for purpose needs to resist decryption for the duration of storage.
- Hashing collisions are cases where two inputs produce the same hash value. This is also known as a birthday attack based on the idea that the attack may be less intensive to compute than expected (the origin is the question of how many people do you need in a room to have a 50% chance that two of them have the same birthday). 
	- Attackers perform recon on hashing systems by placing both benign and malicious documents and comparing them with minor changes to get an idea of how far the system can be pushed before it generates a new hash.
<h3>Quantum and other technologies</h3>
- Quantum computing is a future type that takes standard binary computing (1 or 0) and adds a third state known as _superposition_. Superposition is indeterminate and can be either 0 or 1, collapsing to one of the two values when it is read.  This new processing unit is known as a qubit.
	- Qubits can be entangled with each other. When one entangled qubit is resolved, all other qubits entangled with that qubit are resolved to the same value.
- Homomorphic encryption is a method that allows computation of certain fields in a dataset without decryption. It's a blackbox getter function.
- Blockchain is a concept where transactions are recorded with cryptography and the resulting list is run through a hash function. When another system accesses this public ledger it can calculate each step and verify integrity.
- Stenography is a method for obscuring data within another set of data. An example in technology is using TCP packet data fields as a second message channel, or by changing the least significant bit of pixels in an image file.
	- This might be used in data exfiltration.