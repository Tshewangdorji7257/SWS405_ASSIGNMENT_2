# Lab 1 — Beginner's Luck: Investigation Log

## 1. Objective
Investigate the Windows memory dump to recover three flags and reconstruct the user's activities before the system crashed.

## 2. Environment
- Operating system: Kali Linux
- Tool: Volatility Framework 2.6.1
- Memory image: MemoryDump_Lab1.raw
- Profile: Win7SP1x64

## 3. Investigation Steps

### Step 1: Identify the memory profile
**Command:** `imageinfo`

**Finding:** The memory image was examined to identify the appropriate Windows profile. `Win7SP1x64` was selected for subsequent analysis.

### Step 2: Examine running processes
**Commands:** `pslist`, `pstree`

**Finding:** The process listings showed applications including `cmd.exe`, `mspaint.exe`, `WinRAR.exe`, and `DumpIt.exe`.

### Step 3: Examine command and console history
**Commands:** `cmdscan`, `consoles`

**Finding:** Console history contained a Base64-encoded string. After decoding it, Flag 1 was recovered.

**Flag 1:** `flag{th1s_1s_th3_1st_st4g3!!}`

### Step 4: Investigate the Paint process
**Command:** `memdump -p 2424 -D <output-directory>`

**Finding:** The memory of `mspaint.exe` was extracted and examined using GIMP's raw-data import feature to investigate image data.

**Flag 2:** [Insert the exact flag you recovered]

### Step 5: Locate and extract the archive
**Commands:** `filescan`, `hashdump`, `dumpfiles`

**Finding:** The `Important.rar` archive was located in memory and extracted. The account hash was used to determine the archive password, allowing the image containing Flag 3 to be recovered.

**Flag 3:** [Insert the exact flag from flag3.png]

## 4. Forensic Reasoning
The `consoles` plugin helped recover command-prompt history and the encoded string associated with Flag 1. The `memdump` plugin extracted the Paint process memory for investigating Flag 2. The `filescan` and `dumpfiles` plugins helped locate and extract the archive containing Flag 3, while `hashdump` provided account hash information relevant to its password.

## 5. Conclusion
The investigation used process analysis, console history, memory extraction, and file recovery to investigate the Windows memory image. The recovered flags and screenshots provide evidence of the findings.
