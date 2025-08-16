# CryptoZombies Game Contract

A blockchain-based NFT game built on Ethereum where players can create, battle, and trade unique zombies. This project implements the ERC721 standard for non-fungible tokens and includes a complete gaming ecosystem with breeding, combat, and ownership mechanics.

## Overview

CryptoZombies is a decentralized application (dApp) that allows users to:
- Create unique zombies with randomly generated DNA
- Battle other zombies to gain experience and level up
- Breed zombies with CryptoKitties for special hybrid offspring
- Trade and transfer zombie ownership as ERC721 tokens
- Upgrade zombie attributes through a fee-based system

## Smart Contract Architecture

### Core Contracts

#### 1. **ZombieFactory** (`zombiefactory.sol`)
- **Base contract** for zombie creation and management
- **Inherits from**: `Ownable`
- **Key Features**:
  - Zombie struct definition with DNA, level, stats, and cooldowns
  - Random DNA generation based on user input
  - Initial zombie creation with ownership tracking
  - SafeMath integration for secure arithmetic operations

#### 2. **ZombieFeeding** (`zombiefeeding.sol`)
- **Inherits from**: `ZombieFactory`
- **Key Features**:
  - Zombie breeding and multiplication system
  - CryptoKitties integration for cross-platform breeding
  - Cooldown management for zombie actions
  - DNA mixing algorithm for offspring generation

#### 3. **ZombieHelper** (`zombiehelper.sol`)
- **Inherits from**: `ZombieFeeding`
- **Key Features**:
  - Level-up system with fee requirements
  - Zombie name and DNA modification (level-restricted)
  - Owner withdrawal functionality
  - Utility functions for zombie management

#### 4. **ZombieAttack** (`zombieattack.sol`)
- **Inherits from**: `ZombieHelper`
- **Key Features**:
  - Combat system with probability-based outcomes
  - Win/loss tracking and statistics
  - Random number generation for battle results
  - Automatic leveling upon victory

#### 5. **ZombieOwnership** (`zombieownership.sol`)
- **Inherits from**: `ZombieAttack`, `ERC721`
- **Key Features**:
  - Full ERC721 NFT compliance
  - Token transfer and approval mechanisms
  - Ownership verification and balance tracking
  - Marketplace-compatible token standards

### Supporting Libraries and Interfaces

#### **Ownable** (`ownable.sol`)
- Access control mechanism for administrative functions
- Owner-only modifiers for sensitive operations
- Ownership transfer and renunciation capabilities

#### **SafeMath Libraries** (`safemath.sol`)
- **SafeMath**: Secure arithmetic for `uint256`
- **SafeMath32**: Secure arithmetic for `uint32`
- **SafeMath16**: Secure arithmetic for `uint16`
- Overflow and underflow protection

#### **ERC721 Interface** (`erc721.sol`)
- Standard NFT interface definition
- Transfer and approval event declarations
- Core NFT functionality requirements

## Game Mechanics

### Zombie Creation
- Users create their first zombie for free with a unique name
- DNA is generated using cryptographic hashing
- Each zombie has 16-digit DNA determining appearance and traits

### Combat System
- **Attack Probability**: 70% chance of victory
- **Victory Rewards**: Level up, win count increase, new zombie creation
- **Defeat Consequences**: Loss count increase, cooldown activation
- **Cooldown Period**: 1 day between battles

### Leveling and Upgrades
- **Level Up Fee**: 0.001 ETH per level
- **Name Change**: Available at level 2+
- **DNA Modification**: Available at level 20+
- **Experience Gain**: Through successful battles

### CryptoKitties Integration
- Feed zombies with CryptoKitties DNA
- Special breeding mechanics for kitty-zombie hybrids
- Cross-platform asset interaction

## Technical Specifications

### Solidity Version
```solidity
pragma solidity >=0.5.0 <0.6.0;
```

### Key Data Structures
```solidity
struct Zombie {
    string name;
    uint dna;
    uint32 level;
    uint32 readyTime;
    uint16 winCount;
    uint16 lossCount;
}
```

### Security Features
- **Access Control**: Ownable pattern implementation
- **Safe Arithmetic**: SafeMath libraries for all calculations
- **Input Validation**: Comprehensive require statements
- **Cooldown Systems**: Prevents spam and abuse

## Deployment Requirements

### Dependencies
- OpenZeppelin contracts (for ERC721 compatibility)
- Truffle or Hardhat development environment
- Ethereum testnet or mainnet access

### Gas Optimization
- Struct packing for reduced storage costs
- Efficient loops and array operations
- Minimal external calls and storage writes

## Usage Examples

### Creating a Zombie
```solidity
// First zombie is free
createRandomZombie("MyZombieName");
```

### Battle System
```solidity
// Attack another zombie (owner-only)
attack(myZombieId, enemyZombieId);
```

### Level Up
```solidity
// Pay 0.001 ETH to level up
levelUp(zombieId);
```

### ERC721 Operations
```solidity
// Transfer zombie to another address
transferFrom(from, to, tokenId);

// Approve marketplace for trading
approve(marketplaceAddress, tokenId);
```

## Security Considerations

### Access Control
- Owner-only functions for critical operations
- Token ownership verification for transfers
- Modifier-based permission system

### Random Number Generation
- Nonce-based randomness for battles
- Hash-based DNA generation
- Protection against predictable outcomes

### Economic Security
- Fee-based upgrades prevent spam
- Cooldown systems limit abuse
- Withdrawal mechanisms for owner

## Testing and Auditing

### Recommended Testing
- Unit tests for all contract functions
- Integration tests for cross-contract interactions
- Gas usage optimization testing
- Security audit by professional firms

### Known Limitations
- Random number generation could be improved with Chainlink VRF
- Consider implementing reentrancy guards
- Add pause functionality for emergency situations

## License

This project is licensed under the MIT License.

## Contributing

Contributions are welcome! Please ensure all changes maintain backward compatibility and include appropriate tests.

## Support

For questions or issues, please refer to the Solidity documentation and OpenZeppelin standards for ERC721 implementation details.
