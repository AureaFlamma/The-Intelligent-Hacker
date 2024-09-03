# How the internet works

**RESOURCES**
[How does the Internet Work? (CS.FYI)](https://cs.fyi/guide/how-does-internet-work)
[What is the OSI Model?](https://www.cloudflare.com/en-gb/learning/ddos/glossary/open-systems-interconnection-model-osi/)

## Hardware
Computers on a network are connected to a router. Router is connected to a modem which converts our data into data manageable by a phone network (1). The phone network carries the data to an Internet Service Provider. ISP's manage special routers which connect to other ISPs' routers. 
###### Figure 1
![](internet-schema-7%202.png)

(1) - dial-up internet (now obsolete), DSL and Cable use the telephone network. Wireless and Fibreoptic don't- but the underlying mechanics are the same regardless of the kind of connection. 

## Open systems Interconnection (OSI) Model
[OSI Model diagram](OSI%20Model.md)
1. **Physical Layer** 
2. **Data Link Layer**
3. **Network Layer** | IP
4. **Transport Layer** | TCP
5. **Session Layer** | [SSL/TLS](SSL%20and%20TLS.md)
6. **Presentation Layer**
7. **Application Layer** | [HTTP](HTTP.md)