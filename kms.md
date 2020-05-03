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