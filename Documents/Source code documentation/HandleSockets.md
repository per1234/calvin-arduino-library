# HandleSockets

Classes
-------------------------
class **HandleSockets**

Includes
-------------------------
\#include \<inttypes.h\>

\#include "ArduinoJson.h"

Typedef
-------------------------
typedef unsigned char **BYTE**

Public Attributes
------------------
const char \* **EMPTY\_STR** = "\_$EMPTY$\_"

Public Member Functions
-------------------------
uint8\_t **setupConnection** (BYTE *macAdr)

uint8\_t **anyoneConnected** ()

uint8\_t **sendMsg** (uint8\_t socket, const char *str, uint16\_t length)

void **sendAllMsg** (uint8\_t socket)

String **recvMsg** (uint8\_t socket)

String **getMessagesIn** (uint8\_t index)

uint8\_t **addToMessagesOut** (String reply, uint8\_t socket)

void **prepareMessagesLists** ()

uint8\_t **recvAllMsg** ()

void **determineSocketStatus** ()

void **nextSocket** ()

uint8\_t **getSocketConnectionStatus** (int)

Member Function Documentation
----------------------------
	Manual IP-configuration
	Setting up Ethernet connection and Ethernet server listening on specified port.
	@param byte* MAC-address of the Ethernet-shield,
	@param IPAddress desired IP-address
### void **setupConnection** (BYTE *macAdr, IPAddress ipAdr)

 	DHCP-request
	Setting up Ethernet connection and Ethernet server listening on specified port.
	If first attempt fails, try another time before quitting.
	@param byte* MAC-address of the Ethernet-shield.
	@return returns 1 if success, 0 if failed to  IP-address through DHCP
### uint8\_t **setupConnection** (BYTE *macAdr)

	Check if anyone is connected.
	0 if no socket i connected, 1 if connected
	@return uint8_t statu
### uint8\_t **anyoneConnected** ()

	Sends a message to a specific socket.
	First sends the length in a separate packet then sends the actual message afterwards.
	@param uint8_t socket
	@param const char* message to send
	@param uint16_t length of the message
	@return uint8_t Check if length is handled right
### uint8\_t **sendMsg** (uint8\_t socket, const char *str, uint16\_t length)

	Sends all outgoing messages stored in messagesOut[] to corresponding socket.
	Also resets the message counter to 0 for the corresponding socket.
	@param uint8_t socket
### void **sendAllMsg** (uint8\_t socket)

	Receives a message from a specific socket.
	Begins message with a '{' to comply with the JSON TCP communication of Calvin Base
	@param uint8_t socket
	@return returns the string received from socket
### String **recvMsg** (uint8\_t socket)

	Returns the message stored in messagesIn on msgIndex
	@param uint8_t msgIndex
	@return String message
### String **getMessagesIn** (uint8\_t index)

	Adds message to outgoing message list.
	Returns 255 if messageOut[] is full, else the next index to place the outgoing message in.
	@param String reply, uint8_t socket
	@return uint8_t the next place to store outgoing message for specified socket
### uint8\_t **addToMessagesOut** (String reply, uint8\_t socket)

	Makes sure messagesOut and messagesIn is properly filled with the EMPTY_STR string.
### void **prepareMessagesLists** ()

	Loops through all sockets to see if anything is to be read.
	If data was received the message is stored in to messagesIn array.
	If no data found specific string to determine this is added to the corresponding index.
	@return uint8_t status, 0 if nothing received, 1 if anything was received.
### uint8\_t **recvAllMsg** ()

	Loops through all sockets and determine their connection status.
	W5100 and the Ethernet library has built in support for 4 sockets,
	hence the maximum connected sockets cannot exceed 4 without modification to the Ethernet library.
	If connected, stores the corresponding socket in socketConnectionList[].
	Else stores 255 if socket is disconnected
### void **determineSocketStatus** ()

	Controls which port to listen on next in order to add another socket once it becomes available.
	Simply chooses the next available socket with the lowest number.
### void **nextSocket** ()

	Determines if a specific socket is connected or not
	@Param uint8_t socketNbr, the socket to control.
	@Return int status, 1 if connected, else 0.
### uint8\_t **getSocketConnectionStatus** (int)




