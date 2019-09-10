# Enrolling A Community Node 

Welcome to OPES! We are glad that you have decided to enroll as a Community Node!
Complete the instructions below, and you will be enrolled shortly. 

**This process is only available for pre-approved accounts. To request approval, contact [support@opes.one](mailto:support@opes.one)**

**Note**: *These instructions are deprecated and will expire on September 1st, 2019. A new enrollment process will be implemented at that time.*

## Version 1.1.0

## Key Generation

Generate public/private key-pairs that will control your new Community Node and associated Infrastructure Node and Access Node using the following steps:

1. Using your browser (Chrome, Firefox, Edge, etc) navigate to the URL: [https://keygen.opesx.io/](https://keygen.opesx.io)

2. Click `Generate OPES Key`

3. A public/private key-pair will be generated. The key pair acts like a lock and key for encryption and authorization. We will call this the `Community Owner Key Pair`.
    - This is the primary key pair for your account, and will have total control over your account's security. Store it safely!
    - **WARNING: There is absolutely NO WAY to recover your account if an Owner Private Key is lost or compromised!**
      *  Keep multiple copies of your key-pair by writing them *both* down, taking a picture, or saving them on a USB drive. 
      *  **Save *both* of these keys together in a secure place!** 
      *  ***Do not ever* send your *private-keys* over the internet, or through text messages!** (The link we used generated the keys on your computer and did not send them over the internet.)
    - Note: The public key will begin with "OPES", the private key will begin with random characters

4. Open a new browser window or tab, then follow steps 1-3 again to create a `Community Active Key Pair`. 
   - This key pair provides direct access to your account on-chain. Store it safely, in the same manner as the `Community Owner Key Pair`!

5. To allow someone else to run your AN or IN service without exposing the primary keys on your new account (e.g. deploying an Infrastructure Node maintained by a cloud service provider), additional *Work Keys* should be created. Create these *Work Keys* by twice repeating steps 1-4 above.
    - The following permissions are given to the *Work Keys*
      - **Infrastructure Node Work Key**: Create Blocks
      - **Access Node Work Key**: Sign tallies from Personal Nodes
    - **NOTE**: This step is optional if it is desired to use the same keys for all actions. In that case, simply reuse the same `Community Active Key Pair` as the new *Work Keys*
    - Label the *Work Key* key pairs as listed below:
        - `Access Node Work Key Pair`
        - `Infrastructure Node Work Key Pair`
<br> 

## Account Names Selection

Create an account name (following the rules below) that you want to represent your Community Node account on the OPES blockchain. This name cannot be changed later, and will be displayable to other users, so choose wisely. 

### Account Naming Rules
- The account name must be between one (1) and twelve (12) characters
- The account name may use any lowercase letter from a-z, the numbers 1-5, and period (".").
- The account name must not end with a period ("."). 
- **Note**: In additon to requesting an invalid format name, using any profanity or offensive language in the name will result in the request being rejected

## Info Service Creation (OPTIONAL)

To incorporate OPES with a community, a specific endpoint must be provided which supplies information about that community. The [CN Info Service](../deployment/README.md) must be at an externally accessible location so OPES can find it. Note the fully qualified URL (e.g. `https://access.example-org.com`) as `Community Info URL`.

**NOTE**: The `CN Info Service` does not need to be deployed to complete this process, only for the Community Node's information to be properly displayed to OPES users. Deploying the CN Service may be skipped as long as the future `Community Info URL` is known.   

## Nominator Names

When creating a Community Node, you must be nominated by both another Community Node and Personal Node. Obtain and record the blockchain IDs (similar to the account names that were generated earlier) of these nominators as `Nominating Community Node Name` and `Nominating Personal Node Name`. These names must be valid, active accounts or the request will be rejected.

## Enrollment Email

Finally, create an email addressed to `support@opes.one` with subject `OPES Community Node Enrollment`. 

1. Place your chosen account name into the email body, labeled `Community Node Name`.

2. Add the `Nominating Personal Node Name` and `Nominating Community Node Name` to the email body.

2. Copy & paste the four previously generated ***public keys*** into the email body and label them appropriately. Ensure that the copy did not leave out any characters at the beginning or the end of the keys.
    - Note: Public keys will begin with "OPES", private keys will not. Do not distribute keys that do not begin with "OPES"
    - *DO NOT* send *private* keys to this address, or any other. 
    - Make sure to copy and paste your public keys *exactly* as they are generated. 
    - The four keys that should be included are:
        - `Community Node Owner Public Key`
        - `Community Node Active Public Key`
        - `Access Node Work Public Key`
        - `Infrastructure Node Work Public Key`

3. Add the `Community Info URL` for the CN service into the email body.   

4. Include your actual name in the email.

5. Send the email

### Example Enrollment Email

```
From: example@newcommunity.io
To: support@opes.one
Subject: OPES Community Node Enrollment

Hello,

Here are the details for the Community Node I wish to enroll. Thanks in advance!

---

Community Node Name:
desireCNname

Nominating Personal Node Name:
referPNname1

Nominating Community Node Name:
referCNname1

Community Node Owner Public Key:
OPES56aP9296ULGMPTnW9k82dskngrdoEGS6qDY3LP3a4XL43YpgwX

Community Node Active Public Key:
OPES6hEEMWAktX7YmZDgxnFVMjGaQqXQWKtSGR1nLusGE5KVRb8DW5

Access Node Work Public Key:
OPES7HYZmjKBZUY8U55uRn5HM5HFGiDFqSSseSWMJ3xKLocis3UJGr

Infrastructure Node Work Public Key:
OPES6hEEMWAktX7YmZDgxnFVMjGaQqXQWKtSGR1nLusGE5KVRb8DW5

Community Info URL:
https://newcommunity.io/info

---


Sincerely,
Eric Xample
```

## Finishing Up

Once you have finished, the OPES team will enroll your Community Node. Upon successful enrollment, the OPES team will contact you and provide additional account information, such as the access keys to allow an Infrastructure Node to connect to the OPES-managed Infrastructure Nodes. 
