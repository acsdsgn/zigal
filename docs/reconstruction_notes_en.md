# Reconstruction Notes

---

## Procedure
The restoration was carried out as follows.

### 1. OCR of Machine Code
The dump listings published in the [magazine](#Published-Magazine) were scanned and converted into text data.  
This produced address fields and hexadecimal machine‑code text.  
Practically, the scanned images were uploaded to Google Drive and opened in *Google Document* to extract text.

### 2. Machine‑Code Repair
All work was performed using the spreadsheet software *Microsoft Excel*.

1. **Importing the dump listing**  
   The OCR‑converted machine‑code text was loaded into a worksheet.

2. **Checksum calculation**  
   The machine‑code values were converted to decimal, and both vertical and horizontal checksums were computed.

3. **Machine‑code data with checksums**  
   The decimal‑converted data and the computed checksums were displayed in hexadecimal.  
   This table was used to verify the correctness of the OCR process.  
   Any errors were corrected directly in the imported sheet.

4. **Formatting the dump listing**  
   The verified machine‑code data was formatted, and code for binary generation was produced.  
   This yielded the final machine‑code text data.

### 3. Generating and Loading Machine Code
Machine‑code data for use under N88 DISK‑BASIC was generated and tested to ensure correct loading.

1. **Adding BLOAD headers to the machine‑code text**  
   The header for each file is shown below.  
   These values can be derived from the BSAVE arguments listed later.

| File        | Start | Length | End  | Header (4 bytes) |
|-------------|-------|--------|------|-------------------|
| zigal.mai   | B900  | 162C   | CF2B | **00 B9 2B CF**   |
| zigal.cha   | 1000  | 1980   | 297F | **00 10 7F 29**   |
| title1      | 4B40  | 1B00   | 663F | **40 4B 3F 66**   |
| title2      | 6640  | 09C0   | 6FFF | **40 66 FF 6F**   |
| zigal.dat   | 7000  | 0F30   | 7F2F | **00 70 2F 7F**   |

The BLOAD header consists of four bytes representing the start and end addresses.  
DISK‑BASIC uses this information to determine the load location.

2. **Generating binary data**  
   The machine‑code text with BLOAD headers was converted into binary using `txt2bin102.exe`.  
   The resulting binary files were named appropriately for use with `d88disk.exe`.

3. **Writing binary data**  
   Using `d88disk.exe`, the BLOAD‑headered binaries were written to a blank d88 disk image created in a PC‑8801 emulator.

4. **Verifying binary loading**  
   DISK‑BASIC was launched in the PC‑8801 emulator, and each binary was loaded via BLOAD:

```
CLEAR, &HB8FF
BLOAD "zigalmain", &HB900
BLOAD "zigalchar", &H1000
BLOAD "title1", &H4B40
BLOAD "title2", &H6640
BLOAD "zigaldata", &H7000
```

Entering the monitor with the `mon` command, the `h]d(4‑digit hex address)` command was used to confirm that the binary data was placed correctly.

The correctly placed data was then saved onto a new disk:

```
BSAVE "zigal.mai", &HB900, &H162C
BSAVE "zigal.cha", &H1000, &H1980
BSAVE "title1", &H4B40, &H1B00
BSAVE "title2", &H6640, &H9C0
BSAVE "zigal.dat", &H7000, &HF30
```

The headers shown earlier can be computed from these BSAVE arguments.

### 4. Generating the BASIC Program
As with the machine code, the BASIC program was OCR‑converted into text.  
It was then loaded and saved in the PC‑8801 emulator M88 as follows:

```
cmd load "start.txt"
list
save "start"
```

With this, the files stored in [ZIGAL.d88](../ZIGAL.d88) were completed.

---

## Tools Used

- **M88 – PC‑8801 Emulator**  
  M88 Extension Module: DISKDRV v0.21  
  <http://www.remus.dti.ne.jp/~cisc/>

- **QUASI88 – PC‑8801 Emulator**  
  quasi88‑0.7.3‑win32  
  S. Fukunaga  
  <https://www.eonet.ne.jp/~showtime/quasi88/>

- **TXT2BIN**  
  txt2bin102.exe  
  Kensaku Fujita, 2000‑04‑19

- **d88disk Ver0.0.1**  
  d88disk.exe  
  hamiyun, 2015‑03‑29  
  <http://hamiyun.web.fc2.com/d88disk/d88disk.html>

- **bdump – Binary Dump Editor for Windows95**  
  bdump.exe  
  IMP

---

## Published Magazine
POPCOM Vol. 67, pp. 263–276, Shogakukan (Oct. 1988)
