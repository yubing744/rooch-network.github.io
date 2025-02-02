# 使用场景

本章节描述 Rooch 的特性，给应用带来的新的可能，和新的场景。

## DEX/Swap/DeFi

Rooch 的多链结算，可以让 DEX/Swap/DeFi 可以安全的汇聚更多的资产，从而获得更强的竞争力。


## 多链资产初始化发行

当前某种 Token 一般只发行在某个链上，然后通过跨链桥跨到其他链。但通过不同的跨链桥跨过去的资产类型可能是不一样的，这给用户造成了使用上的困惑。而通过 Rooch 的多链结算以及跨层状态迁移能力，可以实现资产在多个链上同时初始化发行，并且可以通过 Rooch 互通。

## 状态通道应用

Rooch 之上的状态通道可以执行智能合约。当前可以通过 P2P 方式连接的应用，都可以通过 Rooch 重构，利用流式支付或者 Token 经济模型来创建商业模式，不再依赖中心化服务的模式。

可能的应用场景：

1. P2P 游戏：Rooch 提供状态通道的结算以及欺诈证明能力。
2. 去中心化邮件/IM：Rooch 提供状态通道结算，可以支持 P2P 网络上的 DID 以及去中心化存储方案。

我们在状态通道应用的相关探索：

1. [Thor](https://github.com/starcoinorg/thor): 在闪电网络上实现基于 WASM 的智能合约引擎，通过第三方仲裁服务，玩家可以在闪电网络上进行游戏。
2. [Move 状态通道上的五子棋游戏](https://github.com/starcoinorg/stargate/tree/master/demo/Gobang)：一个 Move 状态通道的概念验证方案，实现了状态通道上的五子棋游戏，游戏逻辑通过 Move 实现。