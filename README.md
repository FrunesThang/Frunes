# Frunes-Fractional-Recursion-and-Context-Check-without-Indexer
by x1x@yopmail 
Balance from inputs not processed is burned. The surplus balance based on the checkpoint is burned.
If inputs have different tokens sources after recursion, all balances are destroyed. 1 UTXO carries 1 kind of Token.
To prevent making up a transfer process to trick, (C,F,A,B,E) ops' txid must start with their tickname's first 6 Hexes.
Fractional truncation, burning and destruction may occur, but the total token supply will ultimately inflate.
If a deep mixes or a fake source is found, the UTXO and the transfer-chains must be banned, error UTXOs may burden the wallet.
By coincidence,tick "Qlc7eV" in txid:516c63376556,d87c4779033327184ee00a08c4c14498e14673357ce4a791406b(1MB tx-size), 
	Optimized to set the tx-size limit: 0x??90(max 0x4B90,19344 bytes, including witdata). 
