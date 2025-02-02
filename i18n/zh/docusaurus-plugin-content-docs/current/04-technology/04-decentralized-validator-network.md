# 去中心化的验证者网络

当前的 Layer2 方案中，排序器如何做到去中心化，一直是一个难题。如果排序器做不到去中心化，一方面有单点风险，排序器当机后整个网络就不可用，另外一方面也排序器作弊的风险。在交易被批量写到数据可用层以及共识层之前，排序器可以通过丢弃交易或者调整交易的顺序来作弊。

Rooch 在设计之初就考虑了这点，尝试构建一个去中心化的验证者网络。

## 验证者角色说明

* **排序器（Sequencer）**：给交易排序并执行交易，计算出状态树的根，以及交易累加器的根。
* **校验者（Verifier）**：从共识和数据可用层获取交易，执行并校验，如果发现结果有误，则向仲裁层发起欺诈证明。
  
排序器和校验者在 Rooch 中统称验证者（Validator）。

## 去中心化方案

由于 Layer2 的共识只需要确定交易顺序即可，交易执行的正确性可以通过挑战威慑来保证。而要保证交易顺序，只需要把交易（或者交易的哈希）写到承担共识层角色的 Layer1 即可。

所以 Layer2 要实现去中心化，并不需要再构建一个 PBFT 共识网络去决定交易顺序以及执行结果，只需要设计一套排序器的轮换机制以及 P2P 网络上的数据同步协议。

初步设计思路如下：

1. 任何人都可以通过抵押一定额度的 Token 来链上注册为验证者。
2. 每个 Epoch，链上的智能合约随机选择一个验证者作为排序器（可能需要间隔一个周期）。
3. 没被选上作为排序器的结点自动成为校验者。
4. 所有的验证者构成一个 P2P 网络，验证者收到的交易会转发给排序器，排序器排序执行后会转发给其他验证者，并带上交易执行后状态树的根以及[交易累加器证明](./03-transaction-accumulator-proofs.md)。


## 激励机制

当前的 Layer2 方案中，校验者运行节点并没有收益，除非是发现排序器的欺诈行为，挑战成功。但这个概率太小了，并不能构成运行校验者节点的动力。

而在 Rooch 中，任何验证者都有概率作为排序器，可以获得用户交易费（gas），验证者就有动力持续运行结点，扮演校验者的角色。

:::note

TODO 是否需要专门的验证者奖励需要进一步设计

:::