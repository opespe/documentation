# Access Node Claim Funds Process

OPES Access Nodes are eligible to receive distributions of PE (Personal Equity) based on the Activity generated through the PACTs (Proofs of Activity) they created with Personal Nodes. 

Each Access Node must claim their portion of the distributed PE before it is transferred to their accounts. This is done by sending a "claim funds" action to the OPES Blockchain using the Access Node's Active Key. 

***Note***: *These instructions will be deprecated on August 31st, and will expire September 28th. Check back for updated documentation at those times*  

## References

- [EOS Docker Reference](https://developers.eos.io/eosio-nodeos/docs/docker)

## Prerequisite 

- [Docker](https://www.docker.com/products/docker-desktop) Container Management Software
- Access Node Active Private Key
- [Community Scripts](https://github.com/opespe/community-scripts/)

## Automated Process

This automated script greatly reduces the workload required compared to the [manual process](#manual-process). It is highly recommended to use this automated process, and to only use the manual process when absolutely required. 

A shell script has been provided in the [Community Scripts](https://github.com/opespe/community-scripts/) repo.  

These instructions will be performed through the command line itenrface. 

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

- `<ACCESS_NODE_ACTIVE_KEY>` is the Access Node's Active Private Key in WIF Format. 
- `<ACCESS_NODE_BLOCKCHAIN_NAME>` is the Blockchain ID of the Access Node.

<hr>

**Windows**

On Windows, use PowerShell to run the script using the following command: 

```
./claimfunds.ps1 -account <ACCESS_NODE_BLOCKCHAIN_NAME> -key <ACCESS_NODE_ACTIVE_KEY> -type an
```

<hr>

**Linux**

On Linux, run the script using the following command:

```bash
./claimfunds.sh -a <ACCESS_NODE_BLOCKCHAIN_NAME> -k <ACCESS_NODE_ACTIVE_KEY> -t an
```

<hr>

Follow any instructions that appear on-screen. 

When the script is finished, the Access Node's updated PE balance will be displayed.

## Manual Process  

This manual script greatly increases the workload required compared to the [automated process](#automated-process). It is highly recommended to use the automated process, and to only use the manual process when absolutely required. 

These instructions will be performed through the command line interface.

***NOTE***: If this process is being run on Windows, using PowerShell is <u>required</u>. 

### Create Working Directory

Before starting this process, it is helpful to create a new working directory.

Run 

```bash
mkdir ./opes_working
```

### Create Private Key Files

First, create a file with the Access Node Active Private Key. 

```bash
echo "<ACCESS_NODE_ACTIVE_KEY>" > ./opes_working/an_pk.txt
```

Where `<ACCESS_NODE_ACTIVE_KEY>` is the Access Node's Active Private Key in WIF Format.

Then, create a file with the Claim Funds Private Key. This private key is needed to perform the `claimfunds` action. 

```bash
echo "5JoVPeTasDKTpkKy4Cb3eBEmANS4vczAHyBVr9NUuXcnYENmKHB" > ./opes_working/cf_pk.txt
```

### Share the Working Directory with Docker 

***Note***: On Windows, if Docker Toolbox is installed with VirtualBox, use the following commands to share the hard drive:

```ps
docker-machine stop
$env:mydir = "${pwd}\opes_working"
cd "C:\Program Files\Oracle\VirtualBox"
./VBoxManage sharedfolder add default --name "opes" --hostpath $env:mydir --automount
docker-machine start
cd $env:mydir
```

If using Docker Desktop, use the GUI to share the local drive. 

### Pull OPES Blockchain Image 

Start Docker (or Docker Toolbox) if it is not already running. 

The tools required to interact with the OPES Blockchain are distributed with the Infrastructure Node image on Docker Hub. 

Pull the OPES Infrastructure Node image from Docker Hub 

```bash
docker pull opespe/infranode
```

### Start Blockchain Container

***Note***: On a Windows OS, execute these commands using Windows PowerShell.

***Note***: Ensure that Docker is running 

Next, start the container and mount the local directory using the following command: 

```bash
docker run --rm -it -v "/$(pwd)/opes_working:/mnt/" --entrypoint bash opespe/infranode
```

***Note***: On Windows, the path argument should be `"$(pwd)\opes_working:/mnt/"`

***Note***: If an error `Error response from daemon: invalid mode: /mnt/` occurs on Windows, input the path as the full directory using a lowercase letter and no colon for the drive, e.g. `C:/Users/test/opes_working` becomes `/c/Users/test/opes_working`.

The console should display a prompt similar to the following: 
```bash
root@da743f69d605:/#
```

The shell is now running within the container. 

### Create Environment Variables

For ease of use, the Access Node's Blockchain ID, the Access Node Active Private Key, and the Claim Funds Private Key will be exported to environment variables. Use the following command within the running container:

```bash
export anpk=$(sed "s/[^a-zA-Z0-9]//g" /mnt/an_pk.txt)
export cfpk=$(sed "s/[^a-zA-Z0-9]//g" /mnt/cf_pk.txt)
export anid=<ACCESS_NODE_BLOCKCHAIN_NAME>
```

Where `<ACCESS_NODE_BLOCKCHAIN_NAME>` is the Blockchain ID of the Access Node.

### Start Wallet Service

Start the Wallet Service by running this command in the Blockchain Container:

```bash
keosd &
```

The console should display output similar to the following: 

```bash
info  2019-08-29T02:23:39.661 thread-0  http_plugin.cpp:562           add_handler          ] add api url: /v1/keosd/stop
info  2019-08-29T02:23:39.668 thread-0  http_plugin.cpp:562           add_handler          ] add api url: /v1/node/get_supported_apis
info  2019-08-29T02:23:39.669 thread-0  wallet_api_plugin.cpp:73      plugin_startup       ] starting wallet_api_plugin
info  2019-08-29T02:23:39.671 thread-0  http_plugin.cpp:562           add_handler          ] add api url: /v1/wallet/create
info  2019-08-29T02:23:39.672 thread-0  http_plugin.cpp:562           add_handler          ] add api url: /v1/wallet/create_key
info  2019-08-29T02:23:39.673 thread-0  http_plugin.cpp:562           add_handler          ] add api url: /v1/wallet/get_public_keys
info  2019-08-29T02:23:39.675 thread-0  http_plugin.cpp:562           add_handler          ] add api url: /v1/wallet/import_key
info  2019-08-29T02:23:39.677 thread-0  http_plugin.cpp:562           add_handler          ] add api url: /v1/wallet/list_keys
info  2019-08-29T02:23:39.678 thread-0  http_plugin.cpp:562           add_handler          ] add api url: /v1/wallet/list_wallets
info  2019-08-29T02:23:39.679 thread-0  http_plugin.cpp:562           add_handler          ] add api url: /v1/wallet/lock
info  2019-08-29T02:23:39.680 thread-0  http_plugin.cpp:562           add_handler          ] add api url: /v1/wallet/lock_all
info  2019-08-29T02:23:39.682 thread-0  http_plugin.cpp:562           add_handler          ] add api url: /v1/wallet/open
info  2019-08-29T02:23:39.683 thread-0  http_plugin.cpp:562           add_handler          ] add api url: /v1/wallet/remove_key
info  2019-08-29T02:23:39.685 thread-0  http_plugin.cpp:562           add_handler          ] add api url: /v1/wallet/set_timeout
info  2019-08-29T02:23:39.685 thread-0  http_plugin.cpp:562           add_handler          ] add api url: /v1/wallet/sign_digest
info  2019-08-29T02:23:39.686 thread-0  http_plugin.cpp:562           add_handler          ] add api url: /v1/wallet/sign_transaction
info  2019-08-29T02:23:39.687 thread-0  http_plugin.cpp:562           add_handler          ] add api url: /v1/wallet/unlock
```

If the terminal remains in the process, press `ctrl + c` to exit. 

#### Verify

Test that the Wallet Service is running using the following command:

```bash
cleos wallet list
```

You should see output similar to the following:

```bash
Wallets:
[]
```

### Create a Wallet

Create a wallet to store your private keys using the following command:

```bash
cleos wallet create --file ./my_wallet
```

The console output should be similar to the following:

```bash
warn  2019-08-30T17:12:40.265 thread-0  wallet.cpp:223                save_wallet_file     ] saving wallet to file /root/eosio-wallet/./default.wallet
Creating wallet: default
Save password to use in the future to unlock this wallet.
Without password imported keys will not be retrievable.
saving password to ./my_wallet
```

### Add Private Keys

Next, import the Access Node Active Private Key into the Wallet Service using the following command from within the Blockchain Container:

```bash
cleos wallet import --private-key ${anpk} --name default
```

Then, import the Claim Funds Private Key into the Wallet Service using the following command from within the Blockchain Container:

```bash
cleos wallet import --private-key ${cfpk} --name default
```

For both of those commands, the output should be similar to the following:

```bash
warn  2019-08-30T17:15:20.959 thread-0  wallet.cpp:223                save_wallet_file     ] saving wallet to file /root/eosio-wallet/./default.wallet
imported private key for: EOS6s3pDZmpUVzAtfARXPe4pd5iXW1ULF58L85RfEaXv9FSF36abd
```

#### Verify

Test that the Wallet Service updated using the following command:

```bash
cleos wallet keys
```

The newly added Private Keys should be listed in their Public Key form in the output, similar to below: 

```bash
[
  "EOS54aFGa474gUVzAtfARMMe4pd5oPW2KLF58L85RfEaCn3SF36af"
  "EOS6s3pDZmpUVzAtfARXPe4pd5iXW1ULF58L85RfEaXv9FSF36abd"
]
```

### Check Current Account Balance

Run the following command to determine the Access Node's current balance in PE:

```bash
cleos -u http://pub-infra.opesx.io get currency balance eosio.token ${anid} PE
```

Note the output as the starting balance.


### Submit Action

Submit the claim funds action to the OPES Blockchain using the following command:

```bash
cleos -u http://pub-infra.opesx.io push action eosio claimfunds "'{\"kind\":\"an\", \"nodename\":\"${anid}\"}'" -p ${anid}@active eosio@claimfunds
```

The console output should be similar to the following: 

```
executed transaction: d6acb4fd44a387e839934690c4425673c8a79cae80d4f10ea1f544bbac38eab5  144 bytes  127389 us
#         eosio <= eosio::claimfunds            {"kind":"an","nodename":"antstr111111"}
#   eosio.token <= eosio.token::transfer        {"from":"eosio","to":"antstr111111","quantity":"15.0000 PE","memo":"pay to antstr111111"}
#         eosio <= eosio.token::transfer        {"from":"eosio","to":"antstr111111","quantity":"15.0000 PE","memo":"pay to antstr111111"}
#  antstr111111 <= eosio.token::transfer        {"from":"eosio","to":"antstr111111","quantity":"15.0000 PE","memo":"pay to antstr111111"}
warning: transaction executed locally, but may not be confirmed by the network yet         ]
```

#### Verify

Run the following command to verify the transaction succeeded:

```bash
cleos -u http://pub-infra.opesx.io get currency balance eosio.token ${anid} PE
```

***Note***: It may take several seconds for the transaction to propagate throughout the network. If the Access Node's balance does not update immediately, try again every few seconds until it does. If the balance is not updated after several minutes, ensure that the Access Node is set to receive a distribution, return to the [Submit Action](#submit-action) section, and attempt to send the transaction again. 
