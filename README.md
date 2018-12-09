# ParD (Parallel Digital) Port
ParD is openly viewable but not licensed for use under any circumstances at this time.

## Overview
ParD is a general purpose computer peripheral port specification as well as a number of standardized protocols for common devices. This specification assumes a client/host relationship between devices: for example, a keyboard (client) connected to a personal computer (host).

ParD ports have 13 pins: 8 digital data pins, 1 host handshake pin, 1 client handshake pin, 1 host ground pin, 1 client ground pin, and 1 always-on host-powered pin. All ParD pins operate at 5 volts. Both the host and client device can initiate communication and transmit messages of up to 255 bytes. Messages are an 8 bit length packet followed by that many 8 bit data packets.

## Transmission
When not transmitting, the host and client handshake pins are 0. To initiate a transmission, the host sets data bit 0 to 1 and waits for the client's handshake bit to be 1. It then sets its own handshake bit to 1 and begins transmitting. The client may initiate a transmission in the same way but uses data bit 7 instead. If both host and client try to initiate a transmission at the same time, the client must accept the host's transmission.

A message is an 8 bit length packet followed by that many 8 bit data packets. Each packet is transmitted using the following protocol:
- A sender may set the value in the data pins while the receiver handshake bit is equal to the sender handshake bit.
- Once the pakcet is ready, the sender inverts its handshake bit. It may no longer change the data pins.
- The receiver receives the packet. It acknowledges the packet has been received by inverting its handshake bit. The sender may change the data pins again.

## Standardized Device Protocols
To assist device development, the ParD standard includes protocols for the following types of devices:
- Keyboards
- Text Buffer Displays
- Palette Pixel Displays
- Network Adapters
