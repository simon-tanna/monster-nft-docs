# Labrys Monster NFT Internship Project

## Application Architecture Diagram

![Application Architecture Diagram](/docs/img/Labrys%20Monster%20NFT%20AAD%20Updated.png)

### AAD Elements

#### ERC20 Smart Contract

- The ERC20 implements the openzeppelin ERC20 standard with an added timelocked faucet function.
- Maximum number of Monster Coins to be minted is 1000000000.
- It will mint a maximum 1000 coins to the calling address once every 24 hours until the supply is exhausted.

#### ERC721 Smart Contract

- The ERC721 implements the openzeppelin ERC721URIStorage standard.
- Mints a random monster NFT (5 types) with random power level.
- Cost of minting monster is 15 monster coins.
- It will use VRFConsumerBaseV2 and VRFCoordinatorV2Interface to facilitate the choice of monster and the generation of random power attribute for minted NFT.

#### Polygon Test Network - Mumbai

- This is the test network on which both ERC20 and ERC721 smart contracts will be deployed.

#### Chainlink VRF

- The Chainlink VRF Oracle provides an off-chain generation of random values with proof of how the values were determined being published on-chain.

#### Provider - Alchemy

- Alchemy is the client that will allow the application front end to interact with the blockchain.

#### Open Sea

- NFT marketplace

#### Pinata

- A service that pins the minted NFT to IPFS Storage for reliable access to token

#### IPFS Storage

- A decentralized storage system

#### React/NextJs

- Framework used to build front-end UX/UI

#### Signer - MetaMask

Wallet provider that allows user to connect account and request a monster NFT.

### AAD Interactions

#### Front-End and Smart Contracts via Alchemy

The front-end will use Alchemy to connect to a node on the test-network to read the current state. When a user wants to request a monster, they will be required to sign the transaction by connecting to their MetaMask account.

#### Front-End to IPFS via Pinata (NFT Storage)

When a monster NFT is generated, the image and related metadata will be stored on IPFS. It will be 'pinned' to IPFS through the Pinata service.

#### ChainlinkVRF to ERC721 Smart Contract (Random Attribute Generation)

The ERC721 will have 2 functions that interact with the ChainlinkVRF:

- A request to mint an NFT that interacts with the VRF Coordinator Interface by sending the .
- A response that fulfills the requested random words(numbers) from chainlink and emits the minted NFT

#### NFT state to Open Sea

A minted monster NFT will be viewable on Open Sea via the token address.