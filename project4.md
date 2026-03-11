[Back to Portfolio](./)

DIY Router
==========

-   **Class:** CSCI 332 – Applied Networking
-   **Grade:** C+
-   **Language(s):** C++
-   **Source Code Repository:** [GitHub](https://github.com/LIRiley-prog)  
    (Please [email me](mailto:Liriley@csustudent.net?subject=GitHub%20Access) to request access.)

## Project Description

The DIY Router project was a hands-on networking project completed as part of CSCI 332 – Applied Networking. The project involved building a functional router from scratch — both the physical hardware and the software — to create a local area network (LAN) capable of transferring images and files between connected devices.

The hardware component included hand-crimping custom Ethernet cables and physically assembling the router setup. The software component was written in C++ and implemented the networking logic required to route traffic between devices on the same network, enabling one machine to send images and files directly to another through the DIY router.

This project bridged the gap between theoretical networking concepts and real-world hardware, giving direct experience with how data physically travels across a network — from the cable level all the way up to the application layer.

## How to Compile and Run the Program

```bash
g++ -o router router.cpp
./router
```

## UI Design

The program runs as a command-line application. Once the router is active and devices are connected via the custom Ethernet cables, users can:

- **Send a file or image** — specify a file path and the destination device on the network
- **Receive files** — the program listens for incoming transfers from other connected devices
- **View connection status** — see which devices are recognized on the local network

Transfers are confirmed in the terminal once the file is successfully received on the other end.

## Additional Considerations

One of the most valuable aspects of this project was the physical networking experience. Hand-crimping Ethernet cables required learning the T-568B wiring standard and testing each cable for continuity. Combined with the C++ socket programming needed to transfer data between devices, this project demonstrated a full-stack understanding of networking — from the physical layer to the application layer.

[Back to Portfolio](./)
