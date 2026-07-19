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
