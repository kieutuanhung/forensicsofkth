# Reminiscent-Hack The Box
# Challenge Information
  + Platform: Hack The Box
  + Category: Forensics
  + Difficulty: Easy
# Challenge Scenario
  + Suspicious traffic was detected from a recruiter&#039;s virtual PC. A memory dump of the offending VM was captured before it was removed from the network for imaging and analysis. Our recruiter mentioned he received an email from someone regarding their resume. A copy of the email was recovered and is provided for reference. Find and decode the source of the malware to find the flag.
# Provided Information
  + reminiscent.zip (https://labs.hackthebox.com/api/v4/challenge/download/39?auth_user_id=2596063&expires=1770908177&signature=8967080f1ad07e85f7c0ae10292323800bbc857e3a165f8ac75e63c058ac26a8)
# Analysis
 + Step 1, I dowload this file and unzip it. I have a folder with name is "reminiscent". I see 3 files in this folder. 
 + Step 2, I notice the file named  "flounder-pc-memdump.elf" because i open "imageinfo.txt" and "resume.eml" and i don't see anything suspicious. I try "file flounder-pc-memdump.elf" and i realize this is a RAM exercise.
 + Step 3, I use "vol -f  flounder-pc-memdump.elf windows.info".
    <img width="1886" height="562" alt="image" src="https://github.com/user-attachments/assets/2331086e-03d3-4412-9be6-b61b4b13ef36" />
      Then, I try "vol -f flounder-pc-memdump.elf windows.pslist" to see if I could find anything interesting.
   <img width="1913" height="999" alt="image" src="https://github.com/user-attachments/assets/a4fc1d52-803c-4b31-99e0-47878a6c18b0" />

      Wow! I see "496   2044   powershell.exe   18:06:58
                  2752  496    powershell.exe   18:07:00
                  2772  396    conhost.exe      18:06:58"
      User opened explorer → spawn powershell → spawn powershell  → opened console!.
      So i'm looking at the PowerShell command with "vol -f flounder-pc-memdump.elf windows.cmdline | grep -i powershell"
      I find: 
      <img width="1891" height="752" alt="image" src="https://github.com/user-attachments/assets/85528332-45dc-4dd5-b052-81d736b0c39d" />
      HAHA! I find something.
      In the first half, I decode it with "echo 'JHN0c......' | base64 -d". I have 
      <img width="1894" height="119" alt="image" src="https://github.com/user-attachments/assets/a2c6da58-6440-4751-8100-52b24f106154" />
      And i don't have anything.
      In the second half, I decode with "echo 'JABHAH......' | base64 -d | iconv -f utf-16le -t utf-8" and wowwwww, I find: 
      <img width="1892" height="355" alt="image" src="https://github.com/user-attachments/assets/9b20b418-c80f-4a49-bede-e0c366d88470" />
      So in this, I can see this flag in the last line.
 + Step 4, Flag is "HTB{$_j0G_y0uR_M3m0rY_$}".
    




      



    


