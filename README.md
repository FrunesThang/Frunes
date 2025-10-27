Frunes: Fractional Recursion and Context Check without Indexer

Copyright (c) 2025, see the x1x@yopmail.fr

"etching":{
# If 0xC appears or appears with 0xF:
	"fraction proportions in edicts order":["F?":0x989680(max numerator/1e7),"C?":0x000002(example),"F?":0x000003,...,"F?":0x00000F],
	"output checkpoint balance":0x0000FFFF(65535 divided by 2/1e7 to verify inputs and calculate recursively)
	//Maximum 15 outputs prescribed, leaving 1 output for OP_RETURN (~66 bytes total). Parsing fails if sum exceeds 1e7.
	//Output checkpoint cannot be set if total input balance < 1. Parsing fails if 0xC is absent.
# If 0xA appear:
	"mint references in edicts order":["A?-deploy-tx":6f3975336743586b76506b7268727235344423fd991a761afb63c70679a22fe4,
						"A?-deploy-tx":6f3975336743586b76506b7268727235344423fd991a761afb63c70679a22fe4]				
	//Maximum 2 outputs prescribed (~68 bytes total).
# If 0xD appear:
	"tickname": "Hex ASCII sequence of consecutive letters(a-z,A-Z) and numbers(0-9) from txid head", //o9u3gCXkvPkrhrr54D
	"mint window interval blocks":0x23FD(example, max 0xFFFF, from txid middle),
	"lim":0xE4(example, max 0xFF, from txid tail),
	"tail-inflation out of window & new lim":0x01(1 fixed,yes)/0x00(no),     //cannot be omitted
	"gambling permission":0x01(yes)/0x00(no)       //cannot be omitted

	//First three references are in txid(tickname bytes + 3 bytes), deploying as a mint.
	//Maximum 15 outputs prescribed, leaving 1 output for OP_RETURN (~19 bytes total).
	//Longer ticknames provide higher precision. Ticknames with length < 4 are not recognized (max 32).
# If 0xE appear:
	"trade checkpoint balance":0x0000FFFF (sell 65535 tokens. Fraction proportions not required, surplus balance burned)
	//Similar to Brc-20, using SIGHASH_ANYONECANPAY | SIGHASH_SINGLE. E2 indicates output2 is buyer's address.
	//WARNING: Minimum tx-size including witdata may be limited to 0x0790(1,936 bytes) without alignment hexes.
# If 0xB appear:
	"gamble delay blocks":0x01(1 fixed),  //cannot be omitted
	"current height+1 blockheader tail parity":0x01(odd)/0x00(even),  //cannot be omitted
	"gamble checkpoint balance":0x7FFFFFFF (fraction proportions not required, double if true, burn if false)
	//Surplus balance burned if exceeding 0x7FFFFFFF when true.
}
