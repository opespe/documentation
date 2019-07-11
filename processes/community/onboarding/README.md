# Enrolling A Community Node 

Weclome to OPES! We are glad you have decided to enroll as a Community Node!
Early adopters like yourself should complete the instructions below and you will be enrolled shortly. 

**This process is only available for pre-approved accounts. To request approval, contact [support@opes.one](mailto:support@opes.one)**

Note: *These instructions expire on August 1st, 2019.*

## Process for New Users

### Key Generation

Generate public/private key-pairs for your new Community Node and associated Infrastructure Node and Access Node using the following steps:

1. Using your browser (Chrome, Firefox, Edge, etc) navigate to the URL: [https://keygen.opesx.io/](https://keygen.opesx.io)

2. Click `Generate OPES Key`

3. A public/private key-pair will be generated. The key pair acts like a lock and key for encryption and authorization. We will call this the `Community Owner Key Pair`.
    - This is the primary key pair for your account, and will have total control over your account's security. Store it safely!
    - **WARNING: There is absolutely NO WAY to recover your account if an Owner Private Key is lost or compromised!**
      *  Keep multiple copies of your key-pair by writing them *both* down, taking a picture, or saving them on a USB drive. 
      *  **Save *both* of these keys together in a secure place!** 
      *  ***Do not ever* send your *private-keys* over the internet, or through text messages!** (The link we used generated the keys on your computer and did not send them over the internet.)
    - Note: The public key will begin with "OPES", the private key will begin with random characters
4. Open a new browser window or tab and follow steps 1-3 again to create a `Community Active Key Pair`. 
   - This key pair provides direct access to your account on-chain. Store it safely, in the same manner as the `Community Owner Key Pair`!


<br> 

### Account Names Selection

Create an account name (following the rules below) that you want to represent your Community Node account on the OPES blockchain. This name cannot be changed later, and will be displayable to other users, so choose wisely. 

Next, create another account name that you want to represent your Access Node account on the OPES blockchain. Like the name of your Community Node, this name cannot be changed later, and will be displayable to other users, so choose wisely. 

#### Account Naming Rules
- The account name must be exactly twelve (12) characters
- The account name may use any lowercase letter from a-z and the numbers 1-5
- The account name must start with a letter. 
- **Note**: In additon to requesting an invalid format name, using any profanity or offensive language in the name will result in the request being rejected

### Info Service Creation

To incorporate Opes with a community, a specific endpoint must be provided, which supplies information about that community. The [CN Service](../deployment/README.md) must be at an externally accessible location so OPES can find it. Note the fully qualified URL (e.g. `https://access.example-org.com`) as `Community Info URL`.

### Nominator Names

When creating a Community Node, you must be nominated by another Community Node and Personal Node. Obtain and record the blockchain IDs (similar to the account names that were generated earlier) of these nominators as `Nominating Community Node Name` and `Nominating Personal Node Name`. These names must be valid, active accounts or the request will be rejected.

### Enrollment Email

Finally, create an email addressed to `support@opes.one` with subject `OPES Community Node Enrollment`. Place and label the Community Info URL for the CN service. Place your chosen account names into the email body, labeled `Community Name` and `Access Name`. Copy & paste both of the *public keys* into the email, and label them appropriately.  
-  Note: Public keys will begin with "OPES", private keys will not. Do not distribute keys that do not begin with "OPES"
- *DO NOT* send *private* keys to this address, or any other. 
-  Make sure to copy and paste your public keys *exactly* as they are generated. 
-  Please include your name in the email.

*Once you have finished, the OPES team will enroll your Community Node and contact you upon its enrollment.*

#### Example Enrollment Email

```
From: example@newcommunity.com
To: support@opes.one
Subject: OPES Community Node Enrollment


Nominating Personal Node Name:
nominPNname1

Nominating Community Node Name:
nominCNname1

Community Info URL:
https://access.example-org.com/info

Community Node Owner Public-Key:
OPES56aP9296ULGMPTnW9k82dskngrdoEGS6qDY3LP3a4XL43YpgwX

Community Node Active Public-Key:
OPES6hEEMWAktX7YmZDgxnFVMjGaQqXQWKtSGR1nLusGE5KVRb8DW5

Desired Community Node Name:
desireCNname

Desired Access Node Name:
desireANname


Sincerely,
Eric Xample
```
