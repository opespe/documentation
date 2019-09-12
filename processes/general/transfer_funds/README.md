# OPES Transfer Funds

This process will transfer an OPES asset from one account to another. 

## Prerequisites

- [Docker](https://www.docker.com/products/docker-desktop) Container Management Software
  - ***Note***: Windows Home and legacy Windows users will need to use [Docker Toolbox](https://docs.docker.com/toolbox/toolbox_install_windows/) instead 
- OPES Blockchain Account's Active Private Key

## Automated Process

This automated script greatly reduces the workload required compared to the [manual process](#manual-process). It is highly recommended to use this automated process, and to only use the manual process when absolutely required. 

A shell script has been provided in the [Community Scripts](https://github.com/opespe/community-scripts/) repo.  

These instructions will be performed through the command line interface. 

***NOTE***: If this process is being run on Windows, using PowerShell is <u>required</u>. 

### Download Scripts

Download the [Community Scripts](https://github.com/opespe/community-scripts/) repository to the local directory. 
If Git is installed, it may be used to download the repository with the following command:

```bash
git -c core.autocrlf=false clone https://github.com/opespe/community-scripts.git

``` 

Next, navigate to the root folder of the repository. If the repository was cloned with Git, use this command to navigate: 

```bash
cd ./community-scripts
```

### Execute Script 

Start Docker (or Docker Toolbox) if it is not already running.  

Use the appropriate values to replace these fields in each command:

- `<SENDER_NAME>` is the Blockchain ID of the sender.
- `<ACTIVE_KEY>` is the sender's Active Private Key in WIF Format. 
- `<RECIPIENT_NAME>` is the Blockchain ID of the recipient.
- `<AMOUNT>` is the amount of the asset to transfer
- `<CURRENCY>` is the name of the asset to transfer (default "PE")

<hr>

**Windows**

On Windows, use PowerShell to run the script using the following command: 

```
./transfer-tokens.ps1 -Sender <SENDER_NAME> -Key <ACTIVE_KEY> -Recipient <RECIPIENT_NAME> -Amount <AMOUNT> -Token <CURRENCY>
```

<hr>

**Linux**

On Linux, run the script using the following command:

```bash
./transfer-tokens.sh -s <SENDER_NAME> -k <ACTIVE_KEY> -t <RECIPIENT_NAME> -a <AMOUNT> -t <CURRENCY>
```

<hr>

Follow any instructions that appear on-screen. 

When the script is finished, the account's updated token balance will be displayed.

## Manual Process  

This manual script greatly increases the workload required compared to the [automated process](#automated-process). It is highly recommended to use the automated process, and to only use the manual process when absolutely required. 

These instructions will be performed through the command line interface.

***NOTE***: If this process is being run on Windows, using PowerShell is <u>required</u>. 

### Setup Blockchain Container

Complete the process outlined [here](../connect_node/README.md).

Be sure to import the OPES Blockchain Account's Active Private Key to the Wallet Service as described in that process. 

### Check Current Balance

Before sending any transaction, check the account's available balance with the following command: 

```bash
cleos get currency balance eosio.token <ACCOUNT_NAME> <CURRENCY>

```

Where
- `<ACCOUNT_NAME>` is the Blockchain ID of the account whose balance will be queried
- `<CURRENCY>` is the name of the asset to query 

### Send Transfer Transaction

Execute the following command to send the transfer transaction:

```bash
cleos transfer <SENDER_NAME> <RECIPIENT_NAME> -c eosio.token "<AMOUNT> <CURRENCY>" "<MESSAGE>"
```

Example:
```bash
cleos transfer examplecn1 examplepn1 -c eosio.token "1.0000 PE" "Hello, World"
```
 
- `<SENDER_NAME>` is the Blockchain ID of the sender.
- `<RECIPIENT_NAME>` is the Blockchain ID of the recipient.
- `<AMOUNT>` is the amount of the asset to transfer
- `<CURRENCY>` is the name of the asset to transfer (default "PE")
- `<MESSAGE>` is an optional memo to send


The output should look similar to: 

```
executed transaction: ac989464a987e9061d4eabdfad0e5707a23ba769798a01f3ce010c5b3775b554  128 bytes  490 us
```

### Verify

To verify that the transfer succeeded, check the sender and recipient account's balance using the same process as in the [Check Balance](#check-current-balance) section. 
