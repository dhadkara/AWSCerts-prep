## KMS (Key Management Service)

KMS is managed service to create and manage encryption keys used to encrypt your data.

CMK (Customer Master Key) 
- KMS Encryption keys are regional
- Cannot be exported (Use CloudHSM if you want to export CMK)

Key Material Options
 - KMS
 - Customer Managed
 - CloudHSM

### KMS API commands

```
aws kms encrypt --key-id YOURKEYIDHERE --plaintext fileb://secret.txt --output text --query CiphertextBlob | base64 --decode > encryptedsecret.txt
aws kms decrypt --ciphertext-blob fileb://encryptedsecret.txt --output text --query Plaintext | base64 --decode > decryptedsecret.txt
aws kms re-encrypt --destination-key-id YOURKEYIDHERE --ciphertext-blob fileb://encryptedsecret.txt | base64 > newencryption.txt 
aws kms enable-key-rotation --key-id YOURKEYIDHERE
```
### KMS Envelope Encryption

- Encrypt
KMS Key ---encrypt--> Data Key(envelope key) --encrypts--> Data
- Decrypt
KMS Key(Master Key) --decrypt--> Encrypted Data Key --> Data Key --decrypt--> Data

## Cognito

- Provides web identity federation by acting as identity broker between your app and identity providers
- Seamless across all the devices web as well mobile. Sync data across multiple devices

![Web Identity Federation](images/CognitoDiagram.png)

### User and Identity Pools

__User Pools__ allow users to directly sign-in or indirectly via fb, google etc. via successfully generating JWT tokens works as identity broker.
__Identity Pools__ enable to create unique identities to obtain temporary limited AWS service credentials.

![Coginito Pools](images/cognito-pools.png)

__Push Synchronization__ Cognito user Push Sync to send silent push notification of user data updates to multiple device type associated with user id. It levereges SNS internally.
