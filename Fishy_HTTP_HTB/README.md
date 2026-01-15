# Fishy HTTP – Hack The Box
# Challenge Information
  + Platform: Hack the box
  + Challenge name: Fishy HTTP
  + Category: Forensics
  + Difficulty: Easy
# Challenge Scenario
  + I found a suspicious program on my computer making HTTP requests to a web server. Please review the provided traffic capture and executable file for analysis. (Note: Flag has two parts)
# Provided Files
  +'Fishy_HTTP.zip'
# Analysis
+Step 1, I download file and extract it. I use "unzip Fishy_HTTP.zip". After extracting, i see 2 files 'smphost.exe' and 'sustraffic.pcapng'.
+Step 2, I open 'sustraffic.pcapng' with Wireshark and filter 'http'
  <img width="1886" height="661" alt="Screenshot 2026-01-15 153916" src="https://github.com/user-attachments/assets/8067de89-0e6e-4f78-8cdd-e9bcbadd4540" />
+Step 3, I see a lot of suspicious-looking words and I thought about taking the first letters to form a base64 string.When i take the first letters of No.67, i get "IFZvbHVtZSBpbiBkcml2ZSBDIGhhcyBubyBsYWJlbC4NCiBWb2x1bWUgU2VyaWFsIE51bWJlciBpcyBBMDc5LUFERkINCg0KIERpcmVjdG9yeSBvZiBDOlxUZW1wDQoNCjA1LzA3LzIwMjQgIDA5OjIyIEFNICAgIDxESVI+ICAgICAgICAgIC4NCjA1LzA3LzIwMjQgIDA5OjIyIEFNICAgIDxESVI+ICAgICAgICAgIC4uDQowNS8wNy8yMDI0ICAwNzoyMyBBTSAgICAgICAgNjcsNTE1LDc0NCBzbXBob3N0LmV4ZQ0KICAgICAgICAgICAgICAgMSBGaWxlKHMpICAgICA2Nyw1MTUsNzQ0IGJ5dGVzDQogICAgICAgICAgICAgICAyIERpcihzKSAgMjksNjM4LDUyMCw4MzIgYnl0ZXMgZnJlZQ0KJ2g3N1BfczczNDE3aHlfcmV2U0hFTEx9JyANCg==
  <img width="1755" height="788" alt="Screenshot 2026-01-15 154554" src="https://github.com/user-attachments/assets/3649a2b7-5a4b-4a79-bf61-02b657206689" />
+Step 4, I decode it with Base64, I take 
  <img width="781" height="345" alt="Screenshot 2026-01-15 154822" src="https://github.com/user-attachments/assets/14ed16c8-81a1-4a92-a19f-66b090b5e9e8" />
  and it has 'h77P_s73417hy_revSHELL}'  this is half of the flag.
+Step 5, I use 'exiftool smphost.exe' and i see <img width="1912" height="902" alt="Screenshot 2026-01-15 155238" src="https://github.com/user-attachments/assets/33482fed-3208-4779-92be-0bfce1aa1076" />
  I see MyProject very suspicious.
+Step 6, I open 'smphost.exe' with ILSpy and try open 'main(string[])' of 'MyProject(1.0.0.0,.NETCoreApp, v8.0)'
  <img width="1391" height="812" alt="Screenshot 2026-01-15 155741" src="https://github.com/user-attachments/assets/241b1292-ed02-4068-b818-1a3d1e116324" />
  I decode "YXBwbGUKYWlycGxhbmUKYW50CmF2b2NhZG8KYXJyb3cKYXN0cm9uYXV0CmFsYXJtCmFuY2hvcgphY3JvYmF0CmFsYnVtCmJhbmFuYQpiYWxsCmJvb2sKYnV0dGVyZmx5CmJpcmQKYmVhY2gKYmFza2V0CmJpY3ljbGUKYm90dGxlCmJlYXIKY2F0CmNhcgpjYWtlCmNsb3VkCmNhbmRsZQpjb21wdXRlcgpjb29raWUKY2FtZXJhCmNsb3duCmNhc3RsZQpkb2cKZHVjawpkb29yCmRyYWdvbgpkb2xwaGluCmRpYW1vbmQKZHJ1bQpkZXNrCmRvbGwKZGlub3NhdXIKZWxlcGhhbnQKZWdnCmVhZ2xlCmVhcnRoCmVudmVsb3BlCmVuZ2luZQplbGYKZXJhc2VyCmVzY2FsYXRvcgplYXNlbApmaXNoCmZsb3dlcgpmcm9nCmZpcmUKZm94CmZsYWcKZnJ1aXQKZmVhdGhlcgpmZW5jZQpmbGFzaGxpZ2h0CmdyYXBlCmd1aXRhcgpnbG9iZQpnYW1lCmdvYXQKZ2hvc3QKZ2xhc3NlcwpnYXJkZW4KZ2VtCmdpZnQKaG91c2UKaGF0CmhlYXJ0CmhvcnNlCmhhbW1lcgpoZWxpY29wdGVyCmhvbmV5CmhhbWJ1cmdlcgpob3JuCmhlZGdlaG9nCmljZS1jcmVhbQppZ2xvbwppc2xhbmQKaW5rCmluc2VjdAppcm9uCmljZQppZ3VhbmEKaW52aXRhdGlvbgppbnN0cnVtZW50CmphY2tldApqZWxseWZpc2gKamFyCmp1bmdsZQpqdWljZQpqaWdzYXcKanVtcApqZXdlbApqZXQKamFjay1vLWxhbnRlcm4Ka2FuZ2Fyb28Ka2l0ZQprZXkKa2luZwprb2FsYQprYXlhawprZXR0bGUKa2l0Y2hlbgprZXlib2FyZAprbmlnaHQKbGVtb24KbGlvbgpsYWRkZXIKbGFtcApsZWFmCmxpZ2h0aG91c2UKbG9nCmxhcHRvcApsb2NrCmxhZHlidWcKbWFuZ28KbW9ua2V5Cm1vb24KbW91bnRhaW4KbXVzaHJvb20KbW91c2UKbWFpbGJveAptYWduZXQKbWljcm9waG9uZQptYXNrCm5vdGVib29rCm5lc3QKbmFpbApuZXQKbm9zZQpudXQKbmluamEKbmVja2xhY2UKbmV3c3BhcGVyCm5vb2RsZXMKb3JhbmdlCm93bApvY2VhbgpvY3RvcHVzCm9uaW9uCm92ZW4Kb3lzdGVyCm90dGVyCm9saXZlCm9ybmFtZW50CnBpbmVhcHBsZQpwZWFyCnBpenphCnB1bXBraW4KcGVuZ3VpbgpwZW5jaWwKcGxhbmUKcHlyYW1pZApwYW5kYQpwb3Bjb3JuCnF1ZWVuCnF1aWx0CnF1ZXN0aW9uCnF1aWxsCnF1YWlsCnF1aXZlcgpxdWFydHoKcXVldWUKcXVhcnRlcmJhY2sKcXVhZHJpbGF0ZXJhbApyYWJiaXQKcmFpbmJvdwpyb2JvdApyb2NrZXQKcmluZwpyYWNjb29uCnJ1bGVyCnJvc2UKcmFkaW8KcnVnCnN0YXIKc3VuCnNuYWtlCnNvY2sKc3Bvb24Kc3F1aXJyZWwKc2hpcApzbm93bWFuCnNwaWRlcgpzYW5kd2ljaAp0YWJsZQp0cmVlCnRpZ2VyCnR1cnRsZQp0cmFpbgp0ZWxlc2NvcGUKdG9vdGgKdHJ1bXBldAp0b21hdG8KdGFtYm91cmluZQp1bWJyZWxsYQp1bmljb3JuCnVuaWZvcm0KdXRlbnNpbAp1bml2ZXJzZQp1bmljeWNsZQp1a3VsZWxlCnVuZGVyZ3JvdW5kCnVybgp1cGhvbHN0ZXJlcgp2aW9saW4Kdm9sY2Fubwp2YW4KdmVzdAp2ZWdldGFibGUKdmluZQp2YWN1dW0KdmFzZQp2dWx0dXJlCnZpZGVvCndhdGVybWVsb24Kd2hhbGUKd29ybQp3YWdvbgp3YW5kCndpbmRtaWxsCndhdGNoCndpbmcKd2FsbGV0CndoZWVsCnh5bG9waG9uZQp4LXJheQp4ZWJlYwp4eWxpdG9sCnhlbm9uCnhhbnRoYW4KeGVyb3Npcwp4ZXJvcGh5dGUKeHlsdWxvc2UKeG1hcwp5ZWxsb3cKeWFjaHQKeW9ndXJ0CnlvbGsKeWFrCnlhd24KeXVjY2EKeW9kZWwKeXVydAp5ZXcKemVicmEKemlwcGVyCnpvbwp6aWd6YWcKemVybwp6b21iaWUKemFwCnplbGRhCnpvbmUKemVu"
  I see someone is creating a dictionary <img width="995" height="373" alt="image" src="https://github.com/user-attachments/assets/683d4c24-fd11-4086-bb4e-2147e819bbef" />
  Then, I open 'Program' of 'MyProject(1.0.0.0,.NETCoreApp, v8.0)' <img width="1588" height="803" alt="image" src="https://github.com/user-attachments/assets/96e3d339-1bd6-407b-b207-839ddb55604e" />
  These tags are crucial for decoding the HTML data found in the PCAP file.
  
+Step 6, I reopen 'sustraffic.pcapng' with Wireshark and filter 'http'. I open No.60 and decode with things of 'Program' of 'MyProject(1.0.0.0,.NETCoreApp, v8.0)'.
  I have 'HTB{Th4ts_d07n37_'
So flag is 'HTB{Th4ts_d07n37_h77P_s73417hy_revSHELL}'.




