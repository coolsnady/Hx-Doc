At any point in time while using the network, a user may initiate a withdrawal transaction, which includes withdrawing assets from other chains.
					
When a Senator receives a withdrawal transaction, they sign the transaction and will broadcast it to the network. When it comes to a Citizen's turn to produce a block, the Citizen will collect Senators' signatures and will verify whether at least 2/3 of Senators have signed the transaction. If the specified conditions are met, the transaction and all collected signatures are packaged into a block. Otherwise, the transaction will not be packaged, but will be handled by the next batch of citizens.
		
After a transaction is packaged into a block, the corresponding HIOU (such as HXBTC, HXLTC, etc.) tokens, owned by the user is destroyed. After verifying the transaction, the Senator first determines whether there is a large enough balance in the multi-signature hot wallet to facilitate the withdraw. If sufficient, a withdrawal transaction from a hot multi-signature wallet to the cash withdrawal address is signed by the Senators, and the withdrawal is enabled. If the balance is insufficient, an asset deposit from a multi-signature cold wallet to a multi-signature hot wallet is required. A Citizen will initiate the transfer process after the assets in the hot wallet are determined to be sufficient.
	
The Cross-link withdrawal process is divided into two steps:
					
1). When a user initiates a withdrawal request on the HyperExchange, the request is first packaged by the Citizen (average 2.5 seconds), and waits for no less than 2/3 of Senator's signatures enabling the withdrawal request to be collected. If more than one-third of Senator's do not approve the request, the transaction is voided.
	
2). When the packaged transaction collects 2/3 of signatures from Senators, it will generate a corresponding asset chain debit transaction. This transaction will be broadcasted by a Citizen to the corresponding asset chain for confirmation (meaning it will need to wait for a corresponding number of block confirmations e.g. BTC requires 6 confirmations). On the HyperExchange network, a Citizen packages this withdrawal transaction. When the transaction is approved, the cash withdrawal transaction is completed.

The specific technical implementation process is as follows:
					
After a user initiates a withdrawal application, a Citizen initiates the corresponding original transaction from the multi-signature address transfer to the user's target address, and the original transaction is packaged in the src_trx, and broadcasted to the HyperExchange.
					
After the Senator synchronizes to src_trx and verifies the transaction, the src_trx signature is wrapped to the sig_ trx and then the Citizen conducts the bookkeeping process.
					
When the network collects enough signatures from Senators, a Citizen packages those signatures to generate a complete implementation transaction, and then they call the corresponding asset chain's transaction broadcast interface through the light wallet component built into the Indicator, and then broadcasts this to the corresponding assets chain.
		 	 	 					
The underlying operational flow chart of this process is as follows:

<img class="hx-icon" src="/img/cross-chain-withdraw.svg" />
