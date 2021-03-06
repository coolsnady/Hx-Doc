## 跨链充值流程

用户在 HyperExchange 中除了有 HyperExchange 账户外，还拥有若干个绑定的隧道账户，通过 HyperExchange 包含的其他资产链的轻钱包组件，用户可以从其他资产链地址或从中心化交易所中充值到 HyperExchange 账户绑定的隧道账户地址里。

HyperExchange 上的 Citizen 检测到关联的多重签名的充值地址收到转账后，等待块数到达一定确认高度后，根据充值的来源地址，找到关联的
HyperExchange账户，并在HyperExchange上共识给这个账户地址相应的HIOU（例如 HXBTC/HXLTC 等）。此时 HIOU（例如 HXBTC/HXLTC 等）默认为冻结资产(m 块)，等待 HyperExchange 块数达到一定高度（比如 m+17）后共识生成的 HIOU（HXBTC/HXLTC 等）资产从冻结状态转为可用状态。
在 HyperExchange 上充值分为以下环节：

1、用户充值到 HyperExchange 账户绑定的隧道账户里，这个交易确认依赖于原资产链上确认时间，如 BTC 延迟 6 块确认，LTC 延迟 12 块确认。

2、从隧道账户转账到由 Senator 共识管理的多重签名地址里。这个交易确认同样依赖于原资产链上确认时间，如 BTC 延迟 6 块确认，LTC 延迟 12块确认。

3、HyperExchange 上 Citizen 通过共识在 HyperExchange 上给用户生成对应的 HIOU，并等待 HyperExchange 上区块延迟 17 个区块后确认。

跨链充值的底层操作流程图如下：

<img class="hx-icon" src="/img/cross-chain-deposit.svg" />

在实际操作中，Indicator 会在人机交互上包装简化大部分流程，用户只需要比较简单的步骤即可完成跨链充值。