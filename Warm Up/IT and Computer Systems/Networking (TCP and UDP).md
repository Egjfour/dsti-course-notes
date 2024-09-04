|            Course Name             |   Topic    | Professor |     Date      |                 Tags                 |
| :--------------------------------: | :--------: | :-------: | :-----------: | :----------------------------------: |
| **Warm-Up: Comp. Sci. & Networks** | Networking | Sebastien | 15 Avril 2024 | #ComputerEngineering #CloudComputing |

[Class Video Link](https://learn.dsti.institute/mod/url/view.php?id=17767)

# Summary
*Transmission Control Protocol (TCP) is the primary mechanism through which devices are able to exchange digital information. It is built on the principle that analog data can be chunked into packets to provide to digital systems. These packets contain metadata that allow devices to ensure proper delivery and reconstruction of the data being sent.*

# Key Takeaways
1. In early networking (telephones), physical connections were dynamically constructed to the nearest and available phone exchange until the physical target was located and connected
2. To allow analog data to be handled by digital machines, we chunk the data into packets
3. All <mark style="background: #FFB86CA6;">packets must be the same size</mark> to ensure algorithmic decidability

# Definitions
- Transmission Control Protocol (TCP): A <mark style="background: #FFB86CA6;">payload-based data transmission</mark> process that is agnostic to the physical layer of the networking media
	- This is what allows for the interconnection of networks (the Internet)
- Universal Datagram Protocol (UDP): Same as TCP with a critical difference in that the client and server <mark style="background: #FFB86CA6;">manage their own packet delivery acknowledgement system</mark>
	- Typically used in video streaming and gaming applications where it is not essential to receive 100% of the information to maintain the connection
- Packets: Subsets of a continuous data signal with metadata to ensure accurate delivery
	![[Packets.jpg]]

# Additional Resources
- [TCP Walkthrough (Khan Academy)](https://www.khanacademy.org/computing/computers-and-internet/xcae6f4a7ff015e7d:the-internet/xcae6f4a7ff015e7d:transporting-packets/a/transmission-control-protocol--tcp)
- [TCP/IP (Microsoft)](https://learn.microsoft.com/en-us/troubleshoot/windows-client/networking/tcpip-addressing-and-subnetting)
# Notes
## Networking Basics (Telephone Example)
- Networking is the first step in cloud computing
- Initial networks were telephone lines
	- These produced a <mark style="background: #FFB86CA6;">continuous electrical signal</mark> that had to be maintained to connect phones
	- Operated on the Plain Switched Telephone Network (PSTN) since operators had to physically switch people's connections
	- The PSTN allowed for both [[Computer Systems Basics|analog and digital data]]
		- Used different modulation and demodulation (modem)
- Since direct connections between all people would be physically and economically impractical, we instead connect to local phone exchanges (PEX)
	- Our connections to each other route through these exchanges taking the nearest available path until the destination is reached

## Payload Transmission (TCP)
- Since continuous signals were difficult to maintain, TCP (Transmission Control Protocol) was developed to digitize this procedure
- Packets
	- Continuous data is broken into subsets called packets
	- Each packet <mark style="background: #FFB86CA6;">independently</mark> goes through the various exchanges finding the next nearest and available point until it reaches its destination
- Hurdles to solve
	- Packets may not arrive in the correct order
	- Packets may never arrive
	- Packets may lose data along the way
- Metadata
	- Allows us to track the data and delivery of packets
	- Information includes a packet ID and a checksum
		- The checksum is an algorithmic hash of the payload which allows the recipient to check that they have received the data intended by the sender
- Reception Acknowledgment System
	- Allows the recipient to state that they are missing a payload
	- To have this, all packets must be of the same size to produce algorithmic decidability
	- The <mark style="background: #FFB86CA6;">UDP framework for networking does not include this </mark>feature and instead the client and server manage their own acknowledgement system

