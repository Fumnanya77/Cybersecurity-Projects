## Crack The Hash Walkthrough

For this walkthrough, I will make use of a few command-line tools: 
- hashcat
- hash-identifier
- hashid

**Resources**
https://hashcat.net/wiki/doku.php?id=hashcat - The hashcat documentation


### Level 1

For this level's hashes, I will advise you to use an online hash cracking tool to save time. It will be able to crack 80% of it. But if you think there is some virtue in manually cracking it, I think I can offer a little assistance.

1. 48bb6e862e54f2a795ffc4e541caed4d </br>
   Hint: **md5**, mode: 0. *Reference the hashcat document to find the correct hash mode numbers for the hashes* </br>
   `hashcat -m 0 48bb6e862e54f2a795ffc4e541caed4d rockyou.txt` ====> **easy**

2. CBFDAC6008F9CAB4083784CBD1874F76618D2A97 </br>
   Hint:sha... no version. </br>
   Using the hash-identifier tool, it is **SHA-1**, mode: 100 </br>
   `hashcat -m 100 CBFDAC6008F9CAB4083784CBD1874F76618D2A97 rockyou.txt` ====> **password123**

3. 1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032 </br>
    Hint:sha... no version. </br>
    Using the hash-identifier tool, it is **SHA-256**, mode: 1400 </br>
   `hashcat -m 1400 1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032 rockyou.txt` ====> **letmein**

4. $2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom </br>
   Here, hint: (https://hashcat.net/wiki/doku.php?id=example_hashes) to help us identify the hash type. It was pretty easy to find the one with the $2a$..$... </br>
   The hashtype: **Bycrypt**, mode: 3200 </br>
   `hashcat -m 3200 hash.txt rockyou.txt` ====> **bleh**

5. 279412f945939ba78ce0758d3fd83daa </br>
   Hint: **md4**, mode: 900, but the word is not in the rockyou.txt, so I slightly modified the wordlist using one of the hashcat rules. </br>
   `hashcat -m 900 279412f945939ba78ce0758d3fd83daa rockyou-12less.txt -r /usr/share/hashcat/rules/best64.rule` ====> **Eternity22**

### Level 2
An online hash-cracking tool can help with the first and second hashes on this level

1. F09EDCB1FCEFC6DFB23DC3505A882655FF77375ED8AA2D1C13F640FCCC2D0C85 </br>
   The hash-identifies tool identifies it as **SHA-256**, mode: 1400 </br>
   `hashcat -m 1400 F09EDCB1FCEFC6DFB23DC3505A882655FF77375ED8AA2D1C13F640FCCC2D0C85 rockyou.txt` ====> **paule**

2. 1DFECA0C002AE40B8619ECF94819CC1B </br>
   Hint: **NTLM**, mode:1000 </br></br>
   `hashcat -m 1000 1DFECA0C002AE40B8619ECF94819CC1B rockyou.txt` ====> **n63umy8lkf4i**

3. $6$aReallyHardSalt$6WKUTqzq.UQQmrm0p/T7MPpMbGNnzXPMAXi4bJMl9be.cfi3/qxIf.hsGpS41BqMhSrHVXgMpdjS6xeKZAs02. </br>
   This is a salted hash. Seeing the nature of the hash, I went straight to the hash example resource to identify the correct hash type. **SHA-512** mode:1800. </br>
   It is advised you put the hashes in a file, but if must paste it directly on the command line, you would have to add the escape character \ to make it work. </br>
   `hashcat -m 1800 \$6\$aReallyHardSalt\$6WKUTqzq.UQQmrm0p/T7MPpMbGNnzXPMAXi4bJMl9be.cfi3/qxIf.hsGpS41BqMhSrHVXgMpdjS6xeKZAs02. rockyou.txt` ====> waka99 </br>
   **NB:** Don't leave out the full stop.

4. e5d8870e5bdd26602cab8dbe07a942c8669e56d6  - salt: tryhackme </br>
   Hint: **HMAC-SHA1**, but the mode is dependent on the position of the key. The key places behind the hash, and therefore the mode is 160 </br>
   `hashcat -m 160 e5d8870e5bdd26602cab8dbe07a942c8669e56d6:tryhackme rockyou.txt` ====> 481616481616 </br>

Bonus point - Shorten the rockyou.txt wordlist to decrease cracking time.
