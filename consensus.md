# Consensus mechanism

EcoBall adopts the hybrid consensus mechanism of GPOW+XPOS. It fully combines the outstanding characteristics of the proof of work and the proof of stakes consensus mechanism, takes into account fairness and efficiency, and strives to balance the interests of all participants, increase participation and transparency, improve system efficiency, and meet commercial needs.


GPOW is the optimization and improvement of ProgPoW consensus algorithm by EcoBall based on its own architecture design, but most of the design ideas and algorithms have not changed, and it still follows the original design. So the following will focus on the ProgPoW consensus algorithm.



XPOS was inspired by the Nomination Proof of Stake (NPOS), combined with EcoBall's strategic vision, EcoBall carried out tailoring, arrangement, and reorganization in line with its own requirements. The specific details will be explained one by one in the following introduction. Before that, the NPOS consensus mechanism will also be introduced in detail.

## ProgPOW arithmetic

ProgPoW is a proof-of-work algorithm, which is the abbreviation of "Programmatic Proof-of-Work", which aims to narrow the efficiency gap with dedicated ASIC. It utilizes almost all parts of commercial hardware (GPU), and has been tuned in advance for the most common hardware used in the Ethereum network, and has been specially designed to try to weaken the advantages of ASIC mining machines. Simply put, ProgPoW is an extension of the Ethereum mining algorithm Ethash after GPU tuning, which can defend against ASIC miners.

Since the release of the first Bitcoin mining ASIC, many new proof-of-work algorithms have emerged, all aimed at "Anti-ASIC". The purpose of the so-called "Anti-ASIC" is to resist the centralization of PoW mining power and prevent the tokens using this type of algorithm from being manipulated by a small number of players.

The basic principle of ProgPow is the same as that of PoW, both are proof of work, and the amount of computing power determines the amount of profit. Although the PoW mechanism is fair, mining machine manufacturers and miners are constantly looking for more efficient mining shortcuts to compete, so GPU mining machines and ASIC mining machines were born.

Ethereum currently uses the Ethash algorithm, which has not been compromised by ASIC miners for a long time. GPU mining has been the mainstream in these years. However, recently it has been revealed that ASIC mining machines that can mine Ethereum are available. Its computing power is significantly better than GPU mining machines. The existing mining balance will be broken, and the computing power is likely to be concentrated in the hands of a few miners holding a large number of ASIC mining machines.  Ethereum will face a centralization problem.

In the Ethereum community, the voices against ASICs is roaring, and the ProgPow consensus algorithm was born under this situation. ProgPoW does not bring higher efficiency. On the contrary, it limits the computing power of ASIC miners, making it equal to GPU miners. In other words, ProgPow is a performance suppressor for ASIC miners.

Ecoball comprehensively inspected the current market GPU mining technical solutions and algorithms, and chose ProgPow as the underlying mining algorithm, trying to be more decentralized, more users-friendly, and fairer.

### ProgPOW build and test

First clone the code from github, then compile and build

````  

git clone https://github.com/ifdefelse/ProgPOW
cd ProgPOW
git submodule update --init --recursive
mkdir build
cd build
cmake .. -DETHASHCUDA=ON
make -sj8

````

Then use CUDA and OpenCL to perform benchmark tests, and the command is similar to the following:

````
ethminer/ethminer -U -M 10000000
ethminer/ethminer -G -M 10000000
````

### ProgPOW arithmetic overview

The design goal of ProgPoW is to match the requirements of the algorithm with that of the ordinary GPU: if the algorithm is implemented on a custom ASIC, the efficiency improvement is not large compared with the ordinary GPU.

The main features of the algorithm are:

- Change Keccak_F1600 (64 bits) to Keccak_F800 (32 bits) to reduce the impact on overall force
- Increases the mixing state
- Add a random math sequence to the main loop
- Added small-scale, low-latency cache reading that supports random addresses
- Increased DRAM (Dynamic Random Access Memory) from 128 bytes to 256 bytes

Although ASIC can also deploy this code, it does little to help in terms of efficiency. Most graphics cards need to support these features.

The only optimizable part is:

- Removed graphics pipes (display, geometry engine, surface texture, etc.)
- Removed floating point math
- Some ISA adjustments, such as instructions that exactly match the merge() function

This will increase the efficiency by approximately 1.1-1.2 times. This is much less than 2 times of Ethash or 50 times of Cryptonight.

### Basic principles of standard hardware PoW

With the continuous development of large mining pools, a small number of mining pools control a large amount of computing power, because only by joining these mining pools can small miners obtain more stable economic benefits. Although some people believe that large centralized mining pools defeat the purpose of "Anti-ASIC", it is important that ASIC-based currencies are actually more centralized. 

The reasons are as follows:

1. No natural distribution: In addition to mining, this type of professional hardware has no other economic uses, so most people will not own this type of hardware.

2. No backup organization: When prices are volatile and easily manipulated, there is no backup hardware or stakeholders who can enter the market.

3. High threshold: The early miners are those who are rich enough to invest funds and ecological resources in unknown new tokens. Therefore, the initial distribution of tokens through mining has limitations, which may cause "economic bias" in centralization.

4. Entrusted centralization VS deployment centralization: Although the centralization of the mining pool is caused by user entrustment, the simplification of hardware is not: only specific buyers of this hardware can participate in mining, so it is impossible to take control of the mining pool in a short time.

5. Even with decentralized mining, it is difficult to achieve decentralized control: once large customized ASIC manufacturers participate, designing backdoor hardware becomes meaningless. Ensuring transparency and fairness in the market does not do any good to ASIC manufacturers.

Although the goal of "Anti-ASIC" is very valuable, the whole concept of "Anti-ASIC" is a bit absurd. The CPU (central processing unit) and GPU (graphics processing unit) themselves are ASIC. In theory, any algorithm that can be run on a commercial ASIC (CPU or GPU) can create a customized ASIC with fewer features. Some algorithms are even deliberately designed to be "ASIC-friendly"-the mining efficiency after ASIC deployment is much higher than similar algorithms running on ordinary hardware. This phenomenon is extremely attractive to professional ASIC mining machine manufacturers.

Therefore, ASIC resistance refers to the efficiency gap between professional hardware and hardware with higher popularity and application. The smaller the efficiency difference between custom and general-purpose hardware, the stronger the resistance and the better the algorithm. This efficiency gap is a reasonable standard to measure the quality of the PoW algorithm. Efficiency means absolute performance, efficiency-to-power ratio or cost-effectiveness-these points are all highly correlated. If a company produces and controls an extremely efficient ASIC, then they can control 51% of the network's computing power, and it is very likely to launch an attack.

### Major PoW algorithms

#### SHA256

- Potential efficiency increase of approximately 1000x after deployment of ASIC

The SHA algorithm is a series of simple mathematical operations-addition, logical operations, and twiddle operation. Processing single-point operations on the CPU or GPU requires acquiring and decoding an instruction, reading data from the register file, executing the instruction, and then writing the result back to the register file. This process requires a lot of time and resources.

A small number of transistors and wires are required to implement single-point operations in an ASIC. This means that each operation consumes very little power, space, or time. The hashing core can be constructed by listing the sequence of required operations. This hash core can execute a sequence of operations in a short time and consumes less power and space compared with CPU and GPU. Bitcoin ASICs consist of many identical hash cores and some minimal off-chip communications.

#### Scrypt and NeoScrypt

- Potential efficiency increase of approximately 1000x after deployment of ASIC

In terms of algorithms and bit operations, Scrypt and NeoScrypt are similar to SHA. Unfortunately, for tokens using this type of algorithm, such as Litecoin, their PoW mining algorithm only uses a temporary register with a capacity between 32kb and 128kb. This register has a very small capacity and is very suitable for ASICs. Therefore, the ASIC deployment of this algorithm is similar to SHA, which will result in a significant increase in efficiency.

#### X11 and X16R

- Potential efficiency increase of approximately 1000x after deployment of ASIC

X11 (and similar X series) requires 11 unique hash cores that are arranged in a fixed order. The efficiency of each hash core is similar to that of a single SHA core, so from an overall design perspective, the efficiency gains are still similar.

The X16R requires multiple hash cores to interact through a simple ordered state machine. Each individual core will have a similar increase in efficiency, and the sequencing logic will require the least amount of power, space, and time.

The Baikal BK-X is an ASIC with multiple hash cores and a programmable sequencer that has been upgraded to support a new algorithm with different hashing orders.

#### Equihash

- Approximately 100-fold increase in potential efficiency after deployment of ASIC

The 150MB state is large, but it is possible with ASIC. Binning, sorting, and comparison of strings can be accomplished quickly with ASIC.

#### Cuckoo Cycle

- Approximately 100-fold increase in potential efficiency after deployment of ASIC

Once a Time/Memory Tradeoff attack occurs, it is not clear how much state the chip requires. A professional Graph Traversal core and SHA computing core increase in efficiency in a similar way.

#### CryptoNight

- Approximately 50-fold increase in potential efficiency after deployment of ASIC

CryptoNight does much less computation than Scrypt and requires a full 2MB of register (no known time/memory Tradeoff attack). This high-capacity register will dominate ASIC deployments, limiting the number of hash cores and the absolute performance of ASIC. 

ASIC will consist almost entirely of on-chip SRAM (Static Random Access Memory).

#### Ethash

- Potential efficiency approximately 2x after deployment of ASIC

Because of the high-volume DAG (database availability group), Ethash requires external storage. However, this is all it needs -- there are very few cases where you need to calculate the memory load results. As a result, ASIC can eliminate some of the complexity and power consumption of GPU by simply forming a memory interface to a small computing engine.

## XPOS consensus mechanism

XPOS has been modified based on NPOS in order to comply with EcoBall's design philosophy. NPOS is a consensus mechanism called "Nominated Proof of Stake". The full English name is Nominated Proof of Stake. It was proposed by Polkadot in April 2019 and is an important development direction of POS consensus mechanisms. As we all know, staking is a unique attribute of the PoS consensus. Through staking, token holders actively participate in the governance of the public chain, exercise their token rights, and obtain rewards. To put it simply, we can compare Staking to buying fixed wealth management products, and obtain stable income (interest) by locking in liquidity. At the same time, the locked part can also enjoy the expected return of appreciation. In actual application cases, the POS consensus mechanism has some inherent problems, and then many similar variants have appeared to try to solve these problems. The following will briefly introduce POS and DPOS, and then focuses on XPOS.

### POS consensus mechanism

POS is a proof-of-stake consensus mechanism, fully known as "Proof of Stake", which requires users to provide Proof that they own a certain amount of digital currency (i.e. they have an interest in the digital currency).

PoS was first realized in August 2012 by PPCoin (PPC). PPC also introduced the concept of age (1 age per coin per day), where the total age of a coin held by a user is the number of coins multiplied by the number of days it has been held. The age of coins is inversely proportional to the difficulty of mining. The older the coins are, the lower the difficulty of mining. Once a block is dug out, the age of coins will be cleared and accumulated again, and you must wait 30 days to compete for the next block.

A simple understanding is that POW competes for accounting rights with computing power, while POS competes for accounting rights with equity. PoW is the more you do, the more you get. PoS is the more you hold, the more you get. PoS can also be likened to the interest system, holding money to earn interest and enjoying the profits.

There are obvious defects in the POS consensus mechanism, including the following:

- It is easy to cause oligarchy: some wealthy nodes with top currency holdings may use their influence to manipulate the development of the whole ecology, resulting in the "Matthew Effect", which makes the rich get richer and gradually become a centralized oligarchy.
- The rich do evil: Since the rich control the majority of the currency, there is no mechanism to check and balance if they do evil, or if they band together to do evil. Blockchain will either fork or become a game for a few rich people.
- System efficiency is not high: POS mechanism still needs to run a large number of nodes, transaction confirmation and block efficiency is not high, essentially does not solve the pain points of commercial applications.
- "No-At-Stake" attack: that is, "No-At-Stake" attack. Since the POS consensus mechanism has no strict requirements on the resources of nodes, if the blockchain forks, users with the same number of tokens on the fork chain will acquiesce to the existence of the fork and may actively participate in the mining of the fork chain due to the interest drive.
- "long-range" attack : "long - range" attack, when the node is no longer act as validator, after paid the deposit, although no longer had the right after the validation block, but can still to rollback blocks before the operation, the attacker could bribe the once validator, collect enough private key, to build a long enough against the chain.


### DPOS consensus mechanism

DPoS is called "Delegated Proof of Stake". The emergence of DPoS is to solve some problems existing in PoS mechanism.

The principle of DPOS is the same as that of POS. The main difference is that under DPOS, nodes elect several agents, and the agents validate and keep accounts. Its compliance regulation, performance, resource consumption and fault tolerance are similar to POS. Similar to a board vote, the holder votes a certain number of nodes, and performs verification and accounting on their behalf.

The DPOS mechanism was first proposed by BitShares. BitShares hope to reduce the negative effects of centralization by introducing a layer of technological democracy. Bitshares introduce the concept of "witnesses" who can generate blocks. Each shareholder can vote for Witnesses, and the candidate with the top N total votes (usually 101) can be elected Witnesses. The list of candidates for Witness is updated daily. Witnesses random arrangement, each have 2 seconds to generate blocks according to the order if the witness in a given period of time can't generate block, block generated permissions to the next time the corresponding witness before the next witness block will contain the output of a witness not success to the block and missing all transactions, so the block size increase, confirm the time will be extended accordingly. Witnesses who fail to make blocks will be made public, and if they often fail to make blocks, community shareholders can vote to strip the witness of his bookkeeping rights and forfeit the corresponding income.

In some ways, DPOS is similar to the parliamentary system or the people's congress system. If the representative fails to perform their duties, such as failing to produce a block on time, it is replaced by a new witness node selected by the network.

Compared with POS, DPOS mechanism significantly reduces the number of participating verification and billing nodes and can achieve consensus confirmation at the second level. From the point of view of performance and energy consumption, it can fully meet the commercial needs, but it also inevitably brings the problem of over-centralization. If several witnesses or super nodes collude, it will further form a giant monopoly, which will have an immeasurable impact on the future development of blockchain.

### XPOS consensus mechanism roles

With the above brief introduction to the POS and DPOS consensus mechanisms, let's look at the XPOS consensus mechanism in more detail. There are two main roles in the XPOS consensus mechanism, the nominator and the validator. Let's take a brief look at each of these roles.

#### validator

The validator is responsible for validating transactions and packaging new blocks and receiving rewards generated by blocks. The validator must stake enough capital as a deposit, and run a high-availability, high-bandwidth, high-performance blockchain node program to receive transactions from the chain at any time, and then validate and produce block. If the validator does not perform their duties properly, such as failing to successfully produce blocks, or double-signing, or producing illegal blocks for demonstrable malicious behavior, they may lose part or all of the deposit. The specific number is determined according to the severity and number of errors made by the validator.

#### nominator

Nominators are a group of people who have a token ECO of the original token of the blockchain system. They nominate a validator they trust, staking a certain amount of ECO to the validator as the nomination deposit, entrust the validator to maintain the blockchain network on their behalf, and according to the proportion of the total staking of the validator they staking ECO to, Enjoy the rewards and possible slash of the validator. The system encourages ECO holders to actively participate in the nomination as nominator and participate in the ecological construction of blockchain. Currently nominates can nominate up to 16 verified candidates they trust.

validators do most of the heavy lifting: they are responsible for generating new candidate blocks, validating transactions, and reaching consensus. Once the nominator nominates and stakes ECO, there is no need to do anything. The nominator's experience is akin to "set it and forget it," while the validator will provide a positive service to the network by performing key actions. For this reason, the validator has certain privileges over the payout of the equity mechanism and can declare his right of distribution prior to the allocation of the equity to the nominator.


### GPOW + XPOS hybrid consensus mechanism

The EcoBall blockchain system adopts a hybrid consensus mechanism combining Proof of Work (GPOW) + Proof of Stakes (XPOS). The two consensus mechanisms are flexibly combined to give full play to their respective advantages and ensure a more efficient and faster underlying blockchain system on a fairer and more open, more decentralized basis, which can not only meet the mining needs of the majority of miners, but also meet the application implmentation needs of commercial users.

In the EcoBall blockchain system, GPOW miners are responsible for continuously producing block headers and broadcasting them to all validator nodes  at the same time, XPOS validator nodes are also continuously collecting transactions on the network, verifying and then passing the verification. The transaction is packaged into a block body and combined with the received block header to form a complete block.

Every time a block is generated, the system rewards a certain amount of ECO, of which 30% is allocated to GPOW miners and 70% is allocated to XPOS miners. The block reward is halved every 4 years until the last block is mined.We know that the last block can never be dug out, only infinitely close. By that time, the system has been operating stably for many years, and many valuable assets and business application scenarios have been generated on the chain, and various transactions are actively carried out on the blockchain. Miners and validators will rely more on these transaction fees in the later stages to maintain the effective operation of nodes and network security.

#### Generate block header

GPOW miners generate a blockheader about very 10 seconds through fierce computing power competition. The block header contains the following fields: parent block hash value, uncle block hash value, Coinbase account address, state root, transaction hash, recipient hash, log, difficulty value, block number, highest-paid gas, spent gas, Time Stamp, extra data, mixed hash, nonce value (8 bytes).

Here, the fields of unknown content such as block number, timestamp, transaction hash, gas spent, etc. are temporarily empty and are left to be filled by the validator node later.

#### Transaction verification

The validator node continuously receives transactions on the blockchain network and verifies the validity and legality of the transaction. After the verification is passed, the transaction is broadcast to other validators, and other validators will perform the same verification on the transaction. Transactions verified by more than two-thirds of the validators are sent to the block validator, waiting for packaging and block production.

#### Election of validators

Block-producing validators are randomly selected by all validators in the validator pool. After the validator succeeds in producing a block, a new round of elections will be started; if the validator fails to produce a block successfully, the weight of the validator will be lowered and will be fined.

#### Rewards and penalties

Once the validator successfully generates a block, he will receive a certain amount ECO as a reward. After the validator has deducted the relevant fees, the reward will be distributed to the XPOW miner and all his nominators. All nominators will distribute these rewards according to the proportion of the ECO pledged by the validator. If the validator fails to produce blocks or acts that damage the system, he will be fined, and his nominator will share these fines in proportion.


### POA consensus mechanism

The POA proof of authority consensus mechanism, called Proof-of-Authority in full, is a consensus algorithm based on reputation and prestige, which provides a faster transaction rate for the blockchain. POA was proposed in 2017 by Gavin Wood, the co-founder of Ethereum, former CTO of Ethereum, and technical expert. Miners rely on personal reputation and prestige to become validators of blocks, rather than relying on collateralized cryptocurrency. The verifier of the POA blockchain is composed of trusted verification nodes, and the number has a certain limit. Therefore, the blockchain system has better scalability. The verifier runs the node software to package the transaction and generate blocks. This process is completely automated and only needs to verify that the node is always in a good operating state. The verifier is the key to the entire consensus mechanism. The verifier does not need expensive GPU or sufficient assets, but he must have a known and verified identity. The verifier obtains the right to guarantee the network through this identity in exchange for block rewards. If the verifier has malicious behavior throughout the process, or colludes with other verifiers, the malicious actors can be removed and replaced through on-chain management.


### POU flexible consensus

PoU is the abbreviation of Proof of Unity, and is an innovative consensus mechanism that integrates multiple consensus algorithms.

With the increasing participation of people, the access congestion problem of Bitcoin and Ethereum has become more and more serious. At present (GMT+8 21/03/2021), the average transaction fee of Bitcoin has reached $18.9 while TPS is only 3.44; the transaction fee of Ethereum ETH has reached $6.93, and the transaction fee of a Uniswap is as high as $43.87, while the TPS is only 15.3. To increase TPS, most public chains choose a PoS mechanism to improve the blockchain network congestion problem, such as Polkadot NPoS, grapefruit DPoS, Ethereum 2.0 Casper, etc.


Although this PoS mechanism (DPoS, NPoS, etc.) solves the problem of low TPS to a certain extent, the decentralization feature is greatly reduced, and it is vulnerable to manipulation and attack by a small number of people. It is difficult for ordinary users to participate in maintaining the security of the system. . At the same time, this approach also destroys the fairness of the blockchain.


EcoBall designed a new type of protocol, Proof of Unity, which can solve scalability issues while ensuring decentralization and security, achieving higher throughput (5000±TPS), and decentralization of the entire system. Security and scalability are guaranteed, supporting millions of users with extremely low transaction fees and fast transaction confirmation time.


In the first phase of the Proof of Unity protocol, a hybrid consensus mechanism combining PoW workload and PoS equity proof is adopted. PoW mining nodes and PoS verification nodes jointly maintain the security of the system (Unity) in an innovative way ( the attacker can only attack the system if he controls a large amount of computing power and verification nodes at the same time, that is, if the attacker needs to control 20% of the tokens or verification nodes, it must reach 96% Or more of the whole network computing power at the same time. Only by then,  there will be  a certain probability to achieve the purpose of the attack).EcoBall optimized and adjusted the traditional PoW algorithm and PoS algorithm according to the long-term planning and functional requirements, and named them GPoW and XPOS respectively.


In the subsequent version development of Proof of Unity, it will not be limited to the single implementation of PoW algorithm and PoS algorithm, hash algorithms such as SHA256, Equihash, ProgPoW, as well as DPoS, NPoS, PoA, EcoBFT, threshold signature (DKG+TBLS) Staking methods such as, TPoS, etc., can be combined and reconstructed as needed and can be selectively used in the protocol.
(Note: EcoBFT is a new BFT consensus algorithm developed on the basis of PBFT and other BFTs. EcoBFT is more in line with the characteristics of the blockchain by changing the voting process, thereby improving efficiency and synchronization without lowering security than PBFT. The mechanism is superior to existing BFT consensus algorithms such as PBFT. In addition, EcoBFT is adopted, and the block confirmation speed is better than DPoS and PoW consensus algorithms; threshold signature (DKG+TBLS), DKG (Distributed key generation, distributed key generation) Generated),Through the decentralized random function, the nodes participating in the EcoBFT consensus can be randomly selected from the candidate nodes. At the same time, these random functions can verify the legitimacy and greatly increase the cost of the nodes doing evil, thereby ensuring the security of the overall EcoBall system; the threshold of equity proof TPoS ( Threshold Proof of Stake, used to meet the minimum mortgage amount) )

