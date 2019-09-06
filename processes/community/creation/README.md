
# Community Node Creation

Community Nodes can be created by purchasing a Community Node License on the OPES Blockchain for 3838 PE.
To bootstrap the Community Node network, there will be 20 Community Nodes granted the ability to acquire
50 Keys each that they can use to create 50 Community Node.
These new created CN's are tracked through a unique token, an asset within the OPES Blockchain.
Creating a CN with this unique token will expend the token from the system.

To be considered for one of the 20 Community Nodes that can help bootstrap the Community Node Network,
contact the OPES.ONE at support@opes.one

## References

- [eosio Docker Reference](https://developers.eos.io/eosio-nodeos/docs/docker)

## Prerequisite 

- [Docker](https://www.docker.com/products/docker-desktop) Container Management Software
- Community Node Active Private Key


## Obtaining Signup Info 

When a prospective Community Node wants to join OPES through an existing Community Node, they will send an email with their signup information to the existing Community Node. The email will have content similar to the following: 


```
From: example@newcommunity.io
To: example@existingcn.io
Subject: OPES Community Node Enrollment

Hello,

Here are the details for the Community Node I wish to enroll. Thanks in advance!

---

Community Node Name:
desireCNname

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

## Creating the New Community Node Account On-Chain

In order for the prospective Community Node to create their account on-chain, a nominating CN must call the `onboard` action in the CN Onboarding Contract.


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

- `<COMMUNITY_NODE_BLOCKCHAIN_NAME>` is the Blockchain ID of the enrolling Community Node.
- `<COMMUNITY_NODE_ACTIVE_KEY>` is the enrolling Community Node's Active Private Key in WIF Format. 
- `<REFERRING_PN_ACCOUNT>` is the Blockchain ID of the Personal Node account corresponding to the existing Community Node, or another PN account that should receive referral bonuses from this new CN.
- `<NEW_CN_NAME>` is the Blockchain ID of the prospective Community Node.
- `<NEW_CN_INFO_SERVICE_URL>` is the "Community Info URL" of the new CN as provided in the signup email
- `<NEW_CN_OWNER_PUBLIC_KEY>` is the "Community Node Owner Public Key" of the new CN as provided in the signup email
- `<NEW_CN_ACTIVE_PUBLIC_KEY>` is the "Community Node Active Public Key" of the new CN as provided in the signup email
- `<NEW_AN_WORK_PUBLIC_KEY>` is the "Access Node Work Public Key" of the new CN as provided in the signup email
- `<NEW_IN_WORK_PUBLIC_KEY>` is the "Infrastructure Node Work Public Key" of the new CN as provided in the signup email



<hr>

**Windows**

Windows currently does not have support for the automated process. Follow the [manual process](#manual-process) instead. 

<hr>

**Linux**

On Linux, run the script using the following command:

```bash
./createcn.sh -c <COMMUNITY_NODE_BLOCKCHAIN_NAME> \
 -k <COMMUNITY_NODE_ACTIVE_KEY> \
 -p <REFERRING_PN_ACCOUNT> \
 -n <NEW_CN_NAME> \
 -u <NEW_CN_INFO_SERVICE_URL> \
 -o <NEW_CN_OWNER_PUBLIC_KEY> \
 -a <NEW_CN_ACTIVE_PUBLIC_KEY> \
 --an <NEW_AN_WORK_PUBLIC_KEY> \
 --in <NEW_IN_WORK_PUBLIC_KEY>
```

<hr>

Follow any instructions that appear on-screen. 

When the script is finished, the updated Community Node Table info will be displayed. 

## Manual Process  

These instructions will be performed through the command line interface. 

### Create Working Directory

Before starting this process, it is helpful to create a new working directory.

Run 

```bash
mkdir ./opes_working
```

### Create Public Key Files

Create files with the Public Keys provided by the prospective Community Node.

```
echo "<NEW_CN_OWNER_PUBLIC_KEY>" > ./opes_working/ncn_opk.txt
echo "<NEW_CN_ACTIVE_PUBLIC_KEY>" > ./opes_working/ncn_apk.txt
echo "<NEW_IN_WORK_PUBLIC_KEY>" > ./opes_working/nin_wpk.txt
echo "<NEW_AN_WORK_PUBLIC_KEY>" > ./opes_working/nan_wpk.txt
echo "<NEW_CN_INFO_SERVICE_URL>" > ./opes_working/info_url.txt
```

Where 
- `<NEW_CN_OWNER_PUBLIC_KEY>` is the "Community Node Owner Public Key" of the new CN as provided in the signup email
- `<NEW_CN_ACTIVE_PUBLIC_KEY>` is the "Community Node Active Public Key" of the new CN as provided in the signup email
- `<NEW_IN_WORK_PUBLIC_KEY>` is the "Infrastructure Node Work Public Key" of the new CN as provided in the signup email
- `<NEW_AN_WORK_PUBLIC_KEY>` is the "Access Node Work Public Key" of the new CN as provided in the signup email

### Create Private Key Files

Create a file with the Community Node Active Private Key in the new working directory. 

```bash
echo "<COMMUNITY_NODE_ACTIVE_KEY>" > ./opes_working/cn_pk.txt
```

Where `<COMMUNITY_NODE_ACTIVE_KEY>` is the Community Node's Active Private Key in WIF Format.

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

The tools required to interact with the OPES Blockchain are distributed with the Infrastructure Node image on Docker Hub. 

Pull the OPES Infrastructure Node image from Docker Hub 

```bash
docker pull opespe/infranode
```

### Start Blockchain Container

***Note***: If using a Windows OS, these commands must be executed using Windows PowerShell.

***Note***: Ensure that Docker is running 

Next, start the container and mount the local directory using the following command: 

```bash
docker run --rm -it -v "/$(pwd)/opes_workdir:/mnt/" --entrypoint bash opespe/infranode
```

***Note***: On Windows, the path argument should be `"$(pwd)\opes_working:/mnt/"`

***Note***: If an error `Error response from daemon: invalid mode: /mnt/` occurs on Windows, input the full directory using a lowercase letter and no colon for the drive, e.g. `C:/Users/test/opes_working` becomes `/c/Users/test/opes_working`.

The console should display a prompt similar to the following: 

```bash
root@da743f69d605:/#
```

The shell is now running within the container. 

### Create Environment Variables

For ease of use, the enrolling Community Node's Blockchain ID, the Community Node Active Private Key, and the prospective Community Node's provided info will be exported to environment variables. Use the following commands within the running container:

```bash
export cnpk=$(sed -e "s/[^a-zA-Z0-9]//g" /mnt/cn_pk.txt)
export ncnopk=$(sed -e "s/[^a-zA-Z0-9]//g" -e "s/OPES/EOS/gi" /mnt/ncn_opk.txt)
export ncnapk=$(sed -e "s/[^a-zA-Z0-9]//g" -e "s/OPES/EOS/gi" /mnt/ncn_apk.txt)
export ninwpk=$(sed -e "s/[^a-zA-Z0-9]//g" -e "s/OPES/EOS/gi" /mnt/nin_wpk.txt)
export nanwpk=$(sed -e "s/[^a-zA-Z0-9]//g" -e "s/OPES/EOS/gi" /mnt/nan_wpk.txt)
export cnurl=<NEW_CN_INFO_SERVICE_URL>
export cnid=<COMMUNITY_NODE_BLOCKCHAIN_NAME>
export ncnid=<NEW_CN_NAME> 
export rpnid=<REFERRING_PN_ACCOUNT>

```

Where 
- `<NEW_CN_INFO_SERVICE_URL>` is the "Community Info URL" of the new CN as provided in the signup email
- `<COMMUNITY_NODE_BLOCKCHAIN_NAME>` is the Blockchain ID of the enrolling Community Node.
- `<NEW_CN_NAME>` is the Blockchain ID of the prospective Community Node.
- `<REFERRING_PN_ACCOUNT>` is the Blockchain ID of the Personal Node account corresponding to the existing Community Node, or another PN account that should receive referral bonuses from this new CN.


### Start Wallet Service

Start the Wallet Service by running this command in the Blockchain Container:

```bash
keosd &
```

You should see output similar to the following: 

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

### Create a wallet

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

Next, import the Community Node Active Private Key into the Wallet Service using the following command from within the Blockchain Container:

```bash
cleos wallet import --private-key ${cnpk} --name default
```

The output should be similar to the following:

```bash
warn  2019-08-30T17:15:20.959 thread-0  wallet.cpp:223                save_wallet_file     ] saving wallet to file /root/eosio-wallet/./default.wallet
imported private key for: EOS6s3pDZmpUVzAtfARXPe4pd5iXW1ULF58L85RfEaXv9FSF36abd
```

#### Verify

Test that the Wallet Service updated using the following command:

```bash
cleos wallet keys
```

The newly added Private Key should be listed in the output in its Public Key form, similar to below: 

```bash
[
  "EOS54aFGa474gUVzAtfARMMe4pd5oPW2KLF58L85RfEaCn3SF36af"
]
```

### Check Number of Tickets Remaining

Run the following command to determine the number of tickets an account controls:

```bash
cleos -u http://pub-infra.opesx.io get currency balance eosio.token ${cnid} CNONBRD
```

Note the output.

### Submit onboard Action

Submit the create cn action to the OPES Blockchain using the following command:

```bash
cleos -u http://pub-infra.opesx.io push action cn.onboarder onboard "{\"payment\":\"1 CNONBRD\",\"creator\":\"${cnid}\",\"name\":\"${ncnid}\",\"owner\":\"${ncnopk}\",\"active\":\"${ncnapk}\",\"referpn\":\"${rpnid}\",\"resourcedesc\":\"${cnurl}\",\"producer_key\":\"${ninwpk}\",\"location\":1,\"an_key\":\"${nanwpk}\"}" -p ${cnid}@active
```

#### Verify

Run the following command to determine the number of remaining tickets the account controls:

```bash
cleos -u http://pub-infra.opesx.io get currency balance eosio.token ${cnid} CNONBRD
```

Run the following command to check the Community Node Tables for the new Community Node: 

```bash
cleos -u http://pub-infra.opesx.io get table -L ${ncnid} -l 50 eosio eosio o1cnodes | jq -r ".rows[] | select (.community_node == \"${ncnid}\")
```


***Note***: It may take several seconds for the transaction to propagate throughout the network. If the Community Node table does not update immediately, try again every few seconds until it does. If the table is not updated after several minutes, return to the [Submit "onboard" Action](#submit-onboard-action) section, and attempt to send the transaction again. 
