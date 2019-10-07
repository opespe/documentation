# Enrolling A Community Node 

Welcome to OPES! We are glad that you have decided to enroll as a Community Node!
Complete the instructions below, and you will be enrolled shortly. 

**This process is only available for pre-approved accounts. To request approval, contact [support@opes.one](mailto:support@opes.one)**

**Note**: *These instructions are deprecated and will expire on October 1st, 2019. A new enrollment process will be implemented at that time.*

## <u>Version 1.2.0</u>

## Key Generation & Signup

This process will generate the public/private key-pairs that will control a new Community Node, associated Access Node, and associated Infrastructure Node. It will also generate an email which can be sent to OPES One to request account creation.

### 1: Navigate to Keygen Website

Using a modern web browser (i.e. Chrome, Firefox, Safari, or Edge), navigate to the [OPES Key Generation Website](https://keygen.opesx.io)

### 2: Create Account Names

Create an account name to represent the Community Node account on the OPES blockchain. This name cannot be changed later and will be visible to other users, so choose wisely.

**<u>Account Naming Rules</u>**

**Note**: Requested names that violate these rules will be rejected. In
    addition, names containing profanity or offensive language will be rejected.

- The account name must be between one (1) and twelve (12) characters.
- The account name may use any lowercase letter from a-z, the numbers 1-5, and period (".").
- The account name must not end with a period ("."). 

### 3: Complete Signup Form

Completely fill out the signup form with the following information:
- **Contact Name**: The name of the individual responsible for the Community Node
- **Contact Email Address**: An active, valid email address that OPES Admins can use to communicate with the Community Node owner
- **Desired Community Node Name**: The Community Node blockchain account name created in the previous step.
- **Nominating Personal Node Name**: The blockchain account name of the existing Nominating PN.
- **Nominating Community Node Name**: The blockchain account name of the existing Nominating CN.
- **Community Info URL**: A URL that defines the hosting location for the [Community Node's Info File](https://github.com/opespe/documentation/tree/master/processes/community/deployment/community_info_spec.md)

#### Errors
Validation errors will be highlighted in red, and instructions will be provided on the form field's requirements. The form cannot be submitted until all fields are validated. Correct any errors before continuing.

### 4: Generate Keys

Once the form has been completely filled out with no validation errors, click the `Generate OPES Keys` button.


   The page will automatically generate four public/private key pairs. These key pairs can be thought of as a lock and key for encryption and authorization. The public key is the lock, and the private key is the key. 

   **Note on Identifying Key Types:** 
   - Public Keys (which can be distributed) start with the prefix `OPES`.
   - Private Keys (which ***must*** be kept secret) do not have a defined prefix.
   The key pairs that will be generated are:

  - <u>Community, Access, and Infrastructure Node Owner Key Pair</u>
    - This is the primary key pair for the new Community, Access, and Infrastructure Nodes' accounts, and will have total control over the new accounts' security. Store it safely!
    - **WARNING: There is absolutely _NO WAY_ to recover the Community, Access, or Infrastructure Node's account if the Owner Private Key is lost or compromised!**
    - **WARNING**: The Owner Private Key will be able to transfer funds, update the account's Active Key, and perform other highly secure tasks for the Community, Access, and Infrastructure Nodes. *DO NOT DISTRIBUTE THE OWNER PRIVATE KEY*
    - **NOTE**: The Owner keys for each account may be updated later to use separate keys for more granular access control. 

  - <u>Community, Access, and Infrastructure Node Active Key Pair</u>
    - This key pair provides direct access to the Community, Access, and Infrastructure Nodes' accounts on-chain. Store it safely, in the same manner as the Owner Key!
    - **WARNING**: The Active Private Key will be able to transfer funds and perform other secure tasks for the Community, Access, and Infrastructure Nodes. *DO NOT DISTRIBUTE THE ACTIVE PRIVATE KEY*
    - **NOTE**: This key will be used for the majority of on-chain actions. In situations calling for an account's Private Key, it almost always refers to the Active Private Key. 
    - **NOTE**: The Active keys for each account may be updated later to use separate keys for more granular access control. 

  - <u>Access Node Work Key Pair</u>
    - This key pair has restricted permissions and is only used to sign Proof of Activity tallies from Personal Nodes. 
    - This key pair may be safely provided to third parties (e.g. a cloud service provider) to allow them to run the new Access Node's Proof of Activity tally signing service without exposing the keys for the Access Node's account
    - **NOTE**: The Work keys for an account may be updated to allow key rotation schedules, however only one Work key will be viable at any given time. 

  - <u>Infrastructure Node Work Key Pair</u>
    - This key pair has restricted permissions and is only used to perform block production from the Infrastructure Node. 
    - This key pair may be safely provided to third parties (e.g. a cloud service provider) to allow them to run the new Infrastructure Node's block production and availability service without exposing the keys for the Infrastructure Node's account
    - **NOTE**: The Work keys for an account may be updated to allow key rotation schedules, however only one Work key will be viable at any given time.


### 5: Print and Save Keys

The new keys must be stored safely, ideally in multiple secure locations (e.g. safety deposit box, safe). To continue, click the `Print` button immediately below your keys and print a hard copy of the keys.

### 6: Send Signup Email
A prepopulated email will automatically appear after the `Print` dialog is completed. Click the `Open Email Client (mailto:)` link to open the email in the default email client. Alternatively, the displayed email, recipient email address, and required subject line can be copy/pasted into an email client. Review the message for accuracy, then send it. 

## Finishing Up

Once the signup email has been received, the OPES team will verify and enroll your Community Node. Upon successful enrollment, the OPES team will contact you and provide additional account information, such as the infrastructure access keys to allow the new Infrastructure Node to connect to the OPES-managed Infrastructure Nodes.
## Info Service Creation (OPTIONAL)
To incorporate OPES with a community, a specific endpoint must be provided which supplies information about that community. The [CN Info Service](https:/github.com/opespe/documentation/tree/master/processes/community/deployment/README.md) must be at an externally accessible location so OPES can find it. Note the fully qualified URL (e.g. `https://access.example-org.com`) as `Community Info URL`.
**NOTE**: The `CN Info Service` does not need to be deployed to complete this process, only for the Community Node's information to be properly displayed to OPES users. Deploying the CN Service may be skipped as long as the future `Community Info URL` is known.   
