# Degen Gaming Studio Token

## Overview

This is the smart contract Degen Gaming 🎮, game studio token, the `DGN` is a unique token that can to incentivize and reward players for their loyalty and active usage of the Degen Game Studio and their services.

The smart was written in Solidity and deployed to the Avalanche Fuji Testnet(C-chain).
The contract has functionalities that:

- Allows Degen Game Studio to `mint` or create new tokens and distribute them to players as rewards. Only the owner can mint tokens.
- Allows players to `transfer` their tokens to others.
- Allows players to `redeem` their tokens for items in the in-game store.
- Allows players to check their token balance, `balanceOf` at any time.
- Allows anyone to `burn` tokens, that they own, that are no longer needed.

## Demo Video

https://www.loom.com/share/7d8356918b474f6b82b6ec6bdb305297?sid=edfa6cc5-a6dc-495f-a66f-7b5e1630cdb1

The contract is deployed on the Avalanche Fuji Testnet(C-chain), [DegenToken](https://testnet.snowtrace.io/address/0x413Cb1E6eA2c683dCd111E1c3D3785D69566702c#code)

## Token Information

- **Name:** Degen
- **Symbol:** DGN

### Deployed and Verified Contract Address

0x413Cb1E6eA2c683dCd111E1c3D3785D69566702c

https://testnet.snowtrace.io/address/0x413Cb1E6eA2c683dCd111E1c3D3785D69566702c#code

### Functions

`Constructor` Initializes the ERC-20 token with the specified name and symbol.

- Sets the contract deployer as the owner.
- Mints and InitialSupply of `10e18` to the owner.

`mint()`,allows only the owner of the contract to mint new tokens.

```sh
 function mint(address to, uint256 amount) public onlyOwner {
        _mint(to, amount);
    }
```

`transfer`, allows players to transfer their tokens to others.

```sh
 function transfer(
        address to,
        uint256 value
    ) public virtual override returns (bool success) {
        require(balanceOf(msg.sender) >= value, "Insufficient balance");
        success = super.transfer(to, value);
    }
```

`redeemToken`, allows players to redeem their tokens for items in the in-game store.

```sh
function redeemToken(uint8 _itemID) public {
        if (_itemID >= itemId) revert ItemNotFound();

        transfer(
            IdToGameItemsInfo[_itemID].owner,
            IdToGameItemsInfo[_itemID].amount
        );
        IdToGameItemsInfo[_itemID].owner = msg.sender;
    }
```

`balanceOf`, allows players to check their token balance at any time.

```sh

function balanceOf(
        address _account
    ) public view override returns (uint256) {
        return super.balanceOf(_account);
    }

```

`burn`, allows anyone to burn tokens, that they own, that are no longer needed.

```sh
   function burn(uint _amount) public {
        // checks that balance is not greater that amount
        if (balanceOf(msg.sender) < _amount) revert InsufficientBalance();
        _burn(msg.sender, _amount);
    }

```

`createGameItems`, allows Degen game studio to create game items for its users.

```sh
 function createGameItems(
        string calldata _name,
        uint256 _amount
    ) public onlyOwner {
        itemId++;

        GameItemsInfo storage gameItemsInfo = IdToGameItemsInfo[itemId];

        gameItemsInfo.owner = msg.sender;
        gameItemsInfo.name = _name;
        gameItemsInfo.amount = _amount;

        IdToGameItemsInfo[itemId] = gameItemsInfo;
    }

```

## On-Chain Interactions and Testing on the Fuji testnet

https://testnet.snowtrace.io/address/0x413Cb1E6eA2c683dCd111E1c3D3785D69566702c

## Author

Ifeanyi
[@metacraftersio](https://github.com/ifeanyiugo)

## License

This project is licensed under the MIT License - see the LICENSE.md file for details.
