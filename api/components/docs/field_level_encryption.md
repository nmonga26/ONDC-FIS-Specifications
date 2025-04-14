### Field Level Encryption

  This document outlines a secure communication protocol between Network Participant 1 (NP1) and Network Participant 2 (NP2) utilising the AES-GCM encryption algorithm. 
  The communication process involves NP1 fetching the public keys of NP2 from a registry which are already exchanged during the subscription process, creating a shared key with its private key, and using this shared key to encrypt data for transmission to NP2.


#### Communication Steps
  - Public Key Retrieval from Registry:
      - NP1 initiates the communication process by fetching the public keys of NP2, a step facilitated during the subscription process.

  - Shared Key Generation:
      - NP1 utilizes its private key & the fetched public key to generate a shared key, this process employs the Diffie-Hellman key exchange algorithm.
      ```
        // Calculate the shared secret key using Diffie-Hellman
        const sharedKey = crypto.diffieHellman({
          privateKey: MC4CAQEwBQYDK2VuBCIEIMCU0uKQ36pRs4d9Jm0aUD9Pn6qq+747AY2Kv4UhE/94,
          publicKey: MCowBQYDK2VuAyEA2qqMXULrFHhJCJEI38WnTtwojAtf9cZ3BsUid5Goah4=,
        });

       ```  
  - Data Encryption Using AES-GCM:
      - With the shared key in place, NP1 uses the AES-GCM encryption algorithm to secure the data intended for NP2.
        ```
          // Encrypt the previously encrypted string using the shared key
          encryptedString = Encrypt(data, sharedKey)

        ``` 
  -  Shared Key Decryption:
        - The NP2 decrypts the shared key using its private key and the public key of the NP1
          ```
            // Calculate the shared secret key using Diffie-Hellman
            const sharedKey = crypto.diffieHellman({
              privateKey: MC4CAQEwBQYDK2VuBCIEICDWXCT+/VoLE8TJ5nYbtGv5vI+sqXBtdYgrBMjD73Vz,
              publicKey: MCowBQYDK2VuAyEAmb/MUSKXvtgsPJuEQUM/imlDJ7oe9uPL/m4ta9e8Z1o=,
            });

            ```
  - Data Decryption by NP2:
      - NP2 uses the decrypted shared key to decrypt the received data
        ```
          decryptedString = decrypt(data, sharedKey)
        ```
  - ### Example:
      - Type “CODE”: 
          - In authorization, when the type is set to "code," NP2 is not required to decrypt the token. The token remains in its original form and can be directly utilized without the need for decryption by NP2.

        ```
          "authorization": {
              "type": "CODE",
              "token": "dWt5gzA/oqzWkkN8HI/gC/9fV8AVCkPjQAAAABJRU5Erkgg==”,
              "valid_to": "2024-03-23T23:59:59.999Z",
              "status": "UNCLAIMED"
            }

        ```  
      - Type "ENCRYPTED_CODE":
          -  In authorization, when the type is set to "encryptedCode, NP1 includes the encrypted string as part of the authorization key. NP2 has the to decrypt this string, to access the token's value 

          ```
            "authorization": {
                "type": "ENCRYPTED_CODE",
                "token": "U2FsdGVkX1/gV/2wQx83uKkQdDpNPTq8+75IUZziK17qxdmBvsVT+KfQ==",
                "valid_to": "2024-03-23T23:59:59.999Z",
                "status": "UNCLAIMED"
            }
            ```
      - ENCRYPTED_CODE_PIN  
          ```

            {
              "type": "ENCRYPTED_CODE_PIN",
              "token": "CODE :U2FsdGVkX1/gV/2wQx83uKkQdDpNPTq8+75IUZziK17qxdmBvsVT+KfQ==;PIN:U2FsdGVkX1/gV/2wQx83uKkQdDpNPTq8+75IUZziK17qxdmBvsVT+KfQ==",
              "valid_to": "2024-03-23T23:59:59.999Z",
              "status": "UNCLAIMED"
            }

          ```  


                  
            