# Upgradable Smart Contract System with UUPS Proxy

A robust and secure upgradable smart contract system built with **Solidity**, leveraging the **UUPS (Universal Upgradeable Proxy Standard)** pattern from OpenZeppelin. This project demonstrates a modular and testable architecture for deploying and upgrading smart contracts, ensuring flexibility and future-proofing for decentralized applications.

---

## 🌟 Features

- **Upgradable Contracts**: Seamlessly upgrade contract logic using the UUPS proxy pattern while preserving state.
- **Secure Ownership**: Utilizes OpenZeppelin’s `OwnableUpgradeable` for access control, ensuring only authorized upgrades.
- **Tested with Foundry**: Comprehensive test suite using Foundry to verify deployment, upgrades, and functionality.
- **Modular Scripts**: Includes deployment (`DeployBox`) and upgrade (`UpgradeBox`) scripts for streamlined interactions.
- **Versioned Logic**: Supports multiple contract versions (`BoxV1`, `BoxV2`) with distinct functionality (e.g., value setting in `BoxV2`).
- **Developer-Friendly**: Built with modern tooling (Foundry, OpenZeppelin) and clear documentation for easy onboarding.

---

## 🛠️ Getting Started

### Prerequisites
- [Foundry](https://getfoundry.sh/) (for compiling, testing, and deploying contracts)
- Basic knowledge of Solidity and Ethereum smart contract development

### Installation

#### Clone the Repository
```bash
git clone https://github.com/rocknwa/Upgradable-Smart-Contarcts.git
cd Upgradable-Smart-Contarcts
```

#### Install Foundry
Ensure Foundry is installed. If not, run:
```bash
curl -L https://foundry.paradigm.xyz | bash
foundryup
```

#### Install Dependencies
Install required libraries using Foundry:
```bash
forge install 
forge install Cyfrin/foundry-devops
```

#### Build the Project
Compile the contracts:
```bash
forge build
```

---

## Project Structure

```
├── src/
│   ├── BoxV1.sol        # Initial contract implementation
│   └── BoxV2.sol        # Upgraded contract with additional functionality
├── script/
│   ├── DeployBox.s.sol  # Script to deploy the proxy and BoxV1
│   └── UpgradeBox.s.sol # Script to upgrade to BoxV2
├── test/
│   └── DeployAndUpgradeTest.sol # Test suite for deployment and upgrades
├── README.md            # Project documentation
└── foundry.toml         # Foundry configuration
```

---

## 🚀 Usage

### Deploying the Contract

Deploy the proxy contract with BoxV1 as the initial implementation:
```bash
forge script script/DeployBox.s.sol --rpc-url <YOUR_RPC_URL> --private-key <YOUR_PRIVATE_KEY> --broadcast
```
> This deploys an `ERC1967Proxy` pointing to `BoxV1`, initialized with ownership controls.

### Upgrading the Contract

Upgrade the proxy to BoxV2 (adds `setValue` functionality):
```bash
forge script script/UpgradeBox.s.sol --rpc-url <YOUR_RPC_URL> --private-key <YOUR_PRIVATE_KEY> --broadcast
```

### Interacting with the Contract

- **BoxV1**: Check the version (`version()`) or retrieve the stored value (`getValue()`).
- **BoxV2**: Set a new value (`setValue(uint256)`) and verify it (`getValue()`).

Example (using cast):
```bash
cast call <PROXY_ADDRESS> "version()" --rpc-url <YOUR_RPC_URL>
cast send <PROXY_ADDRESS> "setValue(uint256)" 42 --rpc-url <YOUR_RPC_URL> --private-key <YOUR_PRIVATE_KEY>
```
> **Remember to secure your private key!**

---

## 🧪 Testing

The project includes a comprehensive test suite (`DeployAndUpgradeTest.sol`) to verify:
- Successful deployment of BoxV1 via proxy.
- Correct version reporting (`version() == 1` for BoxV1).
- Inability to call BoxV2 functions before upgrading.
- Successful upgrade to BoxV2 and functionality (`setValue` and `getValue`).

Run tests with:
```bash
forge test
```
For detailed output:
```bash
forge test -vv
```

---

## 📖 Technical Details

### UUPS Proxy Pattern

The project uses OpenZeppelin’s `UUPSUpgradeable` for efficient and secure contract upgrades. Key benefits:

- **Gas Efficiency**: Upgrade logic is stored in the implementation contract, reducing proxy overhead.
- **Security**: Upgrades are restricted to the contract owner via `OwnableUpgradeable`.
- **Flexibility**: Supports iterative upgrades (e.g., from BoxV1 to BoxV2).

### Contracts

- **BoxV1**: A simple contract with a `value` state variable and `version()` returning 1.
- **BoxV2**: Extends BoxV1 with `setValue` functionality and `version()` returning 2.
- **ERC1967Proxy**: Standard proxy contract for delegating calls to the implementation.
- **DeployBox**: Script to deploy the proxy and initialize BoxV1.
- **UpgradeBox**: Script to upgrade the proxy to BoxV2.

### Foundry Integration

- **Testing**: Uses `forge-std` for testing utilities (`Test`, `StdCheats`, `console`).
- **DevOps**: Integrates `foundry-devops` to fetch the most recent proxy deployment.
- **Scripts**: Modular scripts for deployment and upgrades, compatible with Foundry’s scripting environment.

---

## 📬 Contact

For questions or collaboration, connect with me on  
**Email:** [anitherock44@gmail.com](mailto:anitherock44@gmail.com)
