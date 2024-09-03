### Opening connection: 3-way handshake
In HTTP 1.0 every new request required a new connection to be open. As per TCP, every new connection requires a three-way handshake. 

Here's how it works:

1. Client sends a SYN (synchronise) packet containing a random Initial Sequence Number (ISN) in the sequence field.
2. Server returns a SYN/ACK packet, containing server's own ISN in sequence field and client's ISN incremented by one in acknowledgement field.
3. Client sends an ACK (acknowledgement) packet containing server's ISN plus one in acknowledgement field. 

```
Client                          Server
  |                               |
  | ----------- SYN ------------> |
  | Seq = x                       |
  |                               |
  | <-------- SYN/ACK ----------- |
  | Seq = y, Ack = x + 1          |
  |                               |
  | ----------- ACK ------------> |
  | Ack = y + 1                   |
  |                               |
Connection Established
```

The handshake does a number of things:
- **Connection Establishment**: It ensures that both the client and server are aware of each other and agree to establish a connection. This mutual agreement is crucial for reliable communication.
- **Synchronization**: It synchronizes the [[sequence numbers]] between the client and server. Sequence numbers are used to keep track of the order of bytes sent and received, ensuring data integrity and proper sequencing.
- **Reliability**: By exchanging SYN and ACK packets, both parties confirm that their respective communication channels are open and functioning. This reduces the likelihood of data loss or corruption.
- **Flow Control**: The handshake allows both parties to negotiate the initial window size, which is used for flow control. This helps manage the rate of data transmission and prevents network congestion.
- **Error Checking**: The handshake process includes error-checking mechanisms to detect and handle issues such as packet loss, duplication, or corruption. 
### Maintaining connection
After initial sequence numbers are established, we can keep track of the data sent. Assuming only client sends data:
1. Client sends a packet of data with sequence number equal to ISN(c) + 1. That's the number of the first byte of data. He also sends data of length `len`
2. Server sends an acknowledgement packet with sequence number equal to the first byte of data it expects to receive in the next transmission. This is equal to ISN(c) + 1 + len, that is, previous SN plus length of data. 
3. Server's ack number is the number of the first byte of data to be sent by client. Client sends that data and the cycle repeats.
Conversely for server sending data to client. 
```
CLIENT                         SERVER
  |                               |
  | ----------- SYN ------------> |
  | Seq1 = ISN(c) + 1, len1 = z   | 
  |                               |
  | <---------- ACK ------------- |
  | Ack1 = Seq1 + 1               | = ISN(c) + 2 + len
  |                               |
  | ----------- SYN ------------> |
  | Seq2 = Ack1, len2 = y         |
  |                               |
  | <---------- ACK ------------- |
  | Ack2 = Seq2 + len2            |
```

### Closing connection: 4-way handshake
Assuming client wants to initiate closing the connection.
1. Client sends a FIN packet with the number of the last sent byte + 1
2. Server acknowledges the FIN packet by sending an ACK packet with SN equal to the FIN number plus one (so, last byte plus two).
3. Server sends a FIN packet with the sequence number equal to the number of the last byte *it* sent + 1
4. Client acknowledges the FIN packet by sending an ACK packet with sequence number equal to server's FIN number plus one (so, last byte plus two)
5. Connection is closed
```
CLIENT                         SERVER
  |                               |
  | ----------- FIN ------------> |
  | Seq(c) = x + 1                | x = number of last byte of client's data
  |                               |
  | <---------- ACK ------------- |
  | Ack(s) = Seq(c) + 1           | 
  |                               |
  | <----------- FIN ------------ |
  | Seq(s) = y + 1                | y = number of last byte of server's data
  |                               |
  | ---------- ACK -------------> |
  | Ack(c) = Seq(s) + 1           |
```

### Example:

```
CLIENT                          SERVER
  |                               |
  | ----------- SYN ------------> |
  | Seq = 69                      |
  |                               |
  | <-------- SYN/ACK ----------- |
  | Seq = 420, Ack = 70           |
  |                               |
  | ----------- ACK ------------> |
  | Ack = 421                     |
  |                               |
       Connection Established
       [Client sends data]
  |                               |
  | ----------- SYN ------------> |
  | Seq = 70, len = 30            | Seq = ISN(c) + 1 = SN of first byte
  |                               |
  | <---------- ACK ------------- |
  | Ack = 100                     | Ack = ISN(c) + length + 1
  |                               |
  | ----------- SYN ------------> |
  | Seq = 100, len = 5            |
  |                               |
  | <---------- ACK ------------- |
  | Ack = 105                     |
  
 [Conversly for server sending data]
 
  |                               |
  | <----------- SYN ------------ |
  | Seq = 421, len = 10           | Seq = ISN(s) + 1 = IS of first byte
  |                               |
  | ---------- ACK -------------> |
  | Ack = 431                     | Ack = ISN(s) + length + 1
  |                               |
  | <----------- SYN ------------ |
  | Seq = 431, len = 5            |
  |                               |
  | ---------- ACK -------------> |
  | Ack = 436                     |
  
 [Client decides to close connection]
 
  |                               |
  | ----------- FIN ------------> |
  | Seq = 106                     | Fin seq (c) = last SN(c) + 1
  |                               |
  | <---------- ACK ------------- | 
  | Ack = 107                     | Fin ack = last SN(c) + 1 + 1
  |                               |
  | <----------- FIN -------------| 
  | Seq = 437                     | Fin seq (s) = last SN(s) + 1
  |                               |
  | ----------- ACK ------------> | 
  | Ack = 438                     | Fin ack = last SN(s) + 1 + 1
		  Connection closed
```
