# Swisstronik Tesnet Techinal Task 5 (Deploy Private NFT)

link : [Click!](https://www.swisstronik.com/testnet2/dashboard)

Feel free donate to my EVM address

EVM :

```bash
0x6f5c1bEB0Ae14D1422B4B3b874ac6D3d225f9940
```

## Steps

### 1. Clone Repository

```bash
git clone https://github.com/gadroen/swisstronik-deploy-private-nft.git
```
```bash
cd swisstronik-deploy-private-nft
```

### 2. Install Dependency

```bash
npm install
```

### 3. Set .env File

create .env file in root project

```bash
touch .env
```

add this to your .env file
```bash
PRIVATE_KEY="your private key"
```

### 4. Update Smart Contract (Skipp if you won't modify NFT name)

- Open contracts folder
- Open PrivateNft.sol file
- Feel free to modify token name and token symbol

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract PrivateNFT is ERC721, Ownable {
    uint256 private _currentTokenId = 0;

    event NFTMinted(address recipient, uint256 tokenId);
    event NFTBurned(uint256 tokenId);

    constructor(address initialOwner) ERC721("GadroenPrivate", "GDRPRVT") Ownable(initialOwner) {}

    function mintNFT(address recipient) public onlyOwner returns (uint256) {
        _currentTokenId += 1;
        uint256 newItemId = _currentTokenId;
        _mint(recipient, newItemId);

        emit NFTMinted(recipient, newItemId);
        return newItemId;
    }

    function burnNFT(uint256 tokenId) public {
        require(ownerOf(tokenId) == msg.sender, "Error: You're not owner");
        _burn(tokenId);
        emit NFTBurned(tokenId);

    }

    function balanceOf(address account) public view override returns (uint256) {
        require(msg.sender == account, "Error: You're not owner");
        return super.balanceOf(account);
    }
}

```

### 5. Compile Smart Contract

```bash
npm run compile
```

### 6. Deploy Smart Contract

```bash
npm run deploy
```

### 7. Mint Token

```bash
npm run mint
```

### 8. Finsihed

- Open the deployed-adddress.ts (location in utils folder)
- Copy the address and paste the address into testnet dashboard
- push this project to your github and paste your repository link in testnet dashboard
  
 #how to push ? 
```bash
git init
```
```bash
git add .
```
```bash
git remote set-url origin your_repo_link
```
```bash
git push -u origin main
```

by :
github : [gadroen](https://github.com/gadroen)
telegram : @EwinGadroen
//0x6f5c1bEB0Ae14D1422B4B3b874ac6D3d225f9940
