# EthersJS 学习

- 智能合约交互原理

  有两种办法：第一种是自己部署运行一个以太坊节点，第二种是通过 JSON RPC 服务连接一个以太坊节点与整个区块链交互。

  和以太坊交互，需要制作一个符合 EIP1193 规范的对象。

- ethers 库主要帮助解决：

  连接用户钱包，获取用户钱包信息

  连接以太坊节点，获取以太坊网络信息

  连接智能合约，读写智能合约中的状态

- 安装

  ```
  npm install ethers
  ```

---

## Ethers 的常用类与工具

目前的版本是 v6

这些常用操作都是通过 JSONRPC 与区块链交互的，所以他们都是**异步函数**

### Provider 提供者类

- Provider

  对于 `getDefaultProvider()` ，如果有已经在运行的以太坊节点，可以直接用 **`provider = new ethers.JsonRpcProvider(url)`** 连接， 使用 `getDefaultProvider()` 时，会使用 Infura、Alchemy 等提供的免费公共节点（速率有限），开发情况下可以自己去 Infura 申请一个 API 密钥。

  ```js
  import { ethers } from 'ethers'
  
  // 构建一个符合 EIP193 规范的对象 - 获取公开 RPC 服务
  const provider = new ethers.getDefaultProvider()
  
  // 获取区块高度
  const block = await provider.getBlockNumber()
  console.log('block number:', block)
  
  // 获取某个区块或钱包的余额 - (address)
  const balance = await provider.getBalance('0xD59F743E7267b1Ebb70472EB9cae62C45a60Af33')
  console.log('balance:', balance)
  
  // 获取 gas 费用
  const feeData = await provider.getFeeData()
  console.log('gas price:', feeData.gasPrice)
  
  // 获取某个地址或钱包的 nonce - (address)
  const nonce = await provider.getTransactionCount('0xD59F743E7267b1Ebb70472EB9cae62C45a60Af33')
  console.log('nonce:', nonce)
  
  // 查询智能合约的存储数据 - (address, position)
  const storage = await provider.getStorage('0xD59F743E7267b1Ebb70472EB9cae62C45a60Af33', 0)
  console.log('storage:', storage)
  
  // 获取当前网络 - 记得.toJSON()
  const network = await provider.getNetwork()
  console.log('network:', network.toJSON())
  
  // 获取区块信息 - 最新区块
  const blockInfo = await provider.getBlock(block)
  console.log('blockInfo:', blockInfo)
  ```

- **Infura 密钥**

  使用 provider 加 Infura 申请的密钥可以直接查我 base 主网和 base 测试网的余额

  ```js
  import { ethers } from 'ethers'
  
  const baseURL = 'https://base-mainnet.infura.io/v3/'
  const testURL = 'https://base-sepolia.infura.io/v3/'
  const myApiKey = '4829d010d1354b8cbc94369dc06ace36'
  const myAddress = '0x31cF062453Fdf76A34D0f11e50DFcC5baAe604f4'
  
  const provider = new ethers.JsonRpcProvider(baseURL + myApiKey)
  const balance = await provider.getBalance(myAddress)
  console.log('balance:', balance)
  ```
  
- 对于 nonce

  nonce 就是个计数器，用来确保交易顺序和网络安全。

  每个账户都有一个 nonce 值，确保同一个账户的交易按顺序进行，第一个交易是0，第二个交易是1，nonce 保证每笔交易都唯一，

---

### 精度转换 parseEther 与 formatEther

- 使用 parseUnits( ) 和 formatUnits( ) 可以转换单位

  ```js
  import { ethers } from 'ethers'
  
  // 1 以太币 = 10^18 wei - (string, number)
  const wei = ethers.parseUnits('1.0', 18)
  console.log('ethers to wei:', wei)
  
  // 将 wei 转换回来
  const ether = ethers.formatUnits(wei, 18)
  console.log('wei to ethers', ether)
  
  // 简易版 - 默认后面 18 个 0
  const wei2 = ethers.parseEther('1.0')
  console.log('ethers to wei2:', wei2)
  const ether2 = ethers.formatEther(wei2)
  console.log('wei2 to ethers', ether2)
  ```
  
  输出的 `ethers to wei: 1000000000000000000n` 最后的 n 是 js 中的 BigInt

---

### Signer 签名者类与 Wallet 钱包类

- Wallet 钱包类

  ```js
  // 创建随机钱包 - (provider?)
  const wallet = ethers.Wallet.createRandom(provider)
  
  // 创建钱包 - 参数(privateKey， provider?)
  // const wallet2 = new ethers.Wallet('', provider)
  
  // 获取钱包地址 - 标准格式，直接用 wallet.address 格式可能不标准
  const address = await wallet.getAddress()
  console.log('钱包地址:', address)
  
  // 获取钱包私钥
  console.log('私钥:', wallet.privateKey)
  
  // 获取钱包的余额 - (address)
  const balance = await provider.getBalance(wallet.address)
  console.log('余额:', balance)
  
  // 获取 gas 费用
  const feeData = await provider.getFeeData()
  console.log('gas 费用:', feeData.gasPrice)
  
  // 获取钱包的 nonce - (address)
  const nonce = await provider.getTransactionCount(wallet.address)
  console.log('nonce:', nonce)
  ```

- Signer 签名者类

  ```js
  const myAddress = '0x31cF062453Fdf76A34D0f11e50DFcC5baAe604f4'
  const wallet = new ethers.Wallet(privateKey, provider)
  
  // 使用钱包签名 - (message)
  const message = 'Tie-Niu'
  const signature = await wallet.signMessage(message)
  console.log('签名:', signature)
  
  // 用签名验证你是否拥有某私钥 - (message, signature)
  const address = ethers.verifyMessage(message, signature)
  console.log('verify:', address, '签名是否有效:', address === myAddress)
  ```

---

### 交易

- 转账

  ```js
  import { ethers } from 'ethers'
  
  const baseURL = 'https://base-mainnet.infura.io/v3/'
  const testURL = 'https://base-sepolia.infura.io/v3/'
  const myApiKey = '4829d010d1354b8cbc94369dc06ace36'
  const myAddress = '0x31cF062453Fdf76A34D0f11e50DFcC5baAe604f4'
  const privateKey = '4fcb76cd38569b73319495e2c62a6445a8cd3f62570f0c19a875b35da3de83b5'
  const hisAddress = '0xFC6eec11b50042aDc69A3D65642eee3D271D09Da'
  
  const provider = new ethers.JsonRpcProvider(testURL + myApiKey)
  
  // 创建钱包 - (privateKey， provider?)
  const wallet = new ethers.Wallet(privateKey, provider)
  const myBalance = await provider.getBalance(myAddress)
  const hisBalance = await provider.getBalance(hisAddress)
  console.log('转账前', '我的余额:', myBalance, '他的余额:', hisBalance)
  
  // 创建交易
  const tx = {
      to: hisAddress,
      value: ethers.parseEther('0.001')
  }
  
  const txRes = await wallet.sendTransaction(tx)
  // 等待链上确认交易
  const receipt = await txRes.wait()
  // 打印交易收据
  console.log(receipt)
  const myBalance2 = await provider.getBalance(myAddress)
  const hisBalance2 = await provider.getBalance(hisAddress)
  console.log('转账后', '我的余额:', myBalance2, '他的余额:', hisBalance2)
  ```

---

## 合约

以太坊上的智能合约就是区块链上的代码，相当于在前端调取后端接口。**智能合约也是一个以太坊账户**。用户可以通过提交交易来调用合约上的函数来与合约交互。且**任何人都可以部署合约到区块链上**。

### 合约交互

- 创建合约实例

  ```js
  new ethers.Contract(address, abi, signer/provider)
  ```

  其中，第二个参数 abi 是合约的接口，abi 是一大段可读性很差劲的字符串，可以在区块链浏览器的合约详情里查到，当然可以使用人类可读 abi，可以更直观的看到调用的方法。（是一个字符串数组的格式）

  ```js
  const abiWETH = [
      "function balanceOf(address) public view returns(uint)",
      "function deposit() public payable",
      "function transfer(address, uint) public returns (bool)",
      "function withdraw(uint) public",
  ];
  ```

  第三个参数是签名者/提供者，决定了合约的读与写。

- 查询余额与 WETH 转换

  ```js
  const provider = new ethers.JsonRpcProvider(testURL + myApiKey)
  const wallet = new ethers.Wallet(privateKey, provider)
  
  // base sepolia 的 WETH9 合约地址
  const contractAddress = '0x4200000000000000000000000000000000000006'
  // 合约的 abi
  const abiWETH = [
      "function balanceOf(address) public view returns(uint)",
      "function deposit() public payable",
      "function transfer(address, uint) public returns (bool)",
      "function withdraw(uint) public",
  ]
  
  // 声明可写合约
  const contract = new ethers.Contract(contractAddress, abiWETH, wallet)
  // 读取 WETH 合约的链上信息（WETH abi）
  const balanceWETH = await contract.balanceOf(myAddress)
  const balance = await provider.getBalance(wallet.address)
  console.log('账户中的 WETH 余额:', balanceWETH, 'ETH 余额', balance)
  
  // 调用合约的转换方法，将 ETH 转换为 WETH
  const tx = await contract.deposit({ value: ethers.parseEther('0.001') })
  // 等待交易上链
  await tx.wait()
  const balanceWETH2 = await contract.balanceOf(myAddress)
  const balance2 = await provider.getBalance(wallet.address)
  console.log('账户中的 WETH 余额:', balanceWETH2, 'ETH 余额', balance2)
  ```

  打印结果为：

  ```
  账户中的 WETH 余额: 0n ETH 余额 98999926817582498n
  账户中的 WETH 余额: 1000000000000000n ETH 余额 97945176703896444n
  ```

- 调用 WETH 的转账合约

  ```js
  const contractAddress = '0x4200000000000000000000000000000000000006'
  const abiWETH = [
      "function balanceOf(address) public view returns(uint)",
      "function deposit() public payable",
      "function transfer(address, uint) public returns (bool)",
      "function withdraw(uint) public",
  ]
  
  const contract = new ethers.Contract(contractAddress, abiWETH, wallet)
  const balanceWETH1 = await contract.balanceOf(myAddress)
  const balance1 = await contract.balanceOf(hisAddress)
  console.log('他的 WETH 余额:', balance1, '我的 WETH 余额:', balanceWETH1)
  
  // 调用合约给另一个地址转帐 WETH
  const tx = await contract.transfer(hisAddress, ethers.parseEther('0.001'))
  await tx.wait()
  const balanceWETH2 = await contract.balanceOf(myAddress)
  const balance2 = await contract.balanceOf(hisAddress)
  console.log('他的 WETH 余额:', balance2, '我的 WETH 余额:', balanceWETH2)
  ```

### 检索事件

- queryFilter 检索特定事件

  注意这个事件必须放在 abi 里

  ```js
  const contractAddress = '0x4200000000000000000000000000000000000006'
  const abiWETH = [
      "event Transfer(address indexed from, address indexed to, uint amount)"
  ]
  
  const contract = new ethers.Contract(contractAddress, abiWETH, provider)
  
  // 获取过去十个区块的 Tranasfer 事件
  const block = await provider.getBlockNumber()
  // 检索释放过的事件, 必须在 abi 中 - (事件名, 起始区块?, 结束区块?)
  const transferEvents = await contract.queryFilter('Transfer', block - 10, block)
  // 返回数组, 用一个事件 transferEvents[0] 返回转账信息
  const amount = ethers.formatEther(ethers.getBigInt(transferEvents[0].args['amount']))
  console.log('地址:', transferEvents[0].args['from'], '转账', amount, 'WETH 到地址', transferEvents[0].args["to"])
  ```

  打印结果为：

  ```js
  地址: 0x043d4D9220727FE9eFaC096eAF4FC91EAD39a5Cb 转账 0.000000000017 WETH 到地址 0x362fDBB20191ba22d53bF3b09646AA387Cd6dF75
  ```

### 监听合约事件

- Contract.on 持续监听事件


---

## 连接 MetaMask 钱包

首先在浏览器里安装 MetaMask 钱包。

浏览器会给每个页面注入一个 `window.ethereum` 对象，用于和钱包交互。`ethers.js`提供的 `BrowserProvider` 封装了一个标准的浏览器 Provider，直接在程序中生成一个 provider 对象，下面是两种连接 metamask 钱包的方法：

1. 使用 web3Provider 包装器

   ```js
   const provider = new ethers.providers.Web3Provider(window.ethereum)
   await provider.send("eth_requestAccounts", []) 				// 请求账户权限
   const signer = provider.getSigner() 									// 获取 signer
   ```

   比较简洁，但只适用于 metamask 钱包。

2. 项目中使用 detectEtheumProvider 库 + **BrowserProvider**

   **@metamask/detect-provider** 是一个第三方库，库下面有这个 `detectEthereumProvider` 方法，可以检测用户的浏览器里有没有安装以太坊钱包，如 MetaMask，监测到钱包则会返回 window.ethereum 这个对象

   ethers.BrowserProvider( ) 这个方法用来封装浏览器中的以太坊 provider，比如 metamask，接受 window.ethereum ，包装成 provider 实例。

   ```js
   let accounts: string[] = []
   const ethereum = await detectEthereumProvider()									// 检测并获取是否有第三方钱包插件
   const provider = new ethers.BrowserProvider(ethereum) 
   if (walletType === 'WALLETCONNECT') {
       accounts = await provider.provider.enable() 								// WalletConnect 用 enable
   } else {
       accounts = await provider.send('eth_requestAccounts', []) 	// MetaMask 用 eth_requestAccounts
   }
   ```

   避免使用 window.ethereum，在多钱包环境更安全。

   对于 `await provider.send('eth_requestAccounts', [])` ，这是个 JSON-RPC 请求，发送到以太坊钱包以获取账户权限，空数组是参数列表，就算没有参数也要传空数组。

   用户同意授权后，accounts 就会是一个可能包含多个账户地址的数组。

---

