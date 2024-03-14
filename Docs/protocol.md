@page protocol Supported Protocol

- [Futaba SBUS protocol](#sbusintro)
- [Crossfire RC protocol](#crsfintro)

# SBUS {#sbusintro}

The SBUS (Serial Bus) protocol is a digital communication protocol commonly used in radio-controlled (RC) systems for transmitting control signals between transmitters and receivers.

## Configuration

- Baud rate: 100000
- Data bits: 8 Bits
- Parity: Even Parity
- Stop bits: 2 Stop bits
- Signal polarity: Inverted

# CRSF {#crsfintro}

CRSF (Crossfire Serial Protocol) is a digital communication protocol designed for radio-controlled (RC) systems.

## Configuration

- Baud rate: 420000
- Data bits: 8 Bits
- Parity: No Parity
- Stop bits: 1 Stop bits
- Signal polarity: Uninverted

# Guide to Adding More Protocols

To add more protocols to your project, follow these steps:

1. **Create a New Protocol File** : Start by creating a new header file for each additional protocol you want to add. For example, if you want to add a protocol named "XYZ", create a file named `xyz_protocol.h`.

2. **Define Protocol Structure** : In the protocol header file (`xyz_protocol.h`), define the structure of the protocol, including any necessary constants, data structures, and functions.

3. **Implement Protocol Functions** : Implement the protocol functions in a corresponding source file (`xyz_protocol.cpp`). These functions should handle initializing the protocol, processing incoming data, and extracting channel information.

4. **Include Protocol Header** : In your main project files or wherever you want to use the protocol, include the header file of the protocol you've created (`#include "xyz_protocol.h"`).

5. **Initialize Protocol** : Initialize the protocol in your code by calling the initialization function provided by the protocol implementation.

6. **Process Incoming Data** : Call the function to process incoming data from the protocol whenever data is received.

7. **Extract Channel Information** : Use the provided function to extract channel information from the received data, if applicable.

## Basic Functions Required

For initializing the header of a new protocol, you'll typically need the following basic functions:

- `void begin()` : Initializes the protocol, sets up necessary parameters, and prepares for data reception.
- `void processIncoming()`: Processes incoming data from the protocol, including parsing and interpreting the received data.
- `void getChannels()`: Extracts channel information from the received data, if the protocol deals with channel data.

Here's a basic template for the header of a new protocol:

```cpp
#pragma once
#ifndef XYZ_PROTOCOL_H
#define XYZ_PROTOCOL_H

// Include any necessary headers
#include <Arduino.h>

// Define any constants or data structures specific to the protocol

class XYZProtocol : public serialIO {
public:
  explicit XYZProtocol(HardwareSerial &rxPort, int rxPin, int txPin,
                       bool inverted = false)
      : serialIO(&rxPort, rxPin, txPin, inverted){};
  ;
  ~XYZProtocol();

  void begin();
  void processIncoming();
  void getChannel(/* Parameters as needed */);

private:
  HardwareSerial *_serialPort;
  // Add any additional private members as needed
};

#endif // XYZ_PROTOCOL_H
```