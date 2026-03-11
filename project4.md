[Back to Portfolio](./)

DIY Router
==========

-   **Class:** CSCI 332 – Applied Networking
-   **Grade:** C+
-   **Language(s):** C++
-   **Source Code Repository:** [GitHub](https://github.com/LIRiley-prog)  
    (Please [email me](mailto:Liriley@csustudent.net?subject=GitHub%20Access) to request access.)

## Project Description

The DIY Router project is a software-defined network router implemented in C++ as part of CSCI 332 – Computer Networks. The program simulates core routing functionality including packet forwarding, routing table management, and network address processing.

The project deepened understanding of how physical routers operate at the software level — including how packets are received, how routing tables are consulted to determine the next hop, and how data is forwarded across network interfaces. Key networking concepts applied include IP addressing, subnetting, and the logic behind both static and dynamic routing.

## How to Compile and Run the Program

```bash
g++ -o router router.cpp
./router
```

## UI Design

The DIY Router operates as a command-line application. Upon launch, the program initializes a routing table and begins processing simulated network packets. Users can interact with the router to:

- **View the routing table** — display all known routes, next hops, and interface assignments
- **Simulate packet forwarding** — input a destination IP address and observe which route the router selects
- **Add/remove routes** — manually modify the routing table to observe how forwarding decisions change

The console output clearly displays packet flow, routing decisions, and any routing errors (such as unreachable destinations).

## Additional Considerations

This project provided hands-on experience with the internals of network routing that goes beyond theoretical study. Implementing routing logic in C++ required careful attention to binary arithmetic for subnet masking, efficient lookup structures for the routing table, and handling edge cases such as default routes and unreachable hosts.

[Back to Portfolio](./)
