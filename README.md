An Anonymous Verifiable Voting System

Introduction

In today’s world, ensuring that voting is both secure and private is more important than ever. Our project focuses on creating a system where people can vote without anyone else knowing their choices. This kind of system uses special methods to keep votes secret and make sure that all votes are counted correctly. The key to our system is using public-key encryption and mixnets.

Public-key encryption helps keep each vote hidden and secure. Mixnets, on the other hand, shuffle all the votes together. This shuffling is done by a series of servers one after the other, which makes it hard to trace a vote back to the voter. After all the votes are mixed up, they end up in a random order, cutting any ties between a vote and the person who cast it. Zero-knowledge proofs further ensure that all votes are shuffled correctly without showing the votes themselves. This process maintains vote secrecy and fairness.

System Components

Voter: The voter encrypts their vote using a public key issued by the auditor, ensuring confidentiality until decryption.
Auditor: Responsible for key generation and distribution, the auditor also verifies the election’s integrity and decrypts the votes after they are anonymized.
Mixing Servers: Adding anonymity, these servers shuffle and re-encrypt votes, maintaining voter privacy and offering zero-knowledge proofs for integrity.
System Workflow

Key Distribution: The auditor generates and shares a public key with voters for encrypting their votes.
Vote Casting: Voters use the public key to encrypt and submit their choices, keeping them confidential.
Vote Mixing and Re-encryption: Votes are shuffled by the mixnet to anonymize them, with zero-knowledge proofs validating the process.
Decryption by Auditor: The auditor decrypts the anonymized votes with the private key, ensuring vote-counting accuracy.
Tallying and Result Announcement: Votes are tallied and the results announced, with zero-knowledge proofs supporting the trustworthiness of the results.
Technical Implementation

Imports: Modules like Crypto.Util.number (for prime generation, GCD, inverse) and random (for randomness and shuffling) are used for encryption and anonymization.
Key Generation: Generates an ElGamal public-private key pair.
Encryption: Encrypts a vote choice using ElGamal.
Vote Shuffling: Uses mixnets to shuffle and re-encrypt votes.
Zero-Knowledge Proof: Ensures shuffles are performed correctly.
Decryption and Tallying: Uses ElGamal decryption to tally votes securely.
Zero-Knowledge Proofs for Mixnet Verification

Zero-Knowledge Proofs (ZKPs) play a critical role in verifying that vote shuffling and re-encryption were performed accurately. This allows the system to confirm the integrity of the shuffle process, maintaining anonymity without revealing individual votes or shuffle specifics. ZKP ensures the privacy and verifiability of each step in the voting process.

Conclusion

Our Anonymous Verifiable Voting System successfully preserves voter privacy while ensuring election integrity. By combining cryptographic key generation, secure vote encryption, and mixnets with zero-knowledge proofs, the system addresses the need for secure, transparent digital elections. This system represents a significant step forward in advancing secure and tamper-resistant democratic processes in the digital age.

References

A verifiable secret shuffle and its application to e-voting
Verifiable Shuffle of Large Size Ciphertexts
A Review of Cryptographic Electronic Voting
Verifiable Mix-Nets and Distributed Decryption for Voting from Lattice-Based Assumptions
