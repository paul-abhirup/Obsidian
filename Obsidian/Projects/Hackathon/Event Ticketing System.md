
Blockchain features are 

  Marketplace
    ✔ should allow seller to list a ticket
    ✔ should not allow listing above max resale price
    ✔ should allow buyer to purchase a listed ticket
    ✔ should enforce correct royalty payments on purchase
    ✔ should allow seller to cancel a listing
    ✔ should allow users to place bids and store the highest bid
    ✔ should allow seller to accept the highest bid

  TicketNFT
    ✔ should have correct name and symbol
    ✔ should set the correct base URI
    ✔ should allow owner to mint tickets
    ✔ should not allow minting beyond maxTicketsPerWallet
    ✔ should update the base URI by the owner
    ✔ should prevent non-owners from minting
    ✔ should prevent non-owners from changing the base URI


## **User Flow Architecture**

The user flow describes how users interact with your application. Here’s a high-level overview:

1. **User Onboarding**:    
    - User connects their wallet (e.g., MetaMask)        
    - User registers an account (links wallet to email/profile).
        
2. **Event Discovery**:    
    - User browses upcoming events.        
    - User views event details (date, venue, ticket prices).
        
3. **Ticket Purchase**:    
    - User selects an event and purchases a ticket.        
    - Ticket is minted as an NFT(ERC 721 token) and stored in their wallet.
        
4. **Ticket Management**:    
    - User views their owned tickets.        
    - User can list tickets for resale or transfer them.
        
5. **Marketplace Interaction**:    
    - User browses the marketplace for resold tickets.        
    - User can place bids or buy tickets directly.
        
6. **Event Attendance**:    
    - User presents their ticket (QR code) at the event.        
    - Ticket is validated on-chain.
        
7. **Post-Event**:    
    - User can view transaction history and royalties earned (if applicable).
        

---

## **Backend and Frontend Service Design**

Here’s how the backend and frontend services interact:

### **Backend Services**

1. **API Layer**:    
    - Handles HTTP requests from the frontend.
    - Exposes RESTful endpoints for ticket management, marketplace operations, and user authentication.
        
2. **Blockchain Layer**:
    - Interacts with smart contracts using `ethers.js`.
    - Handles transactions (minting, buying, bidding, etc.).
        
3. **Off-Chain Storage**:
    - Uses **Supabase** for:
        - User profiles.
        - Event metadata.
        - Ticket metadata (e.g., seat info, event details, nft details).
            
4. **Authentication**:    
    - Uses **JWT** for session management.        
    - Links wallet addresses to user profiles.
        
5. **Real-Time Updates**:    
    - Uses **Redis** or **Supabase Realtime** for real-time notifications (e.g., new listings, bid updates).
        
6. **Indexing**:    
    - Uses **The Graph** for querying blockchain data (e.g., ticket ownership, marketplace listings).
        

---

### **Frontend Services**

1. **Wallet Integration**:    
    - Uses **MetaMask** or **WalletConnect** for wallet connectivity.        
    - Handles wallet authentication and signing transactions.
        
2. **UI Components**:    
    - **Home Page**: Displays upcoming events.        
    - **Event Page**: Shows event details and ticket purchase options.        
    - **Marketplace Page**: Lists resold tickets and allows bidding.        
    - **Profile Page**: Displays user’s tickets and transaction history.
        
3. **API Integration**:
    - Uses **Axios** or **Fetch API** to interact with the backend.        
    - Handles API responses and updates the UI dynamically.
        
4. **Real-Time Updates**:    
    - Uses **WebSocket** or **Supabase Realtime** to listen for updates (e.g., new bids, ticket sales).
        

---

## **User Authentication and Experience Features**

Here’s how to design the authentication and user experience:

### **1. Wallet Authentication**
- **Flow**:
    1. User clicks "Connect Wallet".
    2. Frontend prompts user to sign a message using their wallet.
    3. Backend verifies the signature and issues a JWT. 
    4. JWT is stored in the frontend (e.g., localStorage) for subsequent requests.
        
- **Features**:    
    - Support for multiple wallets (MetaMask, WalletConnect, etc.).
    - Session persistence (user stays logged in across page refreshes).

### **2. User Registration**
- **Flow**:    
    1. User connects their wallet.
    2. User provides an email address.
    3. Backend links the wallet address to the email and creates a user profile in Supabase.
        
- **Features**:    
    - Email verification (optional).
    - Profile management (update email, view transaction history).
        

### **3. Event Discovery**
- **Flow**:    
    1. User browses the home page for upcoming events.
    2. User clicks on an event to view details (date, venue, ticket prices).
        
- **Features**:
    - Filter events by date, location, or price.
    - Display event highlights (e.g., popular events, sold-out events).
        

### **4. Ticket Purchase**
- **Flow**:
    
    1. User selects a ticket and clicks "Buy".        
    2. Frontend initiates a transaction to mint the ticket NFT.        
    3. Backend handles the transaction and updates the user’s ticket list.
        
- **Features**:    
    - Gas fee estimation.        
    - Transaction status updates (pending, confirmed, failed).
        

### **5. Ticket Management**
- **Flow**:
    1. User navigates to their profile page.
    2. User views their owned tickets.
    3. User can list tickets for resale or transfer them to another wallet.
        
- **Features**:    
    - Display ticket details (event, seat info, QR code).        
    - Allow users to list tickets with a fixed price or auction.
        

### **6. Marketplace Interaction**
- **Flow**:    
    1. User browses the marketplace for resold tickets.        
    2. User can place a bid or buy a ticket directly.        
    3. Backend handles the transaction and updates the marketplace.
        
- **Features**:    
    - Sort listings by price, date, or event.        
    - Real-time bid updates.
        

### **7. Event Attendance**
- **Flow**:    
    1. User presents their ticket (QR code) at the event.        
    2. Event organizer scans the QR code and validates the ticket on-chain.
        
- **Features**:
    - QR code generation for each ticket.        
    - On-chain validation to prevent fraud.
        

### **8. Post-Event**
- **Flow**:
    1. User views their transaction history and royalties earned (if applicable).        
    2. User can provide feedback or rate the event.
        
- **Features**:    
    - Display transaction history (minting, buying, selling).        
    - Show royalties earned from resales.
        

---

## **Backend and Frontend Integration**

## Backend API Endpoints

### 1. Ticket Management
**GET** `/tickets/:tokenId`  
- Fetches NFT ticket metadata + on-chain validity  
- Response: `{ owner, eventId, seatInfo, isUsed, mintDate }`

**POST** `/tickets/mint`  
- Initiate ticket minting transaction  
- Body: `{ eventId, recipientAddress }`  
- Returns: `{ txHash, gasEstimate }`

**GET** `/users/:address/tickets`  
- List all tickets owned by a wallet  
- Response: `Array<{ tokenId, eventDetails, isListed }>`

### 2. Marketplace Operations
**POST** `/marketplace/list`  
- Create fixed-price listing  
- Body: `{ tokenId, price, expiration }`  
- Returns: `{ listingId, txPayload }`

**POST** `/marketplace/bid`  
- Place auction bid  
- Body: `{ tokenId, bidAmount }`  
- Returns: `{ bidNonce, txData }`


**POST** `/marketplace/purchase/:listingId`  
- Execute buy operation  
- Returns: `{ purchaseTx, royaltyBreakdown }`

### 3. Auction Management
**GET** `/auctions/:tokenId/bids`  
- Get bid history for NFT  
- Response: `Array<{ bidder, amount, timestamp }>`

**POST** `/auctions/:tokenId/accept`  
- Accept highest bid  
- Returns: `{ transferTx, royaltyTx }`

### 4. Event Validation
**POST** `/events/validate`  
- QR code validation endpoint  
- Body: `{ qrHash, validatorSig }`  
- Returns: `{ isValid, tokenDetails }`

### 5. Royalty Tracking
**GET** `/royalties/:organizer`  
- Show accumulated royalties  
- Response: `{ totalEarned, pendingPayout, payoutAddress }`

### 6. User Management
**POST** `/users/register`  
- Link wallet to user profile (off-chain)  
- Body: `{ email, walletAddress }`  
- Returns: `{ userId, sessionToken }`

**GET** `/users/:address/activity`  
- Transaction history  
- Response: `Array<{ type: "MINT|PURCHASE", timestamp, txHash }>`

## Supplementary Endpoints

### 7. Event Management (Off-Chain)
**POST** `/events`  
- Create event metadata  
- Body: `{ name, venue, date, seatMap }`  
- Returns: `{ eventId, ipfsCID }`

**GET`** `/events/upcoming`  
- List events with available tickets  
- Response: `Array<{ eventId, ticketsAvailable, minPrice }>`

### 8. System Health
**GET** `/status/blockchain`  
- Node connectivity check  
- Response: `{ chainId, latestBlock, gasPrice }`

**GET** `/status/indexer`  
- Subgraph synchronization status  
- Response: `{ lastSyncedBlock, pendingEntities }`

## Real-Time Features
**WebSocket** `/updates`  
- Subscribe to: 
  - `LISTING_ADDED` 
  - `BID_UPDATED`
  - `TICKET_USED`

## Security Considerations
1. Implement JWT authentication with wallet signature challenges
2. Rate limiting on write operations (1 req/2s per IP)
3. Input validation for all EVM address parameters
4. Use prepared statements for any SQL operations

| Layer             | Tools                          |
|--------------------|--------------------------------|
| API Framework      | Express.js + TypeScript        |
| Transaction Relay  | Defender Relay                 |
| Indexing           | The Graph Subgraph             |
| Rate Limiting      | express-rate-limit             |
| Queue System       | BullMQ (Redis-backed)          |
| Real-Time          | Socket.IO with Redis Adapter   |

### Frontend Integration

1. **Wallet Connection**:   
    - Use `ethers.js` or `web3.js` to connect to the user’s wallet.        
    - Call `/auth/connect` to authenticate the user.
        
2. **Event Discovery**:    
    - Fetch events from `/events` and display them on the home page.
        
3. **Ticket Purchase**:
    - Call `/tickets/mint` to mint a ticket NFT.*        
    - Display transaction status and update the user’s ticket list.
        
4. **Marketplace Interaction**:
    - Fetch listings from `/marketplace/listings`.        
    - Call `/marketplace/bid` or `/marketplace/purchase` to interact with the marketplace.
        
5. **Profile Management**:    
    - Fetch user tickets from `/users/:address/tickets`.        
    - Fetch transaction history from `/users/:address/activity`.
        

---
NOTE 

On the frontend, clients can listen for bid updates like this:
This implementation:
```
// Frontend code example
const socket = io('http://localhost:3000');

// Join a ticket room
socket.emit('joinTicketRoom', tokenId);

// Listen for new bids
socket.on('newBid', (bidUpdate) => {
  console.log('New bid received:', bidUpdate);
  // Update UI with new bid information
});

// Leave the room when done
socket.emit('leaveTicketRoom', tokenId);
```
Focus in the frontend implementation

Maintains real-time updates across multiple server instances using Redis
Provides immediate updates to connected clients via WebSocket
Handles room management for ticket-specific updates
Includes proper error handling and logging
Maintains scalability with Redis pub/sub
Provides clean separation of concerns between services

Signed message--
0x476ba7e560d3c6b0d36e701f73a6d2480dd33f2018519cfe47bafa45b967b6bf58e0b53521b9cd1d6d44dcf3d0def2da7a9e6498f9cda087e04e974a38827d7f1c 0x1581d4149B3998795E9A17DaE91382b5E7541a78

---
# /auth 
### Post /auth/connect 
used to connect the metamask wallet and create a new user if not present in the db
req 
```
wallet address
signedmessage
```

res ----
```
{
    "data": {
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ3YWxsZXRBZGRyZXNzIjoiMHgxNTgxZDQxNDlCMzk5ODc5NUU5QTE3RGFFOTEzODJiNUU3NTQxYTc4IiwiaWF0IjoxNzQwMjI1NzM4LCJleHAiOjE3NDAyMjkzMzh9.uhX1GTadCJSLkfXl_WCbBadz4UTclttSJoMQzgINSfg",
        "user": {
            "id": "bacb3d6d-7345-4f46-8ac5-162597de4380",
            "wallet_address": "0x1581d4149B3998795E9A17DaE91382b5E7541a78",
            "created_at": "2025-02-22T12:02:18.546+00:00",
            "last_login": "2025-02-22T12:02:18.546+00:00"
        },
        "message": "Account created successfully!"
    }
}

```

basically return the jwt token

### Post auth/nonce
used to log the nonce value for signing in 

req
takes in the wallet address

res
```
Wallet: 0x1581d4149B3998795E9A17DaE91382b5E7541a78
Nonce: 1740238790032
```
---
# /tickets
## Post /tickets/mint
used to mint the nft token of the ticket

req
```
{
  "quantity": 2,
  "recipientAddress": "0x1581d4149B3998795E9A17DaE91382b5E7541a78"
}
```
with jwt token and content-type -- aplication.json


res
```
{
    "message": "Tickets minted successfully",
    "data": {
        "txHashes": [
            "0xcb6ff8fef3c5c8c4883eb7087a0ef2c9459bad5f20679b61efc9ac41f1caee25",
            "0x19baba3efee1479a2caf70d6d68407d34ef798b3b26476b278e9001b71139e14"
        ],
        "tokenIds": [
            "0",
            "1"
        ]
    }
}
```

// **there is an issue that there is nothing about the event id for which the ticket i am buying

## GET /tickets/:tokenId
fetches the information related to a ticket

```
{
    "owner": "0x1581d4149B3998795E9A17DaE91382b5E7541a78",
    "eventId": "210351fa-0cd9-48e9-9c63-ca809a26302d",
    "eventNames": "Coldplay Concert Ahmedabad",
    "isUsed": false,
    "mintDate": "2025-02-22T19:57:07.278"
}
```

---
# /marketplace
### Post /marketplace/list
helps to list the ticket in the database for reselling and bidding

req
```
{
  "tokenId": "6",
  "price": "870",
  "expiration": "2025-03-01T23:59:59Z"
}
```

res
```
{
    "listingId": "e5667a82-5b85-4151-a39e-ee6e3fb0ac10",
    "txPayload": "0x..."
}
```

### Post /marketplace/bid
this endpoint bid the listed tokens in the database

req
```
{
  "tokenId": "6",
  "bidAmount": "150"
}
```


res
```
{
    "bidNonce": "b22aae08-e45f-4ee8-b5de-805febcb5072",
    "txData": "0x...",
    "bid": {
        "tokenId": "6",
        "bidder": "0x1581d4149B3998795E9A17DaE91382b5E7541a78",
        "amount": "150",
        "timestamp": "2025-02-22T16:33:51.498Z"
    }
}
```

#### **Test Cases**:
1. **First Bid**:    
    - Request:  
        
        {
          "tokenId": "6",
          "bidAmount": "150"
        }
        
    - Expected: Bid is created successfully.
        
2. **Duplicate Bid**:    
    - Request:
        
        {
          "tokenId": "6",
          "bidAmount": "150"
        }
        
    - Expected: Returns `400 Bad Request` with the message `"You have already placed a bid for this ticket"`.
        
3. **Different Bid Amount**:    
    - Request:
        {
          "tokenId": "6",
          "bidAmount": "200"
        }
        
    - Expected: Returns `400 Bad Request` with the message `"You have already placed a bid for this ticket"`
      
### **Post /marketplace/purchase/:listingId**
this endpoint is used to transfer the token

---
# /events 

### GET /events/upcoming
upcoming events

req
```

```
Authentication token

res
```
[
    {
        "id": "94133c41-30a2-4888-bb9d-516e6974e857",
        "name": "Coldplay Concert",
        "venue": "DY Patil Stadium",
        "date": "2025-04-04T14:07:20",
        "seat_map": {
            "A1": "VIP",
            "A2": "VIP"
        },
        "ipfs_cid": "bafkreiavmyavtywzr2dmajs6r22u4povkbiubul4ux6jhs26qudz5yy3yy",
        "created_at": "2025-02-22T23:07:53"
    },
    {
        "id": "210351fa-0cd9-48e9-9c63-ca809a26302d",
        "name": "Coldplay Concert Ahmedabad",
        "venue": "Ahmedabad Stadium",
        "date": "2025-03-09T23:17:12",
        "seat_map": {
            "A1": "VIP",
            "A2": "VIP"
        },
        "ipfs_cid": "bafybeie6cfiyejs6jkcqzjy4lsckbtejda7ajzoofos5dnnxgcfb6nsqte",
        "created_at": "2025-02-22T23:17:46"
    },
    {
        "id": "be6bc5cf-50c5-4e83-a5dd-223110fdb50b",
        "name": "Coldplay Concert Kolkata",
        "venue": "Kolkata Stadium",
        "date": "2025-03-09T13:18:42",
        "seat_map": {
            "A1": "VIP",
            "A2": "VIP"
        },
        "ipfs_cid": "bafkreie2tfk4jxlrxaf42xsijhqkwk3osbqcjkeraoy3lcqiqavmu7cfxy",
        "created_at": "2025-02-22T23:19:38"
    },
    {
        "id": "13ce9bde-abc9-4f03-b3d5-102577ad3285",
        "name": "Dijit Dosanj Delhi concert",
        "venue": "Delhi Stadium",
        "date": "2025-04-19T23:20:26",
        "seat_map": {
            "A1": "VIP",
            "A2": "VIP",
            "B1": "General",
            "B2": "General"
        },
        "ipfs_cid": "bafkreiby3t6sgcfz5jcd2udde5622oy5siaobhar7qg5b3hyqm23mysc7y",
        "created_at": "2025-02-22T23:21:17"
    },
    {
        "id": "b1c0504b-4cb5-4e9e-96e8-fc4c80ef0f0b",
        "name": "Diljit India tour",
        "venue": "Eden Gardens",
        "date": "2025-04-25T23:22:01",
        "seat_map": {
            "B1": "General",
            "B2": "General"
        },
        "ipfs_cid": "bafkreictih5kwoii5x3t3lzy2gm2futbuxkfxqlcswsyvy4ddzplnrceia",
        "created_at": "2025-02-22T23:22:39"
    }
]
```


### POST /events/validate
this endpoint is used to validate the tickets

---
# /users

### GET /:address/tickets
helps to list the tickets related to this address

http://localhost:3005/users/0x1581d4149B3998795E9A17DaE91382b5E7541a78/tickets
req

nothing just Authentication Header

res
```
[
    {
        "id": "a2520c24-7d02-4560-b58b-eb9e55f87bf0",
        "token_id": "6",
        "event_id": "94133c41-30a2-4888-bb9d-516e6974e857",
        "owner_address": "0x1581d4149B3998795E9A17DaE91382b5E7541a78",
        "is_used": false,
        "mint_date": "2025-02-22T14:59:11.145"
    }
]
```

---

# /status

### /status/blockchain
this endpoint is used just to chec the blockchain status
just to get realtime info about how the blockchain is interacting with the app

req
no req needed 

res
```
{
    "chainId": "80002",
    "latestBlock": 18396700,
    "gasPrice": "36392980814"
}
```

---
# /auction
This endpoint will handle all the auction functoning and bidding using websockets

### GET /auction/:tokenId/bids
lists the token related bids

http://localhost:3005/auction/2/bids

req
///nothing needed just authentication headers

res
```
[
    {
        "id": "77be280e-051f-42eb-a2fc-41b2d4e9323d",
        "token_id": "2",
        "bidder_address": "0x1581d4149B3998795E9A17DaE91382b5E7541a78",
        "amount": 300,
        "created_at": "2025-02-22T21:06:05.977169"
    }
]
```
### **POST /auction/:tokenId/accept**
accepts the highest bid for a specific token

### POST /auction/bids
Places a bid on a specific ticket (`tokenId`)

req
```
{
  "tokenId": "2",
  "bidAmount": "350"
}

```

res
```
{
    "message": "Bid updated successfully",
    "bid": {
        "tokenId": "2",
        "bidder": "0x1581d4149B3998795E9A17DaE91382b5E7541a78",
        "amount": "350",
        "timestamp": "2025-02-22T21:53:01.132Z",
        "type": "update"
    }
}
```
### GET /auction/:tokenId
Fetches auction details for a specific ticket (`tokenId`).

http://localhost:3005/auction/2/bids

res
```
[
    {
        "id": "77be280e-051f-42eb-a2fc-41b2d4e9323d",
        "token_id": "2",
        "bidder_address": "0x1581d4149B3998795E9A17DaE91382b5E7541a78",
        "amount": 350,
        "created_at": "2025-02-22T21:06:05.977169"
    }
]
```

# Frontend Features
- not needed to upload events
- 