# SPHINXHybridKey

## Introduction

This project is dedicated to the world community as an Open-source Post-quantum blockchain layer 1 project, means anyone can join and contribute based on his/ her passion and skills. SPHINX is a blockchain protocol designed to provide secure and scalable solutions in the post-quantum era.

This repository contains code for the SPHINXKey project, which is a `Generating Key, Master key, and Address` module for the SPHINX blockchain framework.

## Components

In the thrilling era of quantum computers, where we find ourselves in a `Super Position` between classical and quantum realms, the choice of a hybrid key exchange scheme combining `X25519` and `Kyber768` holds immense significance. Let's explore why this combination is the perfect fit.

1. Embracing the Best of Both Worlds: `X25519`, a battle-tested and widely adopted algorithm, provides a solid foundation of proven security and efficient key generation. On the other hand, `Kyber768` represents the cutting-edge of post-quantum cryptography, designed to resist attacks from powerful quantum computers. By combining these two exceptional algorithms, we enter a "Super Position" where we benefit from the strengths of both classical and quantum-resistant cryptography.

2. Inspiration from Tech Giants: The widespread adoption of `X25519` and `Kyber768` by the larger tech community serves as our guiding light and inspiration. These algorithms have garnered trust and confidence from experts and industry leaders, paving the way for their integration into our hybrid scheme. By following in the footsteps of these role models, we embrace a solution that is not only innovative but also aligns with industry best practices.

In this era of immense technological possibilities, the combination of `X25519` and `Kyber768` in a hybrid key exchange scheme symbolizes our readiness to face the challenges presented by quantum computing. It demonstrates our commitment to leverage the proven track record of `X25519` and the promising resilience of `Kyber768`. Together, these algorithms empower us to navigate the quantum landscape with confidence, ensuring the security and longevity of our cryptographic systems.

### The Purpose 

The combination of `X25519` and `Kyber768` in a hybrid key exchange is designed to harness the unique strengths of each algorithm, resulting in a more robust and versatile cryptographic solution.

`X25519` is an elliptic curve Diffie-Hellman (ECDH) key exchange algorithm based on the Curve25519 curve. It offers several advantages, including efficient key generation, compact key sizes, and resilience against various common attacks. X25519 excels in terms of both performance and security, making it an ideal choice for key exchange operations.

On the other hand, `Kyber768` is a post-quantum key encapsulation mechanism (KEM) that addresses the security challenges posed by quantum computers. It is based on the Learning With Errors (LWE) problem and provides strong resistance against attacks by quantum adversaries. Kyber768 offers a robust security guarantee in a post-quantum computing era when traditional cryptographic schemes may be vulnerable.

By combining `X25519` and `Kyber768` in a hybrid key exchange, we can leverage the efficiency and security benefits of `X25519` while also incorporating the post-quantum resistance of `Kyber768`. This hybrid approach enables we to strike a balance between immediate performance needs and long-term security considerations. It is particularly advantageous in scenarios where both efficient key exchange and protection against future quantum threats are crucial.

### Description and logic;
- `X25519` given 128-bit security level
- `Kyber-768` given (equal AES-192) mean 192-bit security level
  
If we `merged` them it means we will achieve security level nearly `320-bytes`, its lightweight enough.


### SPHINXKey Namespace

The `SPHINXKey` namespace provides functions for generating key pairs, calculating addresses, and printing key information. It relies on functionality from other included headers such as `Hybrid_key.hpp` and `Hash.hpp`.

### Functions

- The code defines a function called performX25519KeyExchange that performs the `X25519` key exchange given a private key, public key, and a buffer to store the shared key.

- It defines a structure called HybridKeypair, which holds the merged key pair consisting of a Kyber768 key pair and an `X25519` key pair, as well as PKE key pair, and a random number generator.

- The function `generate_hybrid_keypair` generates a hybrid key pair by generating a `Kyber768` key pair, an `X25519` key pair, and a PKE key pair using appropriate functions. It returns the generated hybrid key pair.

- The function deriveMasterKeyAndChainCode is used to derive a master private key and chain code from a given seed using the `HMAC-SHA512` function. It returns the `derived master private key` and `chain code` as a pair.

- There are several utility functions defined, such as `deriveKeyHMAC_SHA512` to derive a key using `HMAC-SHA512`, `hashSWIFFTX512` to calculate the `SWIFFTX-512` hash of data, and `generateRandomNonce` to generate a random nonce.

- The function `deriveKeyHKDF` derives a key using the `HKDF` (HMAC-based Key Derivation Function) algorithm with `SHA256` as the default hash function.

- The function hash calculates the `SWIFFTX-256` hash of a given input.

- The function generateKeyPair generates a random private key and calculates the corresponding public key by hashing the private key.

- The function generateAddress generates an address from a given public key by hashing the public key and taking the first 20 bytes of the hash.

- The function `requestDigitalSignatur`e requests a digital signature for a given data using the provided hybrid key pair.

- The functions encryptMessage and decryptMessage are used to encrypt and decrypt a message, respectively, using the `Kyber768` KEM (Key Encapsulation Mechanism).

- The functions `encapsulateHybridSharedSecret` and `decapsulateHybridSharedSecret` are used to encapsulate and decapsulate a shared secret using the `hybrid KEM`, which combines `X25519` and `Kyber768`.

This code provides a set of functions and structures to support hybrid key generation, key exchange, encryption, decryption, and other cryptographic operations.


#### The interaction and collaboration between Hybrid_Key.hpp and [SPHINXKey](https://github.com/ChyKusuma/SPHINXHybridKey) can be summarized as follows:

## Interactions between SPHINXKey and SPHINXHybridKey Namespaces

1. **SPHINXKey Namespace** interacts with the **SPHINXHybridKey Namespace** by calling the function `generate_hybrid_keypair` from the `SPHINXHybridKey` namespace. This function generates the hybrid keypair and its corresponding private and public keys.

2. The function `SPHINXKey::generateAddress` uses the `SPHINXHybridKey::SPHINXHash::SPHINX_256` function to hash the public key and generate an address based on the hash. This address is used for smart contract identification.

3. In `SPHINXHybridKey::generate_hybrid_keypair`, Kyber768 and X25519 keypairs are generated. The function also derives a master private key and chain code using HMAC-SHA512 from a seed value and then derives private and public keys from the master key and chain code using HMAC-SHA512.

4. The `SPHINXHybridKey` namespace provides functions to encrypt and decrypt messages using Kyber768 for KEM (Key Encapsulation Mechanism).

5. The `SPHINXHybridKey::performX25519KeyExchange` function performs the X25519 key exchange.

6. The `SPHINXHybridKey` namespace also includes functions to encapsulate and decapsulate shared secrets using the hybrid KEM, combining the results of Kyber768 and X25519.

**Combined Usage**:
The combined usage of `SPHINXKey` and `SPHINXHybridKey` allows for the generation of secure hybrid keypairs that leverage the strengths of both Kyber768 and X25519 cryptographic algorithms. The hybrid keypairs can be used for various cryptographic purposes, including encryption, decryption, and key exchange, making it a versatile and robust cryptographic solution.


The interaction between Key.cpp and Hybrid_key.hpp involves calling functions defined in Hybrid_key.hpp from Key.cpp to perform various operations related to hybrid key generation, key exchange, address generation, and public key calculation. Hybrid_key.hpp provides the necessary functions and data structures to support these operations, and Key.cpp utilizes them to implement the desired functionality.


### Note

Every code in the repository is a part of the SPHINX blockchain algorithm, which is currently in development and not fully integrated or extensively tested for functionality. The purpose of this repository is to provide a framework and algorithm for the digital signature scheme in the SPHINX blockchain project.

As the project progresses, further updates and enhancements will be made to ensure the code's stability and reliability. We encourage contributors to participate in improving and refining the SPHINXBlock algorithm by submitting pull requests and providing valuable insights.

We appreciate your understanding and look forward to collaborative efforts in shaping the future of the SPHINX blockchain project.


## Getting Started
To get started with the SPHINX blockchain project, follow the instructions below:

1. Clone the repository: `git clone https://github.com/ChyKusuma/SPHINXHybridKey.git`
2. Install the necessary dependencies (List the dependencies or provide a link to the installation guide).
3. Explore the codebase to understand the project structure and components.
4. Run the project or make modifications as needed.


## Contributing
We welcome contributions from the developer community to enhance the SPHINX blockchain project. If you are interested in contributing, please follow the guidelines below:

1. Fork the repository on GitHub.
2. Create a new branch for your feature or bug fix: `git checkout -b feature/your-feature-name` or `git checkout -b bugfix/your-bug-fix`.
3. Make your modifications and ensure the code remains clean and readable.
4. Write tests to cover the changes you've made, if applicable.
5. Commit your changes: `git commit -m "Description of your changes"`.
6. Push the branch to your forked repository: `git push origin your-branch-name`.
7. Open a pull request against the main repository, describing your changes and the problem it solves.
8. Insert your information (i.e name, email) in the authors space.

## License
Specify the license under which the project is distributed (MIT License).

## Contact
If you have any questions, suggestions, or feedback regarding the SPHINX blockchain project, feel free to reach out to us at [sphinxfounders@gmail.com](mailto:sphinxfounders@gmail.com).
