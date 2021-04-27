# Validation Special Topic


## How to run validator node

Running the validation node takes a lot of responsibility! You are responsible not only for the ECO that you have staked, but also for the ECO that your nominator has staked. If you make a mistake and are punished, your money and your reputation will be in jeopardy. But running the validator node also has a very significant payoff, as you contribute to the security of the blockchain network and make the network more decentralized.


1. Minimum staking requirement


In order to be a validator, the minimum staking ECO must meet the requirements, but this minimum staking is dynamic and changes over time. It depends not only on how many staking are behind each validator, but also on the size of the set of active validators and how many validators are waiting in the pool. The minimum staking may be ECO held by the validator himself or may include ECO held by the nominator. This means that the validator must at least have enough ECO to bind the wallet and pay the additional transaction fees, and then the rest can come from the nominator.


2. Node server configuration

To become a validator, you must run the validator node. The validator node is usually a server, which can be a cloud server or can be configured to manage and maintain a server by itself. The operating system recommended by the node server is Linux, and users can choose their favorite operating system. 

The standard hardware configuration requirements are as follows:

- CPU：Intel(R) Core(TM) i7-7700K CPU @ 4.20GHz
- RAM：64G
- DISK：SSD is recommended, starting at 1T, and plans for future data growth and expansion are required.

The configuration here is not the minimum configuration, but if the configuration is too low, the efficiency of the validator node software operation may be affected.

3. Install Rust runtime environment

The underlying system of EcoBall blockchain is developed in Rust language, so the Rust environment needs to be configured on the node server.

If the node has never installed Rust, you should execute the following command first, and the latest version of Rust will be downloaded and installed.

````
curl https://sh.rustup.rs -sSf | sh
````

If you have already installed Rust, you need to run the following command to ensure that you are using the latest version.

````
rustup update
````

If Rust has been installed or updated, you also need to install the associated dependencies.

````
sudo apt install make clang pkg-config libssl-dev build-essential
````

If you are using OSX and have Homebrew installed, you can execute the command:

````
brew install cmake pkg-config openssl git llvm
````


4. Configure Network Time Protocol

NTP is a network protocol used to synchronize computer clocks over the network. The validator node server needs to synchronize the computer clock to keep the time consistent with other nodes on the network. Therefore, it is necessary to run NTP or similar services.

If the node server is running Ubuntu 18.04 or later, the NTP client should be installed by default. It can be detected by the following command:

````
timedatectl
````

If NTP is installed and running, you should see System clock synchronized: yes (or a similar message). 

If you can't see it, you can install it by executing the following command:

````
sudo apt-get install ntp
````

ntpd will start automatically after installation. You can query ntpd for status information to verify that everything is normal:

````
sudo ntpq -p
````

5. Install EcoBall node software

**To be continued**

6. Synchronize block data

**To be continued**

7. Bind ECO

Set up a wallet, bind a sufficient amount of ECO, as a staked deposit as a related business processing account.

**To be continued**

8. Turn on the validator

**To be continued**



## How to validate?

**To be continued**

