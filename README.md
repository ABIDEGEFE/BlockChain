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
