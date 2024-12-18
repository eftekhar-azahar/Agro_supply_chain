Agro Supply Chain Smart Contract

Overview

The AgroContract is a Solidity-based smart contract designed for managing agricultural supply chains. It provides a decentralized platform where farmers can register, add and manage produce, and facilitate shipments while ensuring transparency and security.

Features

1. Farmer Management

Farmers can register themselves with their wallet address.

Farmer details include ID, name, and wallet address.

2. Produce Management

Farmers can add produce specifying:

Name

Quantity

Price per unit

Produce lifecycle statuses:

Planted

Harvested

Processed

Packed

Shipped

Received

3. Shipment Management

Create shipments associated with produce items.

Update shipment statuses.

4. Access Control

Owner Privileges: Certain functions are restricted to the contract owner.

Farmer Privileges: Only registered farmers can manage their own produce.

Event Logging: Events such as farmer registration, produce addition, and shipment updates are emitted for transparency.

Contract Structure

Enums

ProduceStatus: Defines the lifecycle of produce.

Structs

Farmer: Stores information about farmers.

struct Farmer {
    uint id;
    string name;
    address walletAddress;
    bool isRegistered;
}

Produce: Details about produce items.

struct Produce {
    uint id;
    string name;
    uint quantity;
    uint pricePerUint;
    ProduceStatus status;
    address owner;
}

Shipment: Information about shipments.

struct Shipment {
    uint id;
    uint productId;
    uint quantity;
    string destination;
    bool isShipped;
}

Mappings

Farmers and their wallet addresses.

Produce linked to farmers.

Shipments and their associated produce.

Deployment Instructions

Prerequisites

Node.js and npm installed.

Solidity Compiler (or use Remix IDE).

Wallet software (e.g., MetaMask).

Test ETH for deployment on a testnet.

Steps

Open Remix IDE and paste the smart contract code.

Select the Solidity Compiler and compile the code.

Deploy the contract:

Choose an environment (e.g., Injected Web3 for MetaMask).

Deploy the AgroContract.

Interact with the contract functions through the Remix interface.

Key Functions

1. Farmer Registration

function registerFarmer(string memory _name) external;

Registers a new farmer.

Emits the FarmerRegistered event.

2. Add Produce

function addProduce(string memory _name, uint _quantity, uint _pricePerUnit) external onlyRegisteredFarmer;

Adds new produce to the system.

Emits the ProduceAdded event.

3. Update Produce

function updateProduce(uint _produceId, uint _quantity, uint _pricePerUnit) external onlyProduceOwner(_produceId);

Updates the quantity and price of produce.

4. Add Shipment

function addShipment(uint _produceId, uint _quantity, string memory _destination) external onlyProduceOwner(_produceId);

Creates a new shipment for packed produce.

Emits the ShipmentAdded event.

5. Update Shipment Status

function updateShipmentStatus(uint _shipmentId, bool _isShipped) external onlyOwner;

Updates the shipment status.

Events

FarmerRegistered: Logs farmer registrations.

ProduceAdded: Tracks new produce added.

ProduceUpdated: Tracks updates to produce.

ProduceStatusUpdated: Logs status changes of produce.

ShipmentAdded: Logs new shipment creation.

Access Control Modifiers

onlyOwner: Restricts actions to the contract owner.

onlyRegisteredFarmer: Limits actions to registered farmers.

onlyProduceOwner: Ensures only produce owners can manage their items.

Future Enhancements

Integration with Chainlink Oracles: For real-time data and IoT integration.

Tokenized Payments: Adding a token-based payment system for transactions.

UI Integration: Developing a front-end dashboard for easy interaction.

License

This project is licensed under the GPL-3.0 License.
