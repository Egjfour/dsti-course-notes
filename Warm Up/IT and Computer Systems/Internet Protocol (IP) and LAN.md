|                 Course Name                  |   Topic    | Professor |     Date      |      Tags       |
| :------------------------------------------: | :--------: | :-------: | :-----------: | :-------------: |
| **Warm-Up: Computer Science and Networking** | Networking | Sebastien | 15 April 2024 | #CloudComputing |

[Class Video Link](https://learn.dsti.institute/mod/url/view.php?id=17767)

# Summary
*The internet protocol is an address provided to network-enabled devices which allows for transmission of data through specified [[Networking (TCP and UDP)|networking protocols]]. Since the number of addresses is limited, multiple devices are connected together through a local area network (LAN) which provides an internet access point (IAP). The devices on the LAN recognize each other using subnet mask resolution.*

# Key Takeaways
1. IP Addresses are masked values that are directly built into the CPU hardware
2. There are 3 mandatory values for ANY network card
	1. LAN IP Address
	2. Subnet Mask
	3. IP Address of the route/gateway
3. Subnet mask resolution process is what allows devices to recognize that they are on the same network
4. IP Ports are the channels which tell the server where [[Networking (TCP and UDP)|packets]] should be sent
5. The client includes the local TCP/IP port in the envelope

# Definitions
- Internet Protocol: This is what provides IP Addresses (like a telephone number)
- Network Address Translation Server: Mechanism in the home internet box that allows devices to switch back and forth between the Internet Access Point (IAP) and Local Area Network (LAN)
- Subnet Mask: A 32-bit value that distinguishes between the host bits and network bits of the IP Address which is used to allow devices to recognize if they are on the same network
- Masked Multiplication: The multiplication (in binary) of the destination IP with the subnet mask which allows devices to recognize they're on the same network (Subnet Mask Resolution)
- IP Port: A 16-bit integer value that contains information on where the information from the network call should be sent

# Additional Resources
-  [LAN and WAN (Amazon)](https://aws.amazon.com/compare/the-difference-between-lan-and-wan/#:~:text=In%20LANs%2C%20connections%20between%20devices,connections%20over%20the%20public%20internet.)
- [TCP/IP (Microsoft)](https://learn.microsoft.com/en-us/troubleshoot/windows-client/networking/tcpip-addressing-and-subnetting)
- [Role of a Subnet Mask (Geeks for Geeks)](https://www.geeksforgeeks.org/role-of-subnet-mask/)

# Notes
## Internet Protocol (IP)
- Internet protocol is what provides unique addresses to all internet-connected devices
	- Most devices uses IPv4 which is a 32-bit coded address made up of 4 blocks of number that go from 0 to 255
	- This means there are only 2^32 addresses that can be given out
- These addresses are built directly into the [[Central Processing Unit|hardware layer (CPU)]] which limits memory consumption and arithmetic computational needs
- Public vs Private Addresses
	- Both are *truly visible* to the public
	- The private address is what is used by the local area network
	- The public address is leased to a given device by the internet service provider and is where packets will be sent
	- The <mark style="background: #FFB86CA6;">public addresses are able to be shared among many devices</mark>
## Local Area Network (LAN)
- Allows multiple devices in relatively close proximity that are connected through routers and/or switches to transmit data to each other
- 3 Classes of LAN IPs
	- 16, 20, and 24-bit blocks
	- Ultimately the difference is just in how many hosts can be connected to the network
- The router is ultimately what identifies if the payload can stay inside the LAN or if it must instead go out into the internet
	- This is done by using the subnet mask to perform a <mark style="background: #FFB86CA6;">bit-wise multiplication</mark> with the destination IP address and sender IP address
	- The subnet mask resolution calculation is performed by the sender
## IP Ports
- These allow for multiple apps to make requests even to the same IP address for different information (Chrome tabs from the same website example)
- Both the <mark style="background: #FFB86CA6;">clients and server in a TCP/IP protocol must bind to a port</mark>
- The range 1025 to 10240 are where common services bind
	- Ex: HTTP is on port 80 and HTTPS is on port 443
	- Anything above 10240 is the "ephemeral range" which is where the client will bind to (local IP Port provided in the [[Networking (TCP and UDP)|TCP envelope]])