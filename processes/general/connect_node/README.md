# How to Setup a Node and Connect to the OPES Blockchain

This document describes the process to connect to the OPES Blockchain via the managed Infrastructure Nodes using a provided Docker image. 

## Prerequisite 

- [Docker](https://www.docker.com/products/docker-desktop) Container Management Software
  - ***Note***: Windows Home and legacy Windows users will need to use [Docker Toolbox](https://docs.docker.com/toolbox/toolbox_install_windows/) instead 

## Create Working Directory

Before starting this process, it is helpful to create a working directory where files can be placed from the local machine and will be made accessible to the Docker instance. If a working directory has not yet been created, do so now. 

Run 

```bash
mkdir ./opes_working
```

## Create Private Key Files

Most processes require the use of a Private Key. To facilitate easier input into the required scripts, copy any necessary Private Keys into the working directory. 

For example, the following command may be used:
```bash
echo "<PRIVATE_KEY>" > ./opes_working/<PRIVATE_KEY_FILENAME>
```

Where 
- `<PRIVATE_KEY>` is the Private Key in WIF Format
- `<PRIVATE_KEY_FILENAME>` is the desired file name for the Private Key file

Repeat this process for each unique key/filename pair. 

## Pull OPES Blockchain Image 

Start Docker (or Docker Toolbox) if it is not already running.  

The tools required to interact with the OPES Blockchain are distributed with the Infrastructure Node image on Docker Hub. 

Pull the OPES Infrastructure Node image from Docker Hub 

```bash
docker pull opespe/infranode
```

## Start Blockchain Container

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

## Create Environment Variables

To reduce the likelihood of input errors, export any Private Keys from the working directory as environment variables using the following command:

```bash
export <PRIVATE_KEY_ENVVAR>=$(sed "s/[^a-zA-Z0-9]//g" /mnt/<PRIVATE_KEY_FILENAME>)
```

Where
- `<PRIVATE_KEY_ENVVAR>` is the desired environment variable to hold the data
- `<PRIVATE_KEY_FILENAME>` is the desired file name for the Private Key file

Repeat the command for each key. 

## Start Wallet Service

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

### Verify

Test that the Wallet Service is running using the following command:

```bash
cleos wallet list
```

You should see output similar to the following:

```bash
Wallets:
[]
```

## Create a Wallet

You will need to create a wallet to store your private keys using the following command:

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

## Add Private Keys

Next, import the Community Node Active Private Key into the Wallet Service using the following command from within the Blockchain Container:

```bash
cleos wallet import --private-key ${<PRIVATE_KEY_ENVVAR>} --name default
```

Where
- `<PRIVATE_KEY_ENVVAR>` is the previously created environment variable holding the Private Key

Repeat for each Private Key that needs to be inported. 

Each time the command is executed, the output should be similar to the following:

```bash
warn  2019-08-30T17:15:20.959 thread-0  wallet.cpp:223                save_wallet_file     ] saving wallet to file /root/eosio-wallet/./default.wallet
imported private key for: EOS6s3pDZmpUVzAtfARXPe4pd5iXW1ULF58L85RfEaXv9FSF36abd
```

### Verify

Test that the Wallet Service updated using the following command:

```bash
cleos wallet keys
```

The newly added Private Keys should each be listed in their Public Key form in the output, similar to below: 

```bash
[
  "EOS54aFGa474gUVzAtfARMMe4pd5oPW2KLF58L85RfEaCn3SF36af"
]
```

## Complete Process

The process is now complete. The container is ready to perform the next command. 
