# src/ — Source Data

This directory contains the source materials used for reconstructing the game.

- dump  
  Corrected dump list with vertical/horizontal checksums  
  This is the authoritative source for the machine code.

- dump_nochksum  
  Dump list without vertical/horizontal checksums

- dump_bload  
  Clean dump list without checksums, with bload header
  Useful for reading or feeding into tools.

- bin  
  raw Binary

- bin_d88disk  
  Binary with bload header  
  Can be loaded directly via BASIC - BLOAD

---
These files are not meant to be edited manually.  
For details on how these were generated, see [reconstruction_notes_ja](../docs/reconstruction_notes_ja.md) or [reconstruction_notes_en](../docs/reconstruction_notes_en.md).