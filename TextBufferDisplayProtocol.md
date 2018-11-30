# ParD Text Buffer Display Protocol
ParD protocol name: "ParD-TEXTDSPL"

## Purpose and Requirements
Used to control text buffer displays over ParD ports. A compliant display device meets certain requirements:
- Display devices must be persistent; they don't require data to constantly be pushed to them.
- Display devices must support inidividual character colouring with at least 2 foreground and 2 background colours. THey may support up to 16 foreground and 16 background colours. The colours themselves are unspecified.
-- The character encoding of a display device is left unspecified, but the display must provide an 8 byte identifier of its supported encoding upon request.

## Protocol
The display device responds to a capabilities query but doesn't otherwise initiate transmissions. All transmission sequences from the host to the display begin with a type code:
- 0x0: Capabilities query. The display responds with its row width (1 byte), column height (1 byte), and character encoding identifier (8 bytes).
- 0x1: Set row. The host transmits several messages:
  - First, a message with the type code (0x1) and a row index (1 byte).
  - Second, a message with a colour byte for each character in the row. The high 4 bits of the colour byte are the foreground colour; the low 4 bits are the background colour.
  - Then, as many messages as necessary to transmit the row's character data. For a row of 8 bit characters, only one message is necessary.
- 0x2: Shift rows up. The display shifts all rows up by 1, discarding the top row and leaving the bottom row empty.
