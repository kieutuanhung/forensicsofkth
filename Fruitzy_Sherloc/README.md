Sherlock: Fruitzy
Difficult: Easy
Sherlock Scenario:
CyberJunkie started out as a junior QA Analyst at his friend's startup. He called the CEO of the startup because he believed he had mistakenly downloaded something malicious. The CEO sought help from you, his friend in the cybersecurity field. You sent him a guide on collecting evidence from the machine using KAPE. Now you have been given the forensic image so you can analyze and help your friends, as they cannot afford to hire an MSSP.
File: Fruitzy.zip
Task 1: What is the Subject/topic of the Phishing email?
        Download and extract file, i see 
        <img width="1218" height="493" alt="image" src="https://github.com/user-attachments/assets/cd605d7f-0e89-49e5-8866-b3ffe4253883" />
        i open Special Party Invitation from JANET CARNAHAN.eml with Notepad and find Subject. I see
        <img width="539" height="101" alt="image" src="https://github.com/user-attachments/assets/e5b63a1b-35c5-4d05-ad8c-6c8a60a3fdab" />
        and Task 1 is: Special Party Invitation from JANET CARNAHAN
 Task 2: What is the malicious URI that the malicious link redirected to?
        i see
        <img width="533" height="92" alt="image" src="https://github.com/user-attachments/assets/50aeedd7-4d5c-4364-9d63-87aceba1b894" />
        in Special Party Invitation from JANET CARNAHAN
        and it has something. I have "pomi.digital"
        The user clicks the link in the email.
        That link redirects to a different address.
        You need to find that final address.
        so i find in C:/ file 
        <img width="611" height="43" alt="image" src="https://github.com/user-attachments/assets/a8fea697-1a94-4773-b938-6a9e9764cc13" />
        open it, and find with keyword is "download". Remember, i had "pomi.digital"
        <img width="506" height="178" alt="image" src="https://github.com/user-attachments/assets/43aec243-3575-4fc4-8fdd-0ea2cbbced6b" />
        this is answer: https://pomi.digital/premium/windows_download.php
  Task 3: What is the name of the downloaded file?
        <img width="935" height="145" alt="image" src="https://github.com/user-attachments/assets/ce1512da-807d-48fc-af2e-0a5cc22bf9c8" />
        i also find with "download" in Special Party Invitation from JANET CARNAHAN
        and "premium.exe" is answer
  Task 4: When was the downloaded file executed by the victim according to Amcache?
        i open Amcache.hveLOG1 with Registry Explore
        <img width="538" height="370" alt="image" src="https://github.com/user-attachments/assets/b40a2c7c-57db-46d1-967f-bcf0b945b009" />
        Then, i find with keyword "premium.exe" 
        <img width="944" height="111" alt="image" src="https://github.com/user-attachments/assets/d36ff959-6f64-43e8-95c5-0830466a4ce9" />
        So i have "2026-03-04 16:44:33"
  Task 5: What is the SHA256 hash of the malicious executable downloaded from the phishing Website?
        i also find "premium" in file "History" and i see
        <img width="952" height="125" alt="image" src="https://github.com/user-attachments/assets/df100d77-fe10-403c-a589-199d261dbaa8" />
        so i have MD5: b7f8099a29195303b8dbedec07a28bd0
        then, i find in VirusTotal.
        <img width="911" height="472" alt="image" src="https://github.com/user-attachments/assets/f0326e52-4a8e-443e-9e52-f47a12aa2c28" />
        yeah, finally
        <img width="716" height="344" alt="image" src="https://github.com/user-attachments/assets/1611a424-6722-45ee-9c10-4e9acdf77bb8" />
        SHA-256 here: af240a2c2a4b42e3a130f47ccaab9aa2e20a1a586bc959ee9efd7475055ea7e3
  Task 6: The user executed the file, but no invitation appeared or was found. They then used Microsoft Defender to scan the file. When was this scan initiated?
        i open Microsoft-Windows-Windows Defender%4Operational with Event Viewer and find "premium.exe" 
        <img width="679" height="491" alt="image" src="https://github.com/user-attachments/assets/08fdfaf6-da3f-4649-8740-f4ad84ea2ca1" />
        answer is 2026-03-04 16:48:00
  Task 7: The malware installed a Remote Monitoring and Management (RMM) tool as a backdoor for potential remote access. What was the service name?
        i open System.evtx, filter with ID 7045, and look at the Date and Time column and make sure it's closest to the time of Task 6.
        <img width="805" height="477" alt="image" src="https://github.com/user-attachments/assets/d10f3267-6a98-4240-8941-3ab19ab7531e" />
        It's: CentraStage
  Task 8: The malicious backdoor installation time stomped the RMM executables. What was the modified timestamp set to these executables?
        i open $MFT and find "CagService.exe". Then i see column "Last Modifiedx10"
        <img width="923" height="333" alt="image" src="https://github.com/user-attachments/assets/3cee0af6-3cdc-47a8-b3fd-261378c466e6" />
        2026-02-09 07:56:40 is my answer.
   Task 9: What is the name of the company whose product is the RMM tool?
        This is Datto. I can find it on Google
  Task 10: Pivoting back to the malicious link, when was the domain registered?
        <img width="953" height="442" alt="image" src="https://github.com/user-attachments/assets/777b8d4e-6a9a-4ca7-b332-945044057f8e" />
        i find pomi.digital on WHOIS Lookup
        2026-02-20 01:06:05
  Task 11: Utilizing threat intelligence sources, what is another name for the executable that was initially downloaded?
        we can find on VirusTotal by using SHA-256
        <img width="854" height="242" alt="image" src="https://github.com/user-attachments/assets/9b6c993b-df2a-4f35-bc2a-d902d09124df" />
        It is 5bxrx.exe
        That's all
        <img width="1707" height="483" alt="image" src="https://github.com/user-attachments/assets/f26bcd8b-90e3-4f9c-841d-a4d1e0dc9154" />








  






