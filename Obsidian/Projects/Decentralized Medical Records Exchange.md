### **Decentralized Medical Records Exchange (DMRE)**

- **Problem:** Patients struggle to access and share their medical records securely across different healthcare providers.
- **Solution:** A blockchain-powered platform where medical records are stored on-chain as encrypted data. Patients have full control over access permissions via NFTs or smart contracts, allowing only authorized healthcare providers to access them.

### **How It Works**
1. **Patients Upload Records**: Medical data is encrypted and stored off-chain (e.g., IPFS or Arweave), while metadata is recorded on Polygon.
2. **NFT-Based Ownership**: Each patient gets an NFT that represents access rights to their records.
3. **Smart Contract Permissions**: Patients can grant or revoke access to specific doctors, hospitals, or insurers.
4. **Instant Verification**: Doctors can view patient history in real-time, reducing paperwork and misdiagnoses.

### Features

- **Medical Records as NFTs**: Patients store medical data off-chain and use NFTs to control access.
- **Permission-Based Access**: Patients grant or revoke access to doctors via smart contracts.
- **Secure Storage**: Medical records stored on **IPFS/Filecoin**, with metadata on **Polygon blockchain**.
- **Wallet Authentication**: Users authenticate via **MetaMask/WalletConnect**.
- **Scalable Backend**: **Node.js/Express.js API** interacts with the blockchain.

### **Tech Stack for Decentralized Medical Records Exchange (DMRE)**

- **Blockchain:** Polygon (for scalability) & Ethereum (for security)
- **Smart Contracts:** Solidity + Hardhat (development framework)
- **Storage:** IPFS/Filecoin (for medical records)
- **Backend:** Node.js + Express.js (to interact with the blockchain)
- **Frontend:** React + Next.js (for user interface)
- **Database (Optional):** PostgreSQL/MongoDB (for off-chain metadata)
- **Wallet:** MetaMask (for authentication)
- **APIs:** Moralis/Alchemy (to interact with blockchain data)
- **Security:** OpenZeppelin (for secure smart contracts)
#### **AI (Optional - For Medical Insights)**
- **Python (FastAPI/Flask) + TensorFlow/PyTorch** (for AI-based health analysis)

### Project Structure

```
dmre-project/
│── backend/             # Express.js API for blockchain interaction
│   ├── controllers/             # Business logic (Web3 functions)
│   ├── models/                  # Optional DB schema
│   ├── routes/                  # API routes
│   ├── services/                # Smart contract interaction
│   ├── app.js                   # Express entry file
│   ├── config.js            # Configuration (RPC URLs, private keys)
│   ├── package.json             # Backend dependencies
│
│── blockchain/                # Hardhat setup for Solidity contracts
│   ├── contracts/               # Smart contracts (Solidity)
│   ├── scripts/                 # Deployment scripts
│   ├── test/                    # Smart contract testing
│   ├── hardhat.config.js        # Hardhat configuration
│   ├── package.json             # Dependencies
│
│── frontend/                    # React + Next.js (user interface)
│   ├── components/              # Reusable components
│   ├── pages/                   # Next.js pages
│   ├── utils/                   # Web3 integration (ethers.js)
│   ├── styles/                  # Tailwind CSS for styling
│   ├── package.json             # Frontend dependencies
│   ├── next.config.js           # Next.js configuration
│
│── .env                        # Environment variables (PRIVATE KEYS)
│── README.md                     # Documentation

```

- **Backup Storage:** Filecoin (to persist files permanently)
- **Encryption:** AES-256 (encrypt before uploading)
### **💡 Unique Features & Monetization**
🚀 **Token-based system** – Patients earn crypto incentives for sharing data  
🔐 **Zero-Knowledge Proofs (ZKPs)** – Privacy-preserving data verification  
📜 **DAO for Health Records** – Community-governed access to medical research


### **Estimated Timeline (4 Weeks Plan)**

#### ✅ **Day 1: Research, Planning & Smart Contract Development**

- Finalize the architecture (on-chain vs. off-chain storage, NFT structure, access control).
- Write and test **Solidity Smart Contracts**:
    - NFT minting for medical records
    - Patient NFT creation (ERC-721) → Represents access rights
    - Access control (grant/revoke permissions) --- permission based smart-contracts
      // basically we will use ERC721 for the access control
    - Encryption & secure record storage pointers (IPFS/Filecoin)
    - Data hashing & verification
- Set up Hardhat development environment and writing contracts using hardhat.
- Use **OpenZeppelin** for security best practices.
- Deploy initial contracts on **Polygon Mumbai Testnet** for testing.

#### ✅ **Day 2: Backend API & Wallet Integration**

- Build Node.js/Express.js backend to:
    - Connect with smart contracts.
    - Handle MetaMask authentication.
    - Store minimal off-chain metadata (MongoDB/PostgreSQL).
    - implement blockchain login into the node app using ether.js
- Integrate **IPFS/Filecoin** for decentralized storage and for decentralized medical record storage.
- metamask authentication and jwt for off-chain data
- Set up **Moralis/Alchemy** for reading blockchain events.
- Unit test **Implement API Endpoints**:
	- `POST /mint` → Mint a new medical record.
	- `GET /record/:id` → Retrieve medical record metadata.
	- `POST /grant-access` → Grant a doctor access to records.
- Develop access control logic (only approved wallets can retrieve records)

#### ✅ **Day 3: Frontend Development & UI/UX**

- Build **React + Next.js** frontend:
    - Patient dashboard (Upload, Manage Records, Grant/Revoke Access).
    - Doctor dashboard (Request/View Medical Records). From where they can request access as well as view them
    - MetaMask/WalletConnect authentication flow.
- Integrate smart contracts for NFT based access control
- Connect frontend with backend API & blockchain.
- implement wallet integration using ether.js
- Implement UI components with **shadcn/ui** for a clean, modern look.
- Ensure **responsiveness & accessibility**.

#### ✅ **Day 4: Testing, Deployment & Final Refinements**

- End-to-end testing (Smart Contracts, API, UI).
- Smart Contracts Deployment
	- Deploy **smart contracts to Polygon mumbai mainnet**.
	- Verify contracts using **Etherscan or Polygonscan**.
- Deploy backend
	- Secure API with **JWT authentication & CORS**.
	- Host Express.js API on **Vercel, AWS, or DigitalOcean**
- Deploy frontend
	- Deploy **React + Next.js** on **Vercel or Netlify**.
	- Connect frontend to **deployed backend & smart contracts**.
- smart contract testing
	- Use **Hardhat & Chai** for unit testing.
	- Check for vulnerabilities using **OpenZeppelin Defender**.
- backend testing
	- postman for api testing
	- Check Web3 transactions using **PolygonScan**.
- frontend testing 
	- check for metamask connectivity
- Final optimizations (gas fees, UI improvements, security).
- Prepare a **demo pitch & documentation** for the hackathon.
- Deployment and scalling
	- **Monitor Performance** using Alchemy/Moralis analytics.
	- **Optimize Gas Costs** with Polygon L2 solutions.

# Architechture

Why this architechture
- Scalable - uses polygon for low gas cost 
- Secure - only the patient controls the access 
- Decentralized - Data stored in IPFS, not a centralized server
- Efficient - Smart Contract reduce intermediaries

## **High-Level Architecture Overview**

The architecture consists of **5 key layers**:

1️⃣ **User Interface (Frontend) → React + Next.js**  
2️⃣ **Blockchain Layer → Polygon + Ethereum Smart Contracts**  
3️⃣ **Decentralized Storage → IPFS/Filecoin**  
4️⃣ **Backend (API) → Express.js + Node.js**  
5️⃣ **Authentication & Security → MetaMask, JWT, Access Control**

![[Pasted image 20250207211213.png]]


## **Workflow/ UX**
#### 1. Uploading Medical Records

- User logs in with a metamask wallet 
- User uploads the medical records --> Frontend encrypts it 
- File is stored in IPFS, and the hash is retrived 
- Smart Contracts mints an NFT storing the IPFS hash
- User can now share access to doctors using NFT permissions

#### 2. Granting Access to the User
- Patient selects a doctor wallet address
- Smart contract update the access list (so only the selected doctors can view )
- doctor verifies the access via the blockchain
- Doctor fetches the IPFS hash from the smart contract & decrypts the file in order to see it.

#### 3. Doctor viewing the record
- Doc connects wallet and verifies the access
- smart contract checks permission for the doc's wallet 
- If granted the doc gets the IPFS hash, decrypts the file and views the record

#### 4. Appoinment Setting
- User log in the sytem
- fills the form 
- sets an appoinment date

## **Component Breakdown** --
### BlockChain Layer(Smart Contracts)
- Role 
	- stores the permissions
	- Mints ERC-721(NFT) as Medical Record IDs
	- Control Access using NFT-based permissions
	- Stores only the minimal data(Hash, Owner, Access list)

- Features
	- Mint NFTs
	- Grant or revoke access
	- Verify patient Ownership

- Tech Stack
	- **Blockchain:** Polygon (Ethereum L2 for scalability).
	- **Smart Contracts:** Solidity (ERC-721 for medical NFTs).
	- **Security:** OpenZeppelin (for safe contract implementation).

### Decentralized Storage
- Role 
	- Stores the NFT
	- Blockchain stores the IPFS hash not the actual file

- Features
	- prevents tampering
	- patient control access
	- files stored in encrypted format

- Tech Stack
	- **Storage:** IPFS (InterPlanetary File System)
	- **Backup Storage:** Filecoin (to persist files permanently)
	- **Encryption:** AES-256 (encrypt before uploading)

### Backend
- Role 
	- Acts as the middleman btwn frontend and blockchain
	- Handles off-chain metadata storage
	- calls smart contract on behalf on the frontend

- Features
	- API endpoint 
	- IPFS integration -- for storage
	- Off-Chain metadata storage
	- Auth & JWT for API security

- Tech Stack
	- **Database (Optional):** MongoDB/PostgreSQL (For storing logs, metadata)
	- **Blockchain SDK:** Ethers.js (for smart contract interaction)
	- **Off-Chain Auth:** JWT (for API security)
	- **Smart Contract Access Control:** ERC-721 NFTs
	- **Encryption:** AES-256
	  
### Frontend
- Role 
	- allows users to mint medical records as NFT
	- Gives a Dahboard for the user -- to manage records and access 
	- uses ether.js to connect with the blockchain
	- connects the Metamask for authentication

- Features
	- Connect Wallet (MetaMask)
	- View, Upload & Share Medical Records (via IPFS).
	- Grant/Revoke Access to Doctors via Smart Contract.
	- Call APIs to store off-chain metadata securely.
	- Data Encryption before storong into IPFS
	  
	  // off-chain vs on-chain
	  Off-chain --> 
	  - this are the trans that occur outside the blockhain
	  - generaly they are being processed by the other Layer-2 solutions or other chain, and then recorded in the main chain 
	  - Uses
		  - Lower fees 
		  - faster processing 
		  - improved privacy
		  - reduced load on ledger 
		    // all this because the manipulation is not occuring in the main blockchain 
		
		Whereas *On-chain* reffers to the main blockchain layer

- Tech Stack
	- **Framework:** React + Next.js
	- **Web3 Library:** Ethers.js
	- **Styling:** Tailwind CSS
# Documentation
- create the folder structure 

```bash
	mkdir blockchain && cd blockchain
	npm init -y
	npm install --save-dev hardhat ethers chai mocha @openzeppelin/contracts @nomicfoundation/hardhat-toolbox dotenv
	npx hardhat init
```

```bash
	mkdir backend && cd backend
	npm init -y
	npm install express ethers dotenv cors

```

```bash
	npx create-next-app@latest frontend
	cd frontend
	npm install ethers axios tailwindcss
	npx tailwindcss init -p

```

- blockchain development
	create MedicalRecordNFT.sol
	create deployment script
	edit hardhat.config.js
	write tests
	fill the .env file with the secrets
	`npx hardhat clean`
	`npx hardhat compile`
	
	- Start a hardhat local blockchain
	  `npx hardhat node`
	  this runs local ethereum testnet where transactions happen instantly
	  
	- test in Hardhat's Local Network to simulate transaction
	  `npx hardhat test`
	  Debug error and optimize gas cost
	  
	  ## **What Happens Behind the Scenes?**
		✅ Hardhat **deploys the contract** on a temporary test blockchain. 
		✅ Each test simulates **real blockchain interactions** (minting NFTs, granting/revoking access).  
		✅ Chai/Mocha **checks expected vs actual results** (e.g., does the doctor have access?).  
		✅ If a test **fails**, it means there's a bug in your smart contract logic.
	
	Deploy in testnet
	🔹 **Use Polygon Mumbai Testnet**
	- Fund your **MetaMask wallet** with test MATIC from a **faucet**.
	- Deploy using Hardhat or Remix IDE.

	test the contract on polygon testnet ---
	`npx hardhat run scripts/deploy.js --network mumbai`

	- Save the **contract address** and **ABI** for integration.
	- Verify the contract on **Polygonscan** (optional but recommended).

- backend development, Integartion


- frontend development, Integration



# **Learning from the Project**
- If you know to build fullstack apps
	- you can build effective blockchain apps
	- looks matters
- blockchain just replaces the modern server and data-base 
- to build a web3 app
	- write the contracts 
	- deploy them
	- use backend to interact with the contracts and generate the API endpoints
- 
