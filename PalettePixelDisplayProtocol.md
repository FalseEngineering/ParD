# ParD Palette Pixel Display Protocol
ParD protocol name: "ParD-PALETTEPXLDSPL"

## Purpose and Requirements
Used to control palette-based colour pixel displays or display adapters over ParD ports. Each pixel is an index into a colour palette stored on the display. A compliant display device meets certain requirements:
- Display devices must store a palette. A palette is an array of 15 bit RGB colours with length 2, 4, or 16, corresponding to the pixel bit width.
- Display devices may have dimensions up to 4096 pixels by 4096 pixels.

## Protocol
The display responds to host transmissions where specified but doesn't otherwise initiate transmissions. All transmission sequences from the host begin with a 1 byte type code:
- 0x0: Capabilities query. The display responds with its width (16 bits), its height (16 bits), and its pixel bit width (8 bits).
- 0x1: Set palette. The host transmits a palette of 15 bit colours.
- 0x2: Begin display sequence. The host must send this before any other display transmissions. The display responds with 1 if it accepts or 0 otherwise.
- 0x3: Display sequence element. THe host transmits up to 254 bytes of pixels. The display must display as a single image a sequence of 0x3 messages between an accepted 0x2 message and an 0x4 message.
- 0x4: End display sequence.

## Notes
A 300 pixel by 200 pixel, 16 colour display takes 239 transmissions to fill.
