# Carbon Credit Nex — Guia de Teste com Contratos Reais

## Arquivos entregues

| Arquivo | Descrição |
|---------|-----------|
| `CarbonCredit.sol` | Contrato inteligente completo (ERC-20 + retire) |
| `index.html` | Site com Web3 já configurado |
| `logo-carbon.jpg` | Logo |
| `hero-deploy.jpg` | Imagem principal |
| `logo-amazonia-carbon.svg` | Logo vetorial |

---

## Passo a passo para testar (5–10 minutos)

### 1. Preparar a carteira
1. Instale o **MetaMask**
2. Crie ou importe uma carteira
3. Mude para a rede **Sepolia**
4. Pegue ETH de teste em um destes faucets:
   - https://sepoliafaucet.com
   - https://www.alchemy.com/faucets/ethereum-sepolia
   - https://faucet.quicknode.com/ethereum/sepolia

### 2. Deploy do contrato no Remix
1. Abra https://remix.ethereum.org
2. Crie um arquivo `CarbonCredit.sol` e cole o conteúdo do arquivo entregue
3. Vá em **Solidity Compiler** → escolha versão `0.8.20` ou superior → **Compile**
4. Vá em **Deploy & Run Transactions**
5. Environment: **Injected Provider - MetaMask**
6. Confirme que está na rede **Sepolia**
7. Clique em **Deploy** e confirme a transação
8. **Copie o endereço do contrato** (aparece em "Deployed Contracts")

### 3. Configurar o site
Abra o `index.html` e localize estas linhas:

```js
const CONTRACTS = {
  carbonToken: "0x0000000000000000000000000000000000000000",
  retireContract: "0x0000000000000000000000000000000000000000"
};
```

Substitua pelos endereços reais (o mesmo endereço serve para os dois):

```js
const CONTRACTS = {
  carbonToken: "0xSEU_ENDERECO_AQUI",
  retireContract: "0xSEU_ENDERECO_AQUI"
};
```

Salve o arquivo.

### 4. Rodar o site
Recomendado usar um servidor local:

```bash
npx serve .
# ou
npx live-server
```

Abra o endereço que aparecer (geralmente http://localhost:3000).

### 5. Testar no site
1. Clique em **Conectar Wallet**
2. Aprove a conexão no MetaMask
3. O saldo real deve aparecer no Dashboard
4. Digite uma quantidade (ex: 100)
5. Clique em **Aposentar Créditos**
6. Confirme a transação no MetaMask
7. O saldo deve diminuir

### 6. Verificar no Etherscan
- Acesse https://sepolia.etherscan.io
- Cole o endereço do contrato
- Veja as abas **Transactions**, **Events** e **Contract**

---

## Funções disponíveis no contrato

| Função | Descrição |
|--------|-----------|
| `balanceOf(address)` | Consulta saldo |
| `retire(uint256)` | Aposenta (queima) créditos da sua carteira |
| `retireFrom(address, uint256)` | Aposenta de outra carteira (precisa de approve) |
| `mint(address, uint256)` | Cria novos créditos (só o owner) |
| `totalRetired()` | Total de créditos já aposentados |
| `transfer(address, uint256)` | Transfere créditos |

---

## Observações importantes

- O contrato usa **OpenZeppelin**. No Remix, marque a opção “Enable optimization” se quiser e use a versão do compilador compatível.
- Em produção, remova ou proteja a função `mint`.
- Para Polygon ou Ethereum Mainnet, basta mudar a rede no MetaMask e fazer o deploy novamente.
- O site já está preparado para detectar a rede e solicitar a troca automática para Sepolia.

---

## Suporte

Qualquer dúvida sobre o deploy ou integração, é só pedir.
