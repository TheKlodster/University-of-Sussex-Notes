# Introduction to Cryptography

## Crpytographic Systems
Classed along three independent dimensions:
- The type of operations used for transforming plaintext to ciphertext.
  - Substitution: each element in the plaintext is mapped into another element.
  - Transposition: elements in plaintext are rearranged.
- The number of keys used.
  - Sender and receiver use the same key - symmetric.
  - Sender and receiver use a different key - asymmetric.
- The way in which plaintext is processed.

```
Where p is the plaintext character.
Where c in the ciphertext character.

C = E(k, p) = (p + k) % 26  - Encryption
P = D(k, c) = (c - k) % 26  - Decryption
```

### Steganography
Conceal the existence of the message. Various techniques:
1. Character marking.
2. Pin punctures.
3. Typewriter correction ribbon.
4. Through social media chat.
5. Behind images.

Does not use a lot as it is not very secure.

## Ciphers

### Ceasar Cipher
The ceasar cipher is a type of **substitution** cipher.
- each letter of a given text is replaced by a letter some fixed number of positions down the alphabet.

So for instance, with a shift of 1, A would be replaced by B, B would become C.