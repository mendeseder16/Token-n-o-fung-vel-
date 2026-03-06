# Token-n-o-fung-vel-

Para criar um NFT no OpenSea, você não precisa de um código específico. O processo é realizado através de uma interface gráfica. No entanto, se você estiver interessado em utilizar um contrato inteligente para criar e gerenciar NFTs, aqui está um exemplo simples de um contrato ERC721 em Solidity:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/utils/Counters.sol";

contract MyNFT is ERC721 {
    using Counters for Counters.Counter;
    Counters.Counter private _tokenIdCounter;

    constructor() ERC721("MyNFT", "MNFT") {}

    function mintNFT(address recipient) public returns (uint256) {
        uint256 newItemId = _tokenIdCounter.current();
        _mint(recipient, newItemId);
        _tokenIdCounter.increment();
        return newItemId;
    }
}
```

# Passos para usar o contrato

1. Instale o Node.js e Truffle: Você precisará do Node.js e do Truffle para compilar e implantar seu contrato.
   
   ```bash
   npm install -g truffle
   ```

2. Crie um novo projeto Truffle:

   ```bash
   mkdir MyNFTProject
   cd MyNFTProject
   truffle init
   ```

3. Adicione o contrato: Crie um novo arquivo em `contracts/MyNFT.sol` e cole o código acima.

4. Instale OpenZeppelin: Você precisará da biblioteca OpenZeppelin.

   ```bash
   npm install @openzeppelin/contracts
   ```

5. Compile o contrato:

   ```bash
   truffle compile
   ```

6. Implante o contrato: Crie um script de migração em `migrations/2_deploy_contracts.js`:

   ```javascript
   const MyNFT = artifacts.require("MyNFT");

   module.exports = function(deployer) {
     deployer.deploy(MyNFT);
   };
   ```

7. Faça a migração para a rede Polygon: Configure seu `truffle-config.js` para incluir a rede Polygon e depois execute:

   ```bash
   truffle migrate --network polygon
   ```

# Observação:
Você ainda precisará de uma carteira conectada (como MetaMask) para assinar transações e da sua conta da OpenSea para listá-los. Os passos anteriores sobre como conectar a OpenSea também se aplicam.

# Recursos Adicionais
- Documentação do OpenZeppelin
  - : Para personalizações adicionais em seu contrato.
- Documentação do Truffle: Para saber mais sobre como usar Truffle para implantar contratos inteligentes. 

Isso deve criar a base para que você possa desenvolver e implantar seu próprio NFT!
