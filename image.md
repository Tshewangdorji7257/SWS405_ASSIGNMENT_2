Part A — Installation and setup
![alt text](image.png)

Update Kali and install the required tools
![alt text](image-1.png)

Check whether Python 2 installed
![alt text](image-2.png)

Step 3 — Download Volatility 2
![alt text](image-3.png)

![alt text](image-4.png)

Step 4 — Verify Volatility 2
![alt text](image-5.png)

Step 5 — Check the command works
![alt text](image-6.png)
![alt text](image-7.png)

check volatility
![alt text](image-8.png)


Download the Lab File
Open the official MemLabs repository
Open the repository.
Find the folders for Lab 1 through Lab 5
Open the Lab 1 folder first.
Read its README and click the memory-image download link, which may lead to Google Drive or Mega.
Download the archive. Repeat for Labs 2–5 when you're ready.
![alt text](image-10.png)
![alt text](image-9.png)
![alt text](image-11.png)

Create folders for Labs 1–5
![alt text](image-12.png)

Extract Lab into this folder
![alt text](image-13.png)
![alt text](image-14.png)

Check all five lab folders
![alt text](image-15.png)


lab 1 
Run imageinfo
![alt text](image-16.png)

List running processes (pslist)
![alt text](image-17.png)
![alt text](image-18.png)

Examine the process tree (pstree)
![alt text](image-19.png)
![alt text](image-20.png)

Save your investigation evidence
![alt text](image-21.png)

Display the process list
![alt text](image-22.png)
![alt text](image-23.png)

Display the process tree
![alt text](image-24.png)
![alt text](image-25.png)

. What we found
From your actual output:
Process	PID	What it tells us
explorer.exe	2504	Windows desktop shell for one user session
WinRAR.exe	1512	An archive utility was running
cmd.exe	1984	A command prompt was running
mspaint.exe	2424	Microsoft Paint was running
DumpIt.exe	796	A memory-dumping utility was running
Important clue: WinRAR.exe is particularly worth investigating because Lab 1 involves a password-protected archive. However, this alone does not prove which archive was opened or reveal its password.
Your process tree also shows that WinRAR.exe and mspaint.exe are children of explorer.exe PID 2504 and cmd.exe is under explorer.exe PID 604. These are separate desktop sessions, so we should avoid assuming they belong to the same user activity.

Next: inspect command history
investigate whether the user typed commands that reveal the archive location or password.
![alt text](image-26.png)
![alt text](image-28.png)
![alt text](image-27.png)

Save the results for your report
![alt text](image-29.png)

Display the results:
![alt text](image-30.png)
![alt text](image-31.png)

Revealed an important clue: a Base64-encoded flag.
![alt text](image-32.png)

flag1
Decode the string in Kali
![alt text](image-33.png)

Save the evidence
![alt text](image-34.png)

flag 2
Find the MSPaint process
![alt text](image-127.png)
![alt text](image-128.png)

Dump the process memory
![alt text](image-129.png)
![alt text](image-130.png)

Identify the dumped file
![alt text](image-131.png)
![alt text](image-132.png)

Search for bitmap headers
![alt text](image-133.png)

Check the bitmap headers
![alt text](image-134.png)

Extract the BMP
![alt text](image-135.png)

Find other possible bitmap images
![alt text](image-139.png)

Check the MSPaint dump for image-related data
![alt text](image-140.png)


Open the raw dump in GIMP

![alt text](image-136.png)
![alt text](image-137.png)
![alt text](image-138.png)



third flag
Run filescan
![alt text](image-37.png)

Search for interesting files
![alt text](image-38.png)
![alt text](image-39.png)

Dump Important.rar from memory
![alt text](image-40.png)

Step 7: Check the extracted file
![alt text](image-41.png)

Test the recovered RAR archive
![alt text](image-42.png)

Extract the archive
![alt text](image-43.png)

Recover Windows password hashes
![alt text](image-44.png)

Extract flag3.png
![alt text](image-45.png)

extraction succeeds, check the file:
![alt text](image-46.png)

flag3
![alt text](image-36.png)


lab2
Check your Lab 2 files
![alt text](image-47.png)

Identify the memory profile
![alt text](image-48.png)

Save the initial investigation results
![alt text](image-49.png)

Find the interesting evidence
![alt text](image-50.png)
![alt text](image-51.png)
![alt text](image-52.png)

Look for the KeePass database/Look at the environment variables
![alt text](image-53.png)
![alt text](image-54.png)

lists variable names that appear in the file and drops the common ones by exact name:
![alt text](image-55.png)

Variables that appear only once or twice are the custom ones. Standard ones show up dozens of times. Look for an odd name in that list, then show its full line
![alt text](image-56.png)

copy only the value, the part after NEW_TMP, and decode it:
flag1
![alt text](image-57.png)

Find the password database
This searches the file-scan results for KeePass database files and possible deleted-record clues.
![alt text](image-58.png)

Extract Hidden.kdbx
![alt text](image-59.png)

Check the extracted file
![alt text](image-60.png)

Compare the two KeePass files
Check the KeePass database files
![alt text](image-61.png)

Compare the database files
![alt text](image-62.png)

Open the recovered database
![alt text](image-63.png)

Check Password.png
![alt text](image-64.png)
![alt text](image-65.png)

flag
![alt text](image-66.png)

### Recovery of the Second Flag

The second flag was recovered from a KeePass password database named `Hidden.kdbx`. The database was identified in the memory image using Volatility 2.6.1 and extracted with the `dumpfiles` plugin. The database was opened using KeePass 2 after locating the password clue in `Password.png`. Inside the database's **Recycle Bin** group, an entry titled `Sabka Baap` with the username `Flag` contained the second flag. The entry's creation and modification timestamps were recorded as supporting forensic evidence.

Find the third flag
check which browser processes were present in memory:
![alt text](image-67.png)

search your existing file-scan output for browser-related artifacts
![alt text](image-68.png)
![alt text](image-69.png)
![alt text](image-70.png)

Extract Chrome History
![alt text](image-71.png)

Identify the extracted file
![alt text](image-72.png)

Check the extracted SQLite database
![alt text](image-73.png)

Check the database integrity/If the urls table exists
![alt text](image-74.png)
![alt text](image-75.png)

Record the MEGA link and downloaded the file
![alt text](image-76.png)

Locate the ZIP file / Inspect the archive without extracting it
![alt text](image-77.png)

Extract the inner ZIP
![alt text](image-78.png)
![alt text](image-79.png)

Recalculate the hash
![alt text](image-83.png)
Retry extraction
![alt text](image-81.png)

Verify and open the image
![alt text](image-82.png)
![alt text](image-80.png)

### Lab 2 — A New World: Investigation Summary

I analysed the Windows 7 memory image using Volatility 2.6.1 and identified the `Win7SP1x64` profile. First, I examined the environment variables and discovered an unusual `NEW_TMP` value containing Base64-encoded data. Decoding this value revealed the first flag.

Next, I located and extracted the KeePass database (`Hidden.kdbx`). I used the password clue recovered from `Password.png` to open the database and examined its Recycle Bin, where I found the second flag in a recovered entry.

Finally, I investigated Chrome browser history using the community `chromehistory` plugin and identified a MEGA folder link. I downloaded `Important.zip` and inspected its archive comment, which instructed me to derive the password using the lowercase SHA-1 hash of the stage-3 flag from Lab 1. After calculating the correct hash, I successfully extracted `Important.png` and recovered the third flag.

lab3
Identify the memory profile
![alt text](image-84.png)

Identify running processes
![alt text](image-85.png)
![alt text](image-86.png)
![alt text](image-87.png)

Check the Notepad processes
![alt text](image-88.png)
![alt text](image-89.png)

![alt text](image-90.png)
![alt text](image-91.png)

Find the suspicious files
![alt text](image-92.png)

Find the hidden image
![alt text](image-93.png)
![alt text](image-94.png)

check running process
![alt text](image-95.png)

Extract vip.txt
![alt text](image-96.png)

Read the extracted text file
![alt text](image-97.png)

Decode the text/Apply XOR with 3
first part of the flag
inctf{0n3_h4lf
![alt text](image-98.png)

Extract the hidden text and Read the extracted message
![alt text](image-99.png)
![alt text](image-100.png)

4. Combine the flag parts
The published Lab 3 solution indicates the second part is _1s_n0t_3n0ugh}. If your extracted message confirms that, 
the complete flag is: inctf{0n3_h4lf_1s_n0t_3n0ugh}

lab4
Check your Lab 4 folder and identify the correct profile
![alt text](image-101.png)
![alt text](image-102.png)

Inspect running processes
![alt text](image-103.png)

Search for the deleted file
![alt text](image-104.png)

Run pstree with the correct profile
![alt text](image-105.png)

search for the important file
![alt text](image-106.png)

Try dumping Important.txt
![alt text](image-107.png)

Parse the MFT
![alt text](image-108.png)

Find Important.txt in the report
![alt text](image-109.png)
![alt text](image-110.png)

decode these hex bits using CyberChefOH 
finally we can retrieve the flag
![alt text](image-111.png)


lab 5
Check your Lab 5 files and Identify the correct memory profile
![alt text](image-112.png)

Check running processes
![alt text](image-113.png)

Find the file paths used by processes
![alt text](image-114.png)
![alt text](image-115.png)

Check Internet Explorer history
![alt text](image-116.png)


Locate the RAR archive in memory
![alt text](image-118.png)

Extract the RAR archive
![alt text](image-119.png)
![alt text](image-120.png)

Decode the Stage 1 password/flag
![alt text](image-121.png)

Extract the Stage 2 flag
![alt text](image-122.png)
![alt text](image-123.png)
![alt text](image-124.png)

Check the image and got the flag 2
![alt text](image-126.png)
![alt text](image-125.png)

**Lab 5: Black Tuesday — Investigation Log**

**Objective:** Recover two flags from a Windows 7 memory image. The first flag is used as the password to unlock an archive containing the second flag.

**Step 1: Identify the memory profile and running processes**

I examined `MemoryDump_Lab5.raw` using Volatility's `imageinfo` and `pslist` plugins. The memory profile identified was `Win7SP1x64`. The process list showed `WinRAR.exe`, which indicated that an archive may have been open when the memory image was captured.

**Step 2: Locate and extract the archive**

I used Volatility's `filescan` plugin to search for files associated with the archive. I located `SW1wb3J0YW50.rar` in the SmartNet user's Documents directory and extracted it from memory using `dumpfiles`.

**Step 3: Investigate browser history**

I examined the browser history using Volatility's `iehistory` plugin. The history contained unusually long filenames that appeared to be Base64-encoded strings. I decoded the relevant filename and recovered the first flag.

**Step 4: Unlock the archive**

I used the recovered first flag as the archive password with `unrar`. The password was accepted, and the archive extracted `Stage2.png`.

**Step 5: Recover the second flag**

I examined the extracted `Stage2.png` file and recovered the second flag.

**Results**

- Flag 1: `flag{!!_w3LL_d0n3_St4g3-1_0f_L4B_5_D0n3_!!}`
- Flag 2: `flag{W1th_this_$taGe_2_ 1s_c0mPL3T3_!!}`

