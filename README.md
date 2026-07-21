# Node Types in a Public Blockchain Network

In a public blockchain, different types of computers (nodes) participate in maintaining, securing, and propagating the network. Each node type has a distinct role:

## 1. Wallet Node
- Serves as the **entry point** to the blockchain network.  
- Stores block headers, private keys, and generates **12–24 word seed phrases** for asset recovery.  
- If both the seed phrase and private key are lost, the associated cryptocurrency becomes permanently inaccessible.  
- Used to **send, sign, and create transactions**, as well as check balances.  
- Typically connects to 3–10 active full nodes to broadcast transactions.  
- Runs on lightweight devices (phones, desktops, laptops) with self-custodial apps like **Green Wallet** or **Trust Wallet**.  

---

## 2. Full Node
- Receives, verifies, stores, and broadcasts transactions and blocks.  
- Maintains the **entire blockchain history** from the Genesis block to the latest block.  
- Stores only the **current state** of the blockchain, unlike archive nodes which preserve historical states.
- Full nodes validate blocks incrementally, but perform full history validation during **Initial Block Download (IBD)**.


---

## 3. Miner Node
- A specialized type of full node.  
- Performs all full node tasks plus:  
  - Stores the full blockchain copy.  
  - Collects transactions and builds candidate blocks.  
  - Solves **Proof-of-Work (PoW)** puzzles.  
  - Broadcasts newly mined blocks.  
- **All miners are full nodes, but not all full nodes are miners.**

---

## 4. Pruned Node
- Stores only a subset of blockchain data by discarding older blocks.  
- Useful for devices with limited storage capacity.  
- Retains enough data to validate new transactions and blocks.

---

## 5. Archive Node
- A specialized full node that stores the **entire historical state** of the blockchain.  
- Unlike normal full nodes, archive nodes preserve every state change.  
- Enables queries such as “What was the BTC balance of address X on July 10, 2022, at 5:00 AM?”  
- Commonly used by **researchers, explorers, and analytics companies**.

---

## 6. Boot Node (Seed Node)
- Helps new nodes join the network.  
- Provides peer discovery information so new nodes can establish communication with the blockchain.

---

## 7. Relay Node
- Designed to **forward data quickly**.  
- Reduces propagation delay across the network.  
- Improves efficiency of transaction and block dissemination.

---

# How the Gossip Protocol Works in Blockchain Networks

The **gossip protocol** is the communication mechanism that enables blockchain nodes to share information efficiently and securely. It governs how transactions, blocks, and peer data propagate across the network.

---

## 🔄 Information Shared via Gossip
- **Transactions**  
- **Blocks**  
- **Peer addresses**  
- **Network status**  

---

## 🌐 Network Architecture
- **Public blockchains** use a **peer-to-peer (P2P)** architecture. Connections are opportunistic, randomized, and dynamic.  
- **Permissioned blockchains** may adopt a **hub-and-spoke** architecture for controlled communication.  
- P2P design eliminates single points of failure, ensuring resilience and decentralization.  
- Each peer stores and maintains its own data independently.  

---

## ⚙️ Connection Management
- Nodes limit concurrent connections to optimize hardware resources and mitigate **DoS attacks**.  
- Example: In the **Bitcoin network**, the default maximum is **125 connections** (117 inbound, 8 outbound).  
- **Outbound connections** are strictly managed, authenticated, and randomized.  
- **Inbound connections** are open until the maximum limit is reached.  

---

## 🛠️ Node Onboarding Process
When a new node joins the network, it follows a multi-step process:

1. **Initial boot-up** of the node.  
2. **Query seed nodes** to obtain IP addresses of active peers.  
   - Bitcoin source code includes hardcoded domain names of seed nodes.  
   - If querying fails, fallback IP addresses are used.  
3. The node stores IPs in two internal tables:  
   - **New Table** → untrusted addresses.  
   - **Tried Table** → trusted addresses.  
4. The node queries active peers using these IPs.  
5. The peers return thousands of additional IP addresses, expanding the node’s connectivity.  

---

## 📡 Gossip Protocol Mechanics
- Defined as a **set of rules and logic** embedded in blockchain source code.  
- Example rule: *Pick 3 random connected peers every 100 milliseconds.*  
- When a transaction is issued:  
  1. A full node receives, verifies, and stores it in the **mempool**.  
  2. The node gossips the transaction to its neighbors.  
  3. Each neighbor repeats the process.  
  4. Within seconds, the transaction propagates across the entire network.  

---

## ⏱️ Propagation Characteristics
- Each transaction has a **unique ID**, preventing infinite rebroadcast loops.  
- If a node already has a transaction, it ignores and stops forwarding it.  
- **Bitcoin transaction propagation time**: typically **1–2 seconds**.  

---

# Broadcast Mechanism in Blockchain Networks

When a transaction or block is **broadcast**, does it travel through the normal Internet (routers, ISPs, TCP/IP), or does blockchain have its own dedicated network?

- Blockchain does not have its own dedicated network configured to route transactions and blockchain-related data. Instead, it utilizes the normal Internet infrastructure, starting from the user’s device, traveling through ISP routers, and reaching the full node as the destination. This connection is governed by the **TCP/IP protocol**, like any other Internet connection. The only difference is the destination.  
- The TCP/IP connection is not limited to wallet–full node communication. It also governs the broadcast of data once it is validated and stored by a full node.  
- The blockchain network is an **overlay network** built on top of the Internet. An overlay network is a virtual network formed by applications that communicate over existing infrastructure.  
- The physical Internet provides connectivity, while blockchain software determines which peers to connect to and what messages to exchange.  
- Configuring a reachable full node requires:  
  1. Opening a specific port (e.g., for Bitcoin it is **8333**)  
  2. Setting up firewall rules  
  3. Maintaining a stable Internet connection  
- Internet infrastructure moves the data from one computer to another.  
- The **Gossip Protocol** decides which blockchain peers should receive and forward the transaction.  

---

# What Cryptocurrency Actually Is
- **Cryptocurrency** is a record of transaction history that utilizes cryptography to secure its processes. There is no actual “coin” in the network; instead, the blockchain stores the history of who can spend how much value.  
- Ownership of cryptocurrency means the blockchain records one or more transaction outputs that can be spent by someone who can verify the signature using corresponding public keys. It is essentially the authority to access and manage your transactions through the blockchain network, enabling spending according to blockchain rules.  

---

# What Is Cryptography?
- **Cryptography** is the science of hiding or securing information from public view. Blockchain uses **asymmetric cryptography**, which involves two mathematically linked keys: a private key and a public key.  
- The **private key** is a large, randomly generated number derived from an elliptic curve graph.  
- The **generator point** is a random, publicly known coordinate point on the curve.  
- The **public key** is a coordinate point calculated using the private key and the generator point.  
- The sender creates a **digital signature** using the private key and the hashed value of the actual data. The sender then transmits the data, public key, and signature to the receiver.  
- The receiver uses these public values and plugs them into a multi-variable equation to verify the signature’s validity.  
- The signature consists of two numbers (**s, r**). The receiver attempts to derive the coordinating point (**x, y**) and applies the final check:  

```text
if s == x:
    valid
else:
    invalid
```

- A random number called a **nonce** is generated for every transaction. This nonce is used to generate one of the signature’s numbers (**s**).  
- Reusing the same nonce for at least two transactions gives attackers a significant advantage in calculating the hidden private key. Therefore, the nonce must be random and unique for every transaction.  

---

# What Triggers Block Creation?

- Before understanding what triggers miner nodes to create a block, it is important to understand **why miners build blocks for the network**. The answer is simple: they receive **network rewards (minted coins)** and **transaction fees**.  
- In the Bitcoin blockchain network, there is no specific moment when miners begin creating a block. Block creation is a **continuous process**, occurring 24 hours a day, every second.  

---

## 🔨 Block Creation Process
1. A transaction occurs (e.g., *A sends 5 BTC to B*).  
2. Nodes actively listen for newly incoming transactions.  
3. The transaction is received and placed into the **mempool** (waiting list of transactions).  
4. Miner nodes randomly select transactions from the mempool to create a **candidate block**. Miners typically prioritize transactions with higher fees to maximize profitability.  
5. Miners begin solving complex mathematical problems. By combining block data with a **nonce** (a number to be guessed) and hashing them with **SHA-256**, they attempt to satisfy the network rule known as the **difficulty target**.  
6. The node that finds the correct nonce immediately broadcasts the valid block. Other nodes verify it and append it to the blockchain if valid. Once confirmed, miners discard the processed transactions from their mempool and candidate block.  

---

## ⚔️ Handling Conflicts
- If two miners solve the mathematical puzzle and broadcast their blocks simultaneously, the network may temporarily split, with miners appending different versions of the blockchain.  
- This difference is resolved once the next block is created and broadcast. The **longest chain rule** applies: miners adopt the version of the blockchain with the greater length, ensuring consensus across the network.  

---
