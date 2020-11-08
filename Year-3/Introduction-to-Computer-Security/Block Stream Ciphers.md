# Block Stream Ciphers

## All forms of Encryption
- Symmetric encryption.
- Asymmetric encryption.
- One-way hash.
- Encoding.

## Block & Stream Cipher
### Block Cipher

1. Plaintext is divided into a Message block
   - Message block size depends on what cipher is used.
2. Key is used the cipher block.

### Stream Ciphers

## Symmetric Encryption
Five key ingredients:
1. Plaintext.
2. Encryption algorithm.
3. Secrekt key.
4. Ciphertext.
5. Decryption algorithm.

### Computationally Secure Ecryption Scheme
System's encryption is **computationally secure** if:
- cost of breaking cipher exceeds value of information.
- time.

## Block Cipher Structure
Block size -> Key size -> Number of rounds -> Subkey generation algorithm -> Round function -> Fast sofware - > Ease of analysis.

## Data Encryption Standard (DES)
Block size and key size of 64 bits. Key size 8 bits are check bits, so it's kinda 56 bits instead.

Key processes in DES:
1. Permutation.
   - initial permutation 58 bit becomes first position and 7 becomes last.
2. Round function.
3. Key generation.

Problem with DES: can be bruteforced, key size too small.
Problem with 3DES: too slow.

## Key Districution
The delivering of a key to two aprties that wish to exchange data without allowing others to see the key.

How it's achieved:
- A key could be selected by A and physically delivered by B.


