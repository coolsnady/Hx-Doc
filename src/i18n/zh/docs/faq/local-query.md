智能合约 storage 区的数据可以通过合约接口来查询，但是这样会消耗手续费，并且需要等区块打包才能获得结果。对于一些不涉及到共识的简单
查询功能，合约支持本地查询接口（offline）。通过查询本地区块链数据，获得合约的当前数据状况，不但速度快，而且无需消耗手续费。