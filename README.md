An Anonymous Verifiable Voting System

Introduction
In today’s world, ensuring that voting is both secure and private is more important than ever. Our project focuses on
creating a system where people can vote without anyone else knowing their choices. This kind of system uses special
methods to keep votes secret and make sure that all votes are counted correctly.The key to our system is using what’s
called public-key encryption and mixnets. Public-key encryption helps keep each vote hidden and secure. Mixnets, on the
other hand, shuffle all the votes together. This shuffling is done by a series of servers one after the other, which makes it
hard to trace a vote back to the voter. After all the votes are mixed up, they end up in a random order, cutting any ties
between a vote and the person who cast it.What makes our system even more reliable is something called zero-knowledge
proofs. These are clever ways to check that all votes are shuffled correctly without actually showing the votes themselves.
This ensures that no votes are changed or lost in the shuffle.By building this system, we aim to provide a voting method
that not only keeps everyone’s vote private but also lets everyone check that the voting process was fair and accurate,
without compromising vote secrecy.

System Components
• Voter: The voter component is crucial in ensuring that the votes are cast securely and anonymously. In our system, each
voter encrypts their vote using a public key issued by the auditor. This process ensures that the vote remains confidential and
tamper-proof until decryption. The encryption method used ensures that the encrypted vote remains unreadable to anyone
except the auditor who possesses the corresponding private key. This method aligns with traditional practices in cryptographic
systems where data confidentiality is paramount.
• Auditor: The auditor serves a dual role in our system. Firstly, the auditor is responsible for generating and distributing the
public key used for vote encryption. This key management process is critical as it ensures that all voters have a uniform and
secure method of encrypting their votes. Secondly, after the voting process concludes, the auditor decrypts the collected votes
using the private key. This step is sensitive and crucial as it translates encrypted data back into readable votes which are then
tallied. The auditor also plays a key role in verifying the integrity of the election process, ensuring that the voting process has
been fair and free from tampering.
• Mixing Servers: Mixing servers add an additional layer of anonymity to the voting process. Once votes are cast and collected,
they are passed through a series of mixing servers. Each server shuffles and re-encrypts the votes, further anonymizing them
by breaking the direct link between the voter and their vote. This process is crucial in protecting voter privacy and preventing
any potential vote tracking or manipulation. The mixing servers also provide zero-knowledge proofs to demonstrate that they
have correctly shuffled the votes without altering or losing any data, thus maintaining the integrity and anonymity of the voting
process.

System Workflow
• Key Distribution: Prior to the election, a trusted entity, which we call the auditor, is responsible for creating a secure
environment for the voting process. The auditor generates two very important pieces of information: a public key (often denoted
as pki) and a private key (ski). The public key is akin to a locked mailbox: anyone can drop something inside (in this case, a
vote), but only someone with a key (the private key) can open it and see what’s inside. This public key is shared with all eligible
voters, enabling them to encrypt their votes in preparation for casting.
• Vote Casting: In the voting phase, participants use the auditor’s public key to encrypt their vote, which is essentially their
chosen candidate. This encryption transforms the vote into a secure format that can’t be read by others, ensuring that the
voter’s choice remains a secret. Once encrypted, the vote is submitted to the system, joining the pool of other encrypted votes
which are already available.
• Vote Mixing and Re-encryption: After the voting period ends, the collected votes undergo a process called mixing, performed
by a set of servers known as the mixnet. The mixnet’s job is to shuffle all the encrypted votes, similar to mixing a deck of cards,
so that no one can tell which vote came from which voter. But shuffling isn’t enough on its own; to further enhance secrecy,
the mixnet also re-encrypts the votes. This doesn’t change who each vote is for; it just gives the encrypted vote a new disguise.
While doing all this, the mixnet also creates a special kind of assurance, known as a zero-knowledge proof, which is a way to
prove that the shuffling and re-encryption were done correctly without actually showing the original or final order of the votes.
• Decryption by Auditor: Following the mixnet’s thorough shuffling and re-encryption, the auditor comes back into the picture.
Using the private key that pairs with the earlier distributed public key, the auditor can unlock and decrypt the votes. Thanks
to the mixnet’s careful work, even though the auditor can see the votes, they can’t tell who voted for who. The encryption
methods ensure that the mixing process does not affect the auditor’s ability to count the votes accurately.
• Tallying and Result Announcement: With the votes decrypted, the auditor counts them up. This is the moment of truth
where the votes for each candidate are tallied, and the winner is determined. The integrity of the entire process, upheld by the
zero-knowledge proofs, means that everyone can trust in the announced results, even though the inner workings of the votes’
journey through the mixnet remain private.

Technical Implementation
• Imports: getPrime, GCD, inverse, and getRandomRange are imported from Crypto.Util.number module. These are used for
generating prime numbers, calculating greatest common divisor, finding inverses modulo, and generating random numbers in a
specified range. randrange and shuffle are imported from the random module for generating random numbers and shuffling lists,
respectively. hashlib is imported for cryptographic hashing functions.
• key generation: Generates ElGamal public-private key pair. p is a large prime number, g is a generator, x is a randomly
chosen integer in the range [2, p - 1], h is computed as g power x mod p and returns the public key tuple (p, g, h) and the
private key x.
• Encryption: Encrypts a vote choice using the ElGamal encryption scheme.Generates a random number k in the range [2, p -
1].Computes the ciphertext pair (c1, c2) and returns the pair.
• Vote shuffling: Shuffles the encrypted votes to provide anonymity.For each encrypted vote (c1, c2), Generates a random number
k’ in the range [2, p - 1]. Computes new ciphertext pair (c1’, c2’) where c1’ = (c1 * g power k’) mod p and c2’ = (c2 * h power
k’) mod p. Returns the shuffled and re-encrypted votes.
• Zero-Knowledge Proof in Voting System: In our voting system, zero-knowledge proofs play a crucial role in ensuring that
the shuffling of votes is done correctly without revealing individual votes. We use a combination of commitment schemes and
zero-knowledge proof techniques to achieve this. For each shuffled vote, commitments are generated for both the original and
shuffled votes. These commitments are then used in a zero-knowledge proof to show that the commitments represent the same
set of votes, thus proving the shuffle was honest without revealing the actual vote content. This method ensures that even if
the votes are shuffled and re-encrypted, they remain anonymous and untraceable back to the original voter, maintaining voter
privacy and the integrity of the voting process.
• Verifying the Integrity of the Shuffle: To verify the integrity of the voting shuffle, our system uses complex algorithms
that check the consistency of vote encryption before and after the shuffle. By employing mathematical proofs that leverage the
properties of the zero-knowledge proofs, the system can confirm that the order and content of votes have been altered only in
terms of their sequence and not in their actual content. These proofs ensure that the shuffle does not introduce any bias or
modify the votes, thereby upholding the fairness and transparency of the voting process.
• Decryption and Tallying: Decrypts a vote using the ElGamal decryption algorithm. For a given ciphertext pair (c1, c2) and
private key x, computes: s = (c1 power x) mod p and m = (c2 * s power -1) mod p. Returns the decrypted vote m.


Zero-Knowledge Proofs for Mixnet Verification
A Zero-Knowledge Proof (ZKP) is a method by which one party (the prover) can prove to another party (the verifier) that
a given statement is true, without conveying any additional information apart from the fact that the statement is indeed
true. In the context of voting, this typically involves proving operations like shuffles and re-encryptions were performed
correctly without revealing the original votes or the specifics of the shuffle process. Commitments in this code refer to
cryptographic commitments made to specific values or states before and after the shuffle and re-encryption processes.
These are used to ensure that the values haven’t been tampered with and remain consistent through the process, without
revealing the underlying values themselves. For each re-encryption or shuffle, a new commitment can be generated to the
result. The commitments are then used in a zero-knowledge context to prove that the transformations (shuffles and re-
encryptions) are legitimate.Each commitment in our system likely corresponds to a set of encrypted or transformed votes.
The verification success messages you see (e.g., ”Verification Success for commitment 0”) indicate that a ZKP has been
successfully completed for that particular set of data.For each set of data (or for each commitment), a ZKP would involve
generating proofs that the data matches expected cryptographic patterns or behaviors (such as maintaining consistency
in encryption despite re-ordering). This proves that the operations were performed correctly without revealing what
those operations were exactly.When votes are shuffled and re-encrypted, your system needs to ensure that despite the
operations, the integrity and anonymity of the votes are maintained. This involves proving relationships like logg (original
vote) = logg (shuffled and re-encrypted vote) modulo some parameters, but without revealing the original vote, shuffled
and re-encrypted vote, or the logs themselves.SILMPP stands for Shuffle Integer Logarithm Mix Proof Protocol, a specific
type of zero-knowledge proof protocol designed to complex operations like shuffles in mixnets.The ”SILMPP verification
successful” message indicates that the zero-knowledge proofs required to verify the correctness of the shuffle and mix
operations have been successfully validated. This means the integrity of the shuffle process (and thus the anonymity and
correctness of the voting process) is maintained, and it has been verified without revealing any underlying data about
the votes themselves.In our project, ZKPs are crucial for maintaining voter privacy and ensuring that no unauthorized
information about voter choices or the order of votes is leaked while still allowing external verification of the election’s
integrity. These proofs support the claims of correct, unbiased shuffling and re-encryption by providing mathematical
evidence that all actions were performed correctly, adhering to the designed protocols without exposing any sensitive
details.


Conclusion
In conclusion, our project successfully creates an Anonymous Verifiable Voting System that upholds the privacy of voters
while ensuring the integrity and verifiability of the voting process. By integrating cryptographic key generation, secure
vote encryption, mixnets for vote anonymization, and zero-knowledge proofs, the system sets a high standard for secure
digital elections. It addresses the fundamental need for trust in electronic voting by allowing voters to confidently cast
their ballots, knowing their choices are both private and counted accurately. The implementation of this system represents
a significant step forward in the pursuit of a democratic process that is both transparent and resilient against tampering,
making it a vital advancement for the future of voting in the digital age.


REFERENCES
• A verifiable secret shuffle and its application to e-voting. (ref:https://dl.acm.org/doi/pdf/10.1145/501983.502000)
• Verifiable Shuffle of Large Size Ciphertexts. (ref:https://iacr.org/archive/pkc2007/44500377/44500377.pdf)
• A Review of Cryptographic Electronic Voting. (ref:https://doi.org/10.3390/sym14050858)
• Verifiable Mix-Nets and Distributed Decryption for Voting from Lattice-Based Assumptions.
(ref:https://eprint.iacr.org/2022/422)




