# Agriculture Supply Chain Management Smart Contract

A Clarity smart contract for managing agricultural supply chains on the Stacks blockchain. This contract enables tracking, quality control, and stakeholder management throughout the agricultural product lifecycle.

## Features

### Stakeholder Management
- Registration of supply chain participants (farmers, distributors, retailers, etc.)
- Stakeholder status tracking and scoring
- Role-based access control

### Product Management
- Product registration with unique identifiers
- Product state tracking
- Quality score monitoring
- Location tracking
- Ownership transfer management
- Price tracking

### Transaction History
- Comprehensive transaction logging
- Timestamped state changes
- Quality assessment records
- Location updates
- Ownership transfers

## Core Functions

### Administrative Functions
- `register-stakeholder`: Register new supply chain participants
- `update-stakeholder-status`: Modify stakeholder active status

### Product Management Functions
- `register-product`: Create new product entries
- `update-product-state`: Modify product status
- `transfer-ownership`: Transfer product ownership between stakeholders
- `update-quality-rating`: Update product quality assessments
- `update-location`: Track product movement

### Read-Only Functions
- `get-product-details`: Retrieve product information
- `get-stakeholder-details`: Access stakeholder data
- `get-transaction-details`: View transaction history

## Data Structures

### Stakeholder Registry
```clarity
{
    stakeholder-type: (string-ascii 20),
    stakeholder-status: bool,
    stakeholder-score: uint
}
```

### Product Registry
```clarity
{
    name: (string-ascii 50),
    original-producer: principal,
    current-owner: principal,
    current-state: (string-ascii 20),
    quality-score: uint,
    creation-time: uint,
    physical-location: (string-ascii 100),
    current-price: uint,
    quality-verified: bool
}
```

### Transaction History
```clarity
{
    from-party: principal,
    to-party: principal,
    action-type: (string-ascii 20),
    action-time: uint,
    action-details: (string-ascii 200)
}
```

## Error Codes
- `ERR_NOT_AUTHORIZED (u1)`: Unauthorized access attempt
- `ERR_PRODUCT_DOES_NOT_EXIST (u2)`: Product ID not found
- `ERR_INVALID_STATUS_CHANGE (u3)`: Invalid state transition
- `ERR_PRODUCT_ALREADY_EXISTS (u4)`: Duplicate product ID
- `ERR_INVALID_PARAMETER (u5)`: Invalid input parameters

## Input Validation
- String length validation for all text inputs
- Number range validation for numeric inputs
- Authorization checks for all operations
- Status validation for stakeholders

## Usage Example

1. Register a stakeholder (farmer):
```clarity
(contract-call? .agriculture-supply-chain register-stakeholder 'ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM "farmer")
```

2. Register a product:
```clarity
(contract-call? .agriculture-supply-chain register-product 
    u1 
    "Organic Tomatoes" 
    "Farm A, Field 3" 
    u1000)
```

3. Update product quality:
```clarity
(contract-call? .agriculture-supply-chain update-quality-rating 
    u1 
    u85 
    "Quality inspection completed - Grade A")
```

## Security Considerations

- Only registered stakeholders can perform operations
- Ownership verification for product modifications
- Contract owner has exclusive administrative rights
- Input validation for all parameters
- Quality verification requirements