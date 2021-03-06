##Handle NACK from Calvin-base

Below the program [Wireshark](https://www.wireshark.org/\#download) shows a NACK example from
Calvin-base and the code that handles a NACK. When Calvin-base sends a
NACK, the sequencenbr and token is not incremented in the method
sendToken. A new json-message is created, with the same content as
before, and resent to base without delay handling. The NACK from
Calvin-base becomes a delay when viewing the counter output.

###Wireshark communication

	...8{"to_rt_uuid": "calvin-arduino", "from_rt	_uuid":
	"babc045f-5da1-4eb1-a08e-95e6a272cfde", "cmd": 	"TUNNEL_DATA", "value":
	{"sequencenbr": 0, "peer_port_id":
	"50017184-4e7f-4f76-8c39-9e1f35f59b46", "cmd": 	"TOKEN_REPLY",
	"port_id": "be1fbbb2-9fb3-4bac-bb94-0e601f2df6df", 	"value": "NACK"},
	"tunnel_id": "fake-tunnel"}
	
###Handle NACK

	if(nextSequenceNbr) //if ACK
	{
		sequenceNbr++;
		lastPop[socket] = fifoPop(&actors[pos].inportsFifo[0]);
		request.set("data", lastPop[socket]);
	}
	else if(!nextSequenceNbr) // if NACK
	{
		request.set("data", lastPop[socket]);
	}
