# Rizulcoin 🚀


[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)   ![Token](https://img.shields.io/badge/Token-ERC_20-light_green)  [![OpenZeppelin](https://img.shields.io/badge/-OpenZeppelin-9b36d2)](https://www.openzeppelin.com/)


 

Rizulcoin is an ERC20 token contract that allows for the creation, transfer, and management of tokens. It is built on the [OpenZeppelin](https://www.openzeppelin.com/) library and follows the ERC20 standard.

## 🌟 Features


- 🏗️ Creation of tokens with a specified name and symbol.
- 💸 Token transfers between addresses.
- 🔥 Ability to burn tokens, reducing the total supply.
- 💎 Minting of tokens by the contract owner.
- 🤝 Approval and delegation of token transfers.

## 🚀 Usage

###  Deployment 🏗️

To deploy the contract, follow these steps:

1. Set the Solidity compiler version to at least `0.8`.
2. Import the necessary `IERC20` interface from the OpenZeppelin library.
3. Deploy the contract by providing the desired `name` and `symbol` for the token.

### Contract Owner 🥸

The contract owner has special privileges and is the only address allowed to perform certain operations. The following modifier ensures that only the owner can execute those functions:

```solidity
modifier onlyOwner {
    require(msg.sender == _owner, "Only owner is allowed to perform this operation");
    _;
}
```

## ℹ️ Token Information 

The contract maintains the following information:

- `_name`: The name of the token.
- `_symbol`: The symbol or ticker of the token.
- `_owner`: The address of the contract owner.
- `_totalSupply`: The total supply of tokens.

### Balances 💵

The contract keeps track of token balances for each address using a private mapping `mapping(address => uint256) private _balances;`

You can retrieve the balance of an address using the `balanceOf` function.
```solidity
function balanceOf(address account) external view returns (uint256);
```

### Transfers  🤝
Tokens can be transferred from one address to another using the `transfer` function. Before a transfer is executed, the contract checks if the sender has sufficient balance to cover the transfer amount. If not, an error is raised.
```solidity
function transfer(address to, uint256 value) public returns (bool);
```

### Burning Tokens 🔥
The contract allows for the burning of tokens, reducing the total supply. The `burn` function enables an address to burn a specified amount of their tokens. The sender's balance is reduced, and the total supply is updated accordingly.
```solidity
function burn(uint256 value) public returns (bool);
```

### Minting Tokens ⛏️

The contract owner can mint new tokens by using the `mint` function. This function increases the balance of the specified address and updates the total supply.
```solidity
function mint(address to, uint256 value) public onlyOwner returns (bool);
```

### Approvals and Allowances ✅

To delegate token transfers, the `approve` function allows an address to approve another address to spend a specified amount of tokens on its behalf. 

```solidity
function approve(address spender, uint256 value) external returns (bool);
```

This approval is stored in the `_allowances` mapping which can be accessed using the `allowances` function.

```solidity
function allowance(address owner, address spender) external view returns (uint256);
```

The `transferFrom` function is used to transfer tokens on behalf of another address. It checks the allowance of the sender before executing the transfer.
```solidity
function transferFrom(address from, address to, uint256 value) external returns (bool);
```


## 🔫 Events 

The contract emits the following events:

- `Transfer`: Triggered when tokens are transferred between addresses.
- `Approval`: Triggered when an approval is granted for token transfers.
- `Burn`: Triggered when tokens are erased by a user.
- `Mint`: Triggered when tokens are minted by the owner.

## ⚠️ Errors 

The contract defines several custom errors to handle exceptional situations:

- *`InvalidReceiver`*: Raised when an invalid receiver address (0x0) is specified.
- *`InsufficientBalance`:* Raised when a sender has an insufficient balance for a transfer or burn operation.
- *`InsufficientAllowance`*: Raised when the allowance is insufficient for a `transferFrom` operation.

These errors provide meaningful feedback when an exceptional condition occurs.

## 📄 License 

This contract is licensed under the [MIT License](https://opensource.org/licenses/MIT). You can find the license details in the SPDX-License-Identifier comment at the beginning of the contract.

**Note ▶:** Make sure to import the required OpenZeppelin library using the correct version and path (`@openzeppelin/contracts/token/ERC20/IERC20.sol`) before deploying the contract.
