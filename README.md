# Frunes-Fractional-Recursion-and-Context-Check-without-Indexer
by x1x@yopmail 

Frunes: Fractional Recursion and Context Check without Indexer

Data structure:
{

"tx-size limit including witdata":{
	"PUSHDATA length":0x4B(max, variable),
	"frunes-protocol-version":0x90-0x9F(current version 0x90)
	//0x??90 also set as the tx-size limit, max 0x4B90,19344 bytes. otherwise, parsing fails.
},

"edicts":[
	{"op":0xF(fractional share)/
		  0xA(mint called activate)/
		  0xC(context balance checkpoint)/
		  0xD(deploy)/
		  0xE(exchange)/
		  0xB(gamble)/
		  0x0(OP_RETURN & edicts END-FLAG)/
		  0x1(undefined Function)/0x2(?)/0x3(?).../0x8(?),
	"output":0x0-0xF},
	{"op":D(e.g.),"output":5(e.g.)},...
	//output can't Repeat, 0xC,0xE,0xB,0x0 appear only once,(0xC,0xF) appear together.
	//(0xC,0xF),0xA,0xD,0xE,0xB mutually exclusive with each other. 
],

"etching":{
# If 0xC and 0xF appear:
	"fraction proportions in edicts order":["F?":0x5F5E100(max numerator/1e8),"C?":0x0000002(e.g.),"F?":0x0000003,...,"F?":0x000000F],
	"output checkpoint balance":0x0000FFFF(65535 divided by 2/1e8 to check inputs and calculate recursively)
	//prescribe max 15 outputs, leave 1 output for OP_RETURN, maybe 73.5 bytes in total. The sum exceeds 1e8, parsing fails.
	//If the total balance of inputs < 1, the output checkpoint can't be set. And If no 0xC, parsing fails.
# If 0xA appear:
	"mint references in edicts order":["A?-deploy-tx":683951374e57694b4470535a6ea89f498bdf93b896171542688ddf4c73f2c82e,
							"A?-deploy-tx":683951374e57694b4470535a6ea89f498bdf93b896171542688ddf4c73f2c82e]				
	//prescribe max 2 outputs, maybe 68 bytes in total.
# If 0xD appear:
	"tickname": "Hex ASCII sequence of consecutive letters(a-z,A-Z) and numbers(0-9) at the head of txid", //h9Q7NWiKDpSZn
	"mint window interval blocks":0xA89F(e.g. max 0xFFFF, at the middle of txid),
	"lim":0x37(e.g. max 0x2E, at the tail of txid),
	"is tail-inflation out of the window & new lim":0x01(1 fixed,yes)/0x00(no),     //can't be omitted
	"is allowed to gamble":0x01(yes)/0x00(no)       //can't be omitted

	//The first three references are in the txid(tickname bytes + 3 bytes), deploy as a mint.
	//prescribe max 15 outputs, leave 1 output for OP_RETURN, maybe 19 bytes in total.
	//The longer the tickname, the more precious. Not recognized If the tickname length is less than 12,(max 29).
# If 0xE appear:
	"trade checkpoint balance":0x0000FFFF (sell 65535 tokens. no need to use fraction proportions, the surplus balance is burned)
	//like Brc-20, use SIGHASH_ANYONECANPAY | SIGHASH_SINGLE. E2 means output2 is the buyer's address.
	//WARNING:If no alignment hexes, tx-size including witdata may limited to minimum 0x0790(1936 bytes).
# If 0xB appear:
	"gamble after blocks":0x01(1 fixed),  //can't be omitted
	"this height+1 blockheader tail is odd":0x01(odd)/0x00(even),  //can't be omitted
	"gamble checkpoint balance":0x7FFFFFFF (no need to use fraction proportions, double If true, bruned If false)
	//Exceeds 0x7FFFFFFF, If true, the surplus balance is burned.
},

"alignment hexes":{0xABC...}
//Can be omitted
}

//Balance from inputs not processed is burned. The surplus balance based on the checkpoint is burned.
//If inputs have different tokens sources after recursion, all balances are destroyed. 1 UTXO carries 1 kind of Token.
//To prevent making up a transfer process to trick, (C,F,A,B,E) ops' txid must start with their tickname's first 6 Hexes.
//Fractional truncation, burning and destruction may occur, but the total token supply will ultimately inflate.
//If a deep mixes or a fake source is found, the UTXO and the transfer-chains must be banned, error UTXOs may burden the wallet.
//By coincidence,tick "Qlc7eV" in txid:516c63376556,d87c4779033327184ee00a08c4c14498e14673357ce4a791406b(1MB tx-size), 
	Optimized to set the tx-size limit: 0x??90(max 0x4B90,19344 bytes, including witdata). 
