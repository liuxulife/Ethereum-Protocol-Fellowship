---
timezone: America/New_York
---

# 0xKJ

1. 自我介绍
    - Dr KJ，密码学和共识算法博士，Useful PoW 和 Minus Theory 发现者。
    - 近期向以太坊提出扩容方案 https://ethresear.ch/t/l1-improvement-based-on-minus-theory/21494
    - 由于仅仅熟悉 PoW 以太坊机制，对于 PoS 并不是太理解。所以来补课，并且试图搞清楚以太坊 L1 扩容的可能性和技术细节。

2. 你认为你会完成本次残酷学习吗？
    - 不一定！

## Notes

<!-- Content_START -->

### 2025.02.06

今天是首次参加残酷共学，由于基本上我已经手撸过一个完整的POW区块链了，对以太坊的虚拟机和MPT也有过动手经验，所以这次会主要把注意力放在之前不太熟悉的POS知识上，也希望能结合到代码层面，弥补对 https://github.com/ethereum/go-ethereum 和 https://github.com/prysmaticlabs/prysm 的认知。

今天主要熟悉 The Protocol 部分, 值得一看的主要是 https://epf.wiki/#/wiki/protocol/architecture ，在转向POS之后，仅仅运行geth已经不够，还要结合 prysm 运行 Beacon Node。
第一张图中User APIs可以理解为ETH RPC，以前我实现过 https://github.com/EcoPoW/BitPoW/blob/master/eth_rpc.py

Beacon APIs 和 validator 连接，结合这两天看的油管视频，prysm应该是可以运行成 Beacon Node 或者 validator 模式的，所以这里的 validator 应该是用来验证 POS 谁有权出块的验证，而不是对整个区块链或者 EVM 执行结果的验证。

Engine API 是 geth 和 prysm 之间通信的API，暂时还不知道具体工作内容。但是可以知道，如果 POS 算法得知当前节点现在有出块权，prism 应该第一时间主动通知 geth 切换到出块模式。

代码可以看到 https://github.com/prysmaticlabs/prysm/tree/develop/cmd 有 beacon-chain 和 validator 模式，以及其它模式。每个都会有对应的`main.go`代码。在运行 `func main` 之后进入 `func startNode`，`node.New` 和 `beacon.Start` 之后应该就跳转到https://github.com/prysmaticlabs/prysm/blob/develop/beacon-chain/node/node.go 去了。

今天就先研究到这里。

### 2025.02.07

<!-- Content_END -->
